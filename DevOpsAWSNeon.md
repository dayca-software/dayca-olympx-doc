# OlympX - Automatizacion DevOps Con AWS Y Neon

> Diseño operativo para desarrollo y producción. No contiene credenciales ni ejecuta despliegues.

## 1. Objetivo

Automatizar validación, migraciones y despliegue de OlympX con separación clara entre `dev` y
`prod`, usando Neon para PostgreSQL y AWS para hosting, archivos, secretos y observabilidad.

## 2. Flujo General

```text
Pull Request
    |
    v
CI: lint + typecheck + tests + build + Prisma validate
    |
    +--> Merge a develop --> Deploy DEV automático
    |                         Neon Dev + AWS Dev
    |
    +--> Merge a main ------> Aprobación manual
                              |
                              v
                            Deploy PROD
                            Neon Prod + AWS Prod
```

## 3. Ambientes

| Ambiente | Branch    | Base Neon              | AWS                         | Deploy                       |
| -------- | --------- | ---------------------- | --------------------------- | ---------------------------- |
| Dev      | `develop` | Proyecto `olympx-dev`  | Recursos con sufijo `-dev`  | Automático                   |
| Prod     | `main`    | Proyecto `olympx-prod` | Recursos con sufijo `-prod` | Manual después de aprobación |

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

Si una validación falla, no se puede hacer merge a `develop` ni a `main`.

## 5. Deploy A Dev

Se dispara después de mergear a `develop`.

1. Construir la imagen de `olympx-api`.
2. Etiquetar la imagen con el SHA del commit.
3. Publicar la imagen en ECR `olympx-api-dev`.
4. Ejecutar migraciones contra Neon Dev usando `DIRECT_URL`.
5. Desplegar la imagen en App Runner o ECS Dev.
6. Construir Web y Admin con `VITE_API_URL` de Dev.
7. Publicar assets en S3 Dev.
8. Invalidar la distribución CloudFront Dev.
9. Ejecutar smoke tests contra `/api/health` y login.

## 6. Deploy A Prod

Se dispara después de mergear a `main` y aprobar el environment `production` en GitHub.

1. Reutilizar o reconstruir la imagen identificada por SHA.
2. Publicarla en ECR `olympx-api-prod`.
3. Ejecutar migraciones compatibles contra Neon Prod.
4. Desplegar la API en App Runner o ECS Prod.
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
| Imagen API          | ECR                     | Repositorios `dev` y `prod`                    |
| API NestJS          | App Runner inicialmente | Servicios `olympx-api-dev` y `olympx-api-prod` |
| Web/Admin           | S3 + CloudFront         | Buckets y distribuciones separadas             |
| Archivos de usuario | S3                      | Buckets separados y privados                   |
| Secretos            | Secrets Manager         | Prefijos `dev/` y `prod/`                      |
| Identidad CI/CD     | IAM + GitHub OIDC       | Roles separados por ambiente                   |
| Logs                | CloudWatch              | Grupos separados                               |
| Alertas             | CloudWatch Alarms + SNS | Alertas de error, latencia y costo             |

App Runner reduce la operación inicial. ECS Fargate puede evaluarse cuando se necesiten mayor
control de red, workers, tareas programadas o despliegues más complejos.

## 8. Secretos Y Variables

### Runtime API

Guardar en AWS Secrets Manager, nunca en GitHub ni en el repositorio:

- `DATABASE_URL`: conexión pooled de Neon para runtime.
- `DIRECT_URL`: conexión directa de Neon para Prisma migrations.
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
├── deploy-dev.yml
└── deploy-prod.yml
```

### Permisos

- GitHub Actions usa OIDC para asumir un role AWS.
- No se guardan access keys permanentes.
- El role Dev solo puede operar recursos Dev.
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
- Probar migraciones en Neon Dev antes de producción.

## 11. Monitoreo Y Costos

- Health check periódico de la API.
- Alerta por errores 5xx.
- Alerta por latencia p95.
- Alerta por fallos de deploy.
- Budget mensual AWS con umbrales de 50%, 80% y 100%.
- Revisar consumo de Neon por proyecto.
- Mantener escalado mínimo en cero cuando el servicio lo permita.

## 12. Orden De Implementacion

1. Crear proyectos Neon `olympx-dev` y `olympx-prod`.
2. Configurar `DATABASE_URL` pooled y `DIRECT_URL` directa.
3. Agregar `directUrl = env("DIRECT_URL")` al datasource Prisma si se usarán ambas conexiones.
4. Crear ECR, S3, CloudFront, Secrets Manager y roles OIDC.
5. Agregar Dockerfile reproducible para la API.
6. Crear workflow `ci.yml`.
7. Crear workflow `deploy-dev.yml`.
8. Validar migración, API, Web y Admin en Dev.
9. Crear workflow protegido `deploy-prod.yml`.
10. Ejecutar primer release con aprobación manual.

## 13. Infraestructura Como Codigo Con Terraform

Terraform será la herramienta para versionar y reproducir la infraestructura AWS. No se deben crear
recursos permanentes manualmente fuera de Terraform, salvo el bootstrap inicial del state.

### Estructura Pendiente

```text
infra/aws/
├── README.md
├── bootstrap/
│   └── state/
├── modules/
│   ├── ecr/
│   ├── app-runner/
│   ├── s3-cloudfront/
│   ├── secrets/
│   ├── github-oidc/
│   └── monitoring/
└── environments/
    ├── dev/
    │   ├── main.tf
    │   ├── variables.tf
    │   ├── outputs.tf
    │   └── terraform.tfvars.example
    └── prod/
        ├── main.tf
        ├── variables.tf
        ├── outputs.tf
        └── terraform.tfvars.example
```

### Recursos Gestionados

- ECR para imágenes de la API.
- App Runner para NestJS inicialmente.
- S3 y CloudFront para Web y Admin.
- S3 privado para archivos de usuarios.
- Secrets Manager.
- IAM y GitHub OIDC.
- CloudWatch, budgets y alarmas.
- Route 53 y ACM cuando exista dominio.

Neon se mantiene como proveedor externo de PostgreSQL. Sus URLs no se guardan en Terraform ni en el
repositorio; se cargan en Secrets Manager por ambiente.

### State Y Ambientes

Dev y Prod deben tener states separados, aunque inicialmente compartan una cuenta AWS:

```text
S3 Terraform State
├── olympx/dev/terraform.tfstate
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

- `develop` puede aplicar Dev automáticamente.
- `main` requiere aprobación manual antes de aplicar Prod.

### Bootstrap Manual Inicial

El bucket remoto de state y su cifrado deben crearse una sola vez, con acceso restringido. Después
del bootstrap, el resto de los recursos debe pasar a ser administrado por Terraform.

### Pendientes Para Retomar

- Confirmar región AWS.
- Confirmar App Runner frente a ECS Fargate.
- Definir dominio y nombres de buckets.
- Crear backend remoto de Terraform.
- Crear módulos y variables por ambiente.
- Configurar roles IAM con GitHub OIDC.
- Preparar Dockerfile de la API.
- Conectar `DATABASE_URL` y `DIRECT_URL` desde Secrets Manager.

## 14. Criterio De Operacion

La automatización se considera lista cuando:

- Un Pull Request bloquea merges si falla CI.
- `develop` despliega Dev sin intervención manual.
- `main` requiere aprobación antes de Producción.
- Los secretos no están en el repositorio.
- Las migraciones se ejecutan contra la base correcta.
- El release puede identificarse y revertirse por SHA.
- Health, errores, latencia y costo tienen alertas básicas.
