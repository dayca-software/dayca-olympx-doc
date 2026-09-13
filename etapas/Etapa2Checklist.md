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
- `PATCH /api/auth/password` cambia la contraseña con autenticación y contraseña actual válida.
- `POST /api/auth/password/request` responde sin enumerar cuentas y crea recuperación para usuarios activos.
- `POST /api/auth/password/reset` consume un token válido una sola vez.
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
- Política mínima de contraseña aplicada en registro y cambio de contraseña.
- Cambio de contraseña autenticado disponible y cubierto por regresiones.

## Validaciones de calidad

- Validacion global activa con `ValidationPipe`.
- DTOs de entrada para login, perfil y ubicacion.
- Contrato compartido usado por consumers.
- Typecheck y tests basicos de API en verde.
- Recuperación técnica con token de un solo uso, expiración y entrega desacoplada disponible.
- Throttling global activo con límites específicos para recuperación.
- Smoke HTTP local validó health, login, login admin, sesión, perfil, recuperación y rechazo `429` por burst.

## Pendientes de cierre

- Entrega real del email de recuperación y deep link con proveedor configurado.
- Verificación de email y refresh token si se mantienen en alcance.
- OAuth Google y Apple si se mantiene en alcance.
- Alinear el algoritmo implementado (PBKDF2) con RNF-002, que actualmente documenta bcrypt costo 12.
- Refinar perfil de usuario y estados de error.
- Endurecimiento de seguridad y pruebas de regresion.

## Criterio de aprobacion

- Login, perfil y health deben responder de forma consistente.
- El contrato de respuesta debe ser uniforme en todas las rutas clave.
- El modelo Prisma debe sostener el flujo de autenticacion y perfil sin atajos manuales.
- Las rutas criticas deben estar cubiertas por pruebas basicas.
- El seed debe permitir probar el flujo completo sin carga manual.
- La seguridad base debe estar presente: hash de contrasena, headers y rate limiting.
