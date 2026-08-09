# Etapa 2 - Checklist Backend, BD y Auth

> Criterio minimo para considerar cerrada la Etapa 2.

## Entregables esperados

- Servidor NestJS operativo.
- Modelo de datos Prisma + PostgreSQL.
- API base con health check.
- Autenticacion JWT.
- Envoltorio de respuesta estandarizado.

## Verificacion minima

- `GET /api/health` responde correctamente.
- `POST /api/auth/login` entrega token y usuario.
- `POST /api/auth/register` crea cuenta y entrega token inicial.
- `GET /api/auth/me` devuelve la sesion actual.
- `GET /api/users/me` devuelve el perfil autenticado.
- `POST /api/auth/login/admin` funciona para cuentas de admin.
- La API responde con `ApiEnvelope<T>` en rutas principales.

## Cobertura actual

- NestJS activo.
- Prisma y seed funcionando.
- Login y `me` operativos.
- Registro de usuario operativo.
- Auth admin operativo.
- Envelope `ApiEnvelope<T>` aplicado.
- Swagger, CORS, Helmet y throttling configurados.
- Contraseñas hasheadas en seed y login.

## Validaciones de calidad

- Validacion global activa con `ValidationPipe`.
- DTOs de entrada para login, perfil y ubicacion.
- Contrato compartido usado por consumers.
- Typecheck y tests basicos de API en verde.

## Pendientes de cierre

- OAuth Google y Apple si se mantiene en alcance.
- Refinar perfil de usuario y estados de error.
- Endurecimiento de seguridad y pruebas de regresion.

## Criterio de aprobacion

- Login, perfil y health deben responder de forma consistente.
- El contrato de respuesta debe ser uniforme en todas las rutas clave.
- El modelo Prisma debe sostener el flujo de autenticacion y perfil sin atajos manuales.
- Las rutas criticas deben estar cubiertas por pruebas basicas.
- El seed debe permitir probar el flujo completo sin carga manual.
- La seguridad base debe estar presente: hash de contrasena, headers y rate limiting.
