# Etapa 2 - Backend, Datos Y API

## Objetivo

Entregar una base backend operativa y extensible para soportar autenticación, perfiles y las etapas
posteriores del producto.

## Componentes Entregados

- Aplicación NestJS operativa.
- PostgreSQL y Prisma configurados.
- Seed reproducible para usuarios y datos demo.
- Health check.
- Swagger.
- CORS, Helmet, compression y throttling configurados.
- Contratos compartidos mediante `dayca-olympx-contracts`.
- Respuestas con `ApiEnvelope<T>`.

## Rutas De Verificacion

| Método | Ruta                    | Resultado esperado              |
| ------ | ----------------------- | ------------------------------- |
| GET    | `/api/health`           | Estado saludable de la API      |
| POST   | `/api/auth/login`       | Token y usuario autenticado     |
| POST   | `/api/auth/login/admin` | Token y usuario con rol `admin` |
| POST   | `/api/auth/register`    | Cuenta creada y sesión inicial  |
| GET    | `/api/auth/me`          | Usuario de la sesión actual     |
| GET    | `/api/users/me`         | Perfil autenticado              |

## Evidencia Técnica

- [`olympx-api/src/main.ts`](../../../olympx-api/src/main.ts): bootstrap, prefijo API y pipes.
- [`olympx-api/prisma/schema.prisma`](../../../olympx-api/prisma/schema.prisma): esquema Prisma.
- [`olympx-api/prisma/seed.ts`](../../../olympx-api/prisma/seed.ts): datos iniciales.
- [`AvanceAPI.md`](../../AvanceAPI.md): estado funcional del backend.

## Verificaciones Ejecutadas

- Typecheck API aprobado.
- Suite API: 21 archivos y 152 tests pasando.
- `prisma generate` y seed funcionales.
- Health check validado en entorno local.
