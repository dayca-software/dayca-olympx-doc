# OlympX - Automatizacion DevOps Con AWS Y Neon

> Diseño operativo para desarrollo y producción. No contiene credenciales ni ejecuta despliegues.

## 1. Objetivo

Automatizar validación, migraciones y despliegue de OlympX con separación clara entre `staging` y
`prod`, usando Neon para PostgreSQL y AWS para hosting, archivos, secretos y observabilidad.

## 2. Flujo General

```text
Pull Request
    |
    v
CI: lint + typecheck + tests + build + Prisma validate
    |
    +--> Merge a staging --> QA STAGING (deploy manual)
    |                        Neon Staging + AWS Staging
    |
    +--> Merge a main ------> Aprobación manual
                              |
                              v
                            Deploy PROD
                            Neon Prod + AWS Prod
```

## 3. Ambientes

| Ambiente | Branch    | Base Neon                 | AWS                            | Deploy                       |
| -------- | --------- | ------------------------- | ------------------------------ | ---------------------------- |
| Staging  | `staging` | Proyecto `olympx-staging` | Recursos con sufijo `-staging` | Manual-only para QA          |
| Prod     | `main`    | Proyecto `olympx-prod`    | Recursos con sufijo `-prod`    | Manual después de aprobación |

Las bases de datos deben ser proyectos Neon separados. Las branches de Neon se pueden usar para
pruebas efímeras, pero nunca se debe conectar producción con una branch de desarrollo.

## 4. Pipeline De Integracion Continua

Se ejecuta en cada Pull Request y antes de cualquier deploy.

### Validaciones

- Instalar dependencias con lockfile.
- Verificar formato y lint.
- Ejecutar typecheck de API, web, admin y contracts.
- Ejecutar tests unitarios y de integración disponibles.
- Ejecutar `npx prisma validate`.
- Construir API, web y admin.
- Escanear dependencias y la imagen Docker.

### Regla

Si una validación falla, no se puede hacer merge a `staging` ni a `main`.

## 5. Deploy A Staging

Se ejecuta manualmente desde la rama `staging` cuando QA necesita una nueva versión.

1. Construir la imagen de `olympx-api`.
2. Etiquetar la imagen con el SHA del commit.
3. Publicar la imagen en ECR `olympx-api-staging`.
4. Actualizar ECS Express Mode Staging con la imagen identificada por digest; el contenedor ejecuta las
   migraciones con `prisma migrate deploy` antes de iniciar NestJS.
5. Validar CloudWatch Logs y el estado `ACTIVE` con una tarea `RUNNING`.
6. Construir Web y Admin con `VITE_API_URL` de Staging cuando entren en alcance.
7. Publicar assets en S3 Staging cuando entren en alcance.
8. Invalidar la distribución CloudFront Staging cuando entre en alcance.
9. Ejecutar smoke tests contra `/api/health` y login.

## 6. Deploy A Prod

Se dispara después de mergear a `main` y aprobar el environment `production` en GitHub.

1. Reutilizar o reconstruir la imagen identificada por SHA.
2. Publicarla en ECR `olympx-api-prod`.
3. Desplegar una migración compatible contra Neon Prod mediante `prisma migrate deploy` durante el arranque
   controlado del contenedor.
4. Desplegar la API en ECS Prod cuando el entorno de producción esté provisionado.
5. Construir Web y Admin con `VITE_API_URL` de Producción.
6. Publicar assets en S3 Prod.
7. Invalidar CloudFront Prod.
8. Ejecutar smoke tests de health, autenticación y una ruta protegida.
9. Registrar el SHA desplegado y el resultado del release.

Las migraciones deben ser backward-compatible. No se deben eliminar columnas ni cambiar contratos
críticos en el mismo release que todavía usa la versión anterior de la API.

## 7. Servicios AWS

| Necesidad           | Servicio                | Separación                                     |
| ------------------- | ----------------------- | ---------------------------------------------- |
| Imagen API          | ECR                     | Repositorios `staging` y `prod`                    |
| API NestJS          | ECS Express Mode       | Servicios `conquest-api-staging` y `conquest-api-prod` |
| Web/Admin           | S3 + CloudFront         | Buckets y distribuciones separadas             |
| Archivos de usuario | S3                      | Buckets separados y privados                   |
| Secretos            | Secrets Manager         | Prefijos `staging/` y `prod/`                  |
| Identidad CI/CD     | IAM + GitHub OIDC       | Roles separados por ambiente                   |
| Logs                | CloudWatch              | Grupos separados                               |
| Alertas             | CloudWatch Alarms + SNS | Alertas de error, latencia y costo             |

ECS Express Mode reduce la operación inicial manteniendo Fargate administrado. Los servicios se mantienen
separados por ambiente y el despliegue de staging permanece bajo demanda para QA.

## 8. Secretos Y Variables

### Runtime API

Guardar en AWS Secrets Manager, nunca en GitHub ni en el repositorio:

- `DATABASE_URL`: conexión de Neon usada por runtime y `prisma migrate deploy`; para el primer staging
  debe ser una conexión directa.
- `DIRECT_URL`: reservarla como secreto adicional cuando el datasource Prisma soporte separar pooled y
  directa.
- `JWT_SECRET`.
- `CORS_ORIGIN`.
- `APP_URL`.
- Credenciales de Firebase si se habilita push real.
- Secretos de RevenueCat y otros proveedores.

### Build Web Y Admin

- `VITE_API_URL` debe apuntar al dominio de API del ambiente correspondiente.
- No incluir secretos privados en variables `VITE_*`; quedan expuestas en el bundle.

## 9. GitHub Actions

Estructura recomendada:

```text
.github/workflows/
├── ci.yml
├── deploy-staging.yml
└── deploy-prod.yml
```

### Permisos

- GitHub Actions usa OIDC para asumir un role AWS.
- No se guardan access keys permanentes.
- El role Staging solo puede operar recursos Staging.
- El role Prod requiere environment protegido y aprobación.

## 10. Rollback

### Aplicacion

- Cada deploy queda asociado a un SHA inmutable.
- Si falla el smoke test, volver a la imagen anterior.
- Conservar las últimas versiones estables en ECR.

### Base De Datos

- Las migraciones no se revierten automáticamente.
- Usar migraciones expand/contract.
- Restaurar backup solo ante incidente de datos y siguiendo un runbook.
- Probar migraciones en Neon Staging antes de producción.

## 11. Monitoreo Y Costos

- Health check periódico de la API.
- Alerta por errores 5xx.
- Alerta por latencia p95.
- Alerta por fallos de deploy.
- Budget mensual AWS con umbrales de 50%, 80% y 100%.
- Revisar consumo de Neon por proyecto.
- Mantener escalado mínimo en cero cuando el servicio lo permita.

## 12. Orden De Implementacion

1. Crear proyectos Neon `olympx-staging` y `olympx-prod`.
2. Configurar `DATABASE_URL` de staging; para el primer bootstrap usar una URL Neon directa que permita
   `prisma migrate deploy`.
3. Si se separan conexiones pooled/directa, agregar `directUrl = env("DIRECT_URL")` al datasource Prisma
   y exponer `DIRECT_URL` como secreto adicional.
4. Crear ECR, S3, CloudFront, Secrets Manager y roles OIDC.
5. Agregar Dockerfile reproducible para la API.
6. Crear workflow `ci.yml`.
7. Crear workflow `deploy-staging.yml`.
8. Validar migración y API en Staging; Web y Admin quedan para una segunda iteración.
9. Crear workflow protegido `deploy-prod.yml`.
10. Ejecutar primer release con aprobación manual.

## 13. Infraestructura Como Codigo Con Terraform

Terraform será la herramienta para versionar y reproducir la infraestructura AWS. No se deben crear
recursos permanentes manualmente fuera de Terraform, salvo el bootstrap inicial del state.

### Estructura Inicial Implementada

```text
olympx-devops/
├── terraform/
│   ├── modules/ecr/
│   ├── modules/ecs-express/
│   ├── modules/github-oidc/
│   └── environments/
│       ├── staging/
│       └── prod/
└── workflows/
    ├── ci.yml.example
    └── deploy-staging.yml.example
```

El entorno `staging` contiene ECR, ECS Express Mode, roles de ejecución e infraestructura, secrets, health
check, CloudWatch Logs y state remoto configurable. Los workflows permanecen como plantillas hasta
configurar el role OIDC y las variables protegidas del repositorio.

### Recursos Gestionados

- ECR para imágenes de la API.
- ECS Express Mode para NestJS.
- S3 y CloudFront para Web y Admin.
- S3 privado para archivos de usuarios.
- Secrets Manager.
- IAM y GitHub OIDC.
- CloudWatch, budgets y alarmas.
- Route 53 y ACM cuando exista dominio.

Neon se mantiene como proveedor externo de PostgreSQL. Sus URLs no se guardan en Terraform ni en el
repositorio; se cargan en Secrets Manager por ambiente.

### State Y Ambientes

Staging y Prod deben tener states separados, aunque inicialmente compartan una cuenta AWS:

```text
S3 Terraform State
├── olympx/staging/terraform.tfstate
└── olympx/prod/terraform.tfstate
```

La alternativa preferida a futuro es una cuenta AWS independiente para cada ambiente mediante AWS
Organizations. No se deben usar workspaces como única barrera de seguridad para Producción.

### Validaciones Terraform

Cada Pull Request debe ejecutar:

```bash
terraform fmt -check -recursive
terraform init
terraform validate
terraform plan
```

El pipeline debe ejecutar `apply` únicamente en el ambiente correspondiente:

- `staging` se usa para QA y el workflow de deploy es manual-only.
- `main` requiere aprobación manual antes de aplicar Prod.

### Bootstrap Manual Inicial

El bucket remoto de state y su cifrado deben crearse una sola vez, con acceso restringido. Después
del bootstrap, el resto de los recursos debe pasar a ser administrado por Terraform.

### Estado de implementación

- AWS staging, Secrets Manager, ECR y ECS Express Mode están provisionados con Terraform.
- El rol GitHub OIDC está creado para `dayca-software/dayca-olympx-api` y el environment `staging`.
- La imagen actual está identificada por SHA y el despliegue se ejecuta manualmente.
- El workflow local está en `olympx-api/.github/workflows/deploy-staging.yml`.
- Pendiente: publicar el workflow y configurar sus variables/secreto en GitHub.

## 14. Operación actual

1. Trabajar en la rama `staging` para QA; reservar `main` para producción.
2. Ejecutar manualmente el workflow desde `staging` cuando se publique en GitHub, o publicar manualmente la
   imagen desde la raíz.
3. Validar `/api/health`, Swagger y las migraciones antes de entregar la URL a mobile.
4. Mantener `DATABASE_URL` y `JWT_SECRET` únicamente en Secrets Manager.

## 15. Criterio De Operacion

La automatización se considera lista cuando:

- Un Pull Request bloquea merges si falla CI.
- El workflow de `staging` requiere ejecución manual.
- `main` queda reservada para Producción.
- Los secretos no están en el repositorio.
- Las migraciones se ejecutan contra la base correcta.
- El release puede identificarse y revertirse por SHA.
- Health, errores, latencia y costo tienen alertas básicas.
