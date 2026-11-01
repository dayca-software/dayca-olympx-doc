# Staging OlympX — AWS + Neon

Checklist para levantar un staging aislado de **API + PostgreSQL** sin mezclar datos, secretos ni state
con desarrollo o producción.

## Alcance

- API NestJS en ECS Express Mode sobre Fargate.
- Imagen API en ECR.
- PostgreSQL administrado en un proyecto/branch Neon separado.
- Migraciones Prisma ejecutadas por el contenedor antes de iniciar la API.
- Sin web, admin, mobile ni Firebase obligatorio en el primer corte.

Stack Terraform: `olympx-devops/terraform/environments/staging`.

## 1. Prerrequisitos

- [ ] Cuenta AWS confirmada y región elegida.
- [ ] Terraform `>= 1.10` instalado.
- [ ] AWS CLI autenticado con permisos de bootstrap ECR, IAM, ECS Express, Secrets Manager y CloudWatch Logs.
- [ ] Proyecto Neon separado de desarrollo/producción.
- [ ] Usuario/base Neon creados y conexiones verificadas desde una máquina autorizada.
- [ ] Repositorio GitHub y branch de staging definidos para el workflow posterior.
- [ ] Si `olympx-contracts` es privado, crear `CONTRACTS_READ_TOKEN` como secret de GitHub con permiso de
      lectura únicamente para ese repositorio.
- [ ] Dominio HTTPS opcional para la API; ECS Express entrega una URL HTTPS temporal.

Comprobación local antes de provisionar:

```bash
aws sts get-caller-identity
terraform version
```

No continuar si AWS devuelve una cuenta o región equivocada.

## 2. Neon

Crear una base separada, por ejemplo `olympx-staging`. No reutilizar `olympx_dev` ni producción.

- `DATABASE_URL`: URL que usará la API y el arranque de Prisma.
- `DIRECT_URL`: conservar la URL directa para el procedimiento futuro de migraciones si se habilita en
  el datasource Prisma; no publicarla ni guardarla en Git.

Antes del deploy, confirmar que el usuario de la URL tiene permisos para crear tablas y aplicar las 36
migraciones actuales. El contenedor ejecutará `prisma migrate deploy`; no usar `prisma db push` en staging.

## 3. Secrets Manager

Crear secretos individuales en la región elegida. Los valores nunca deben entrar a `terraform.tfvars`.

| Variable runtime | Nombre sugerido               |
| ---------------- | ----------------------------- |
| `DATABASE_URL`   | `olympx/staging/DATABASE_URL` |
| `JWT_SECRET`     | `olympx/staging/JWT_SECRET`   |
| `REVENUECAT_WEBHOOK_SECRET` | `olympx/staging/REVENUECAT_WEBHOOK_SECRET` |

Opcionales para una segunda iteración:

- `FIREBASE_PROJECT_ID`
- `FIREBASE_CLIENT_EMAIL`
- `FIREBASE_PRIVATE_KEY`
- `PASSWORD_RESET_WEBHOOK_URL`
- `PASSWORD_RESET_WEBHOOK_AUTH_TOKEN`

`REVENUECAT_WEBHOOK_SECRET` y `PASSWORD_RESET_WEBHOOK_AUTH_TOKEN` deben entrar como secretos
adicionales del task definition. `PASSWORD_RESET_WEBHOOK_URL` es una variable runtime no sensible.

El primer staging puede operar sin Firebase; la API mantendrá push deshabilitado de forma segura.

## 4. State Terraform

Crear una sola vez un bucket S3 de state con cifrado, versionado y bloqueo. No reutilizar el state de
producción. Copiar los ejemplos y reemplazar únicamente valores locales:

```bash
cd olympx-devops/terraform/environments/staging
cp terraform.tfvars.example terraform.tfvars
cp backend.hcl.example backend.hcl
```

Editar `terraform.tfvars`:

- `aws_region`.
- ARNs reales de `DATABASE_URL` y `JWT_SECRET`.
- `APP_URL`/`CORS_ORIGIN` si existe dominio HTTPS.
- `github_repository` y `github_oidc_enabled` solo después de confirmar el repositorio.

Inicializar y validar sin crear recursos de aplicación:

```bash
terraform init -backend-config=backend.hcl
terraform fmt -recursive
terraform validate
terraform plan
```

## 5. Bootstrap de ECR y ECS Express Mode

La primera imagen debe existir antes de crear ECS Express:

```bash
terraform apply -target=module.ecr
```

Publicar la imagen desde la raíz del workspace:

```bash
aws ecr get-login-password --region <region> \
  | docker login --username AWS --password-stdin <account>.dkr.ecr.<region>.amazonaws.com
docker build --platform linux/amd64 -f olympx-api/Dockerfile \
  -t <account>.dkr.ecr.<region>.amazonaws.com/conquest-api-staging:staging .
docker push <account>.dkr.ecr.<region>.amazonaws.com/conquest-api-staging:staging
```

Crear el resto del stack:

```bash
terraform plan -out=staging.tfplan
terraform apply staging.tfplan
terraform output ecs_express_service_url
```

El despliegue debe dejar el servicio ECS Express en estado `ACTIVE` con una tarea `RUNNING`. El `start.sh`
ejecutará `prisma migrate deploy` antes de arrancar NestJS. Los logs se consultan en
`/aws/ecs/conquest-api-staging`:

```bash
aws logs tail /aws/ecs/conquest-api-staging \
  --profile <perfil-staging> \
  --region <region> \
  --since 30m
```

## 6. Smoke de aceptación

Guardar la URL devuelta por Terraform como `STAGING_API_URL` sin incluirla en secretos de aplicación:

```bash
curl --fail "${STAGING_API_URL}/api/health"
curl --fail "${STAGING_API_URL}/api/docs"
```

- [x] Health responde `200`.
- [x] Logs de ECS confirman que las migraciones terminaron sin error.
- [x] Prisma aplica las 36 migraciones mediante `migrate deploy`.
- [x] Registro/login funcionan con una cuenta de prueba no productiva.
- [x] Login entrega access token y refresh token rotativo; la reutilización revoca la familia y logout revoca la sesión.
- [x] Una ruta protegida rechaza un token inválido.
- [ ] Los uploads no se consideran persistentes hasta configurar S3; no probarlos como almacenamiento
      definitivo en este primer corte.
- [ ] Mobile QA usa `https://<staging>/api` y completa login + sesión + cierre.

## 7. OIDC y deploy repetible

El rol OIDC ya está creado y el workflow manual está preparado localmente en
`olympx-api/.github/workflows/deploy-staging.yml`. No se ejecutan despliegues automáticos.

Cuando se publique el workflow, configurar en el environment protegido `staging`:

1. Secret `AWS_ROLE_TO_ASSUME`: output `github_actions_role_arn`.
2. Variables `AWS_REGION`, `ECR_REPOSITORY` y `ECS_EXPRESS_SERVICE_ARN`.
3. Ejecutar manualmente desde la rama `staging` y registrar el SHA desplegado.

## 8. Criterio de cierre

- [ ] AWS, Neon y state están separados de producción.
- [ ] Secretos no aparecen en Git, logs ni artefactos.
- [ ] Migraciones Prisma aplicadas mediante `migrate deploy`.
- [x] Health, login y una ruta protegida validados por HTTPS.
- [x] URL documentada para mobile QA.
- [ ] Rollback probado apuntando a una imagen anterior por SHA.
- [ ] Push Firebase/APNs se valida después, con credenciales y dispositivos físicos.

## Estado actual del workspace

- API en ECS Express: `ACTIVE`, con una tarea `RUNNING`.
- Revisión activa `13`, arquitectura `X86_64`, deployment `SUCCESSFUL`, digest `sha256:3409ce37…`.
- URL actual de staging: `https://co-983f7a26bfbc4020889665e1b2b8ebef.ecs.us-east-1.on.aws`.
- Health, Swagger, rutas públicas y autenticación sin token validados por HTTPS.
- 36 migraciones Prisma aplicadas; no hay migraciones pendientes.
- CORS permite únicamente el endpoint HTTPS de la API; `conquestspa.cl` no está habilitado.
- Pendiente: publicar el workflow y configurar las variables/secreto del environment de GitHub.
