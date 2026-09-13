# Etapa 2 - Autenticacion Y Verificacion

## Funcionalidades

- Registro por email.
- Login de usuario.
- Login específico de Admin.
- Consulta del usuario autenticado.
- Persistencia de sesión mediante token JWT.
- Validación de DTOs de entrada.
- Contraseñas almacenadas con hash.
- Bloqueo de cuentas no activas.
- Control de acceso por rol.
- Normalización de email con `trim().toLowerCase()`.
- Política mínima de contraseña: 8 caracteres, una mayúscula y un número.
- Cambio de contraseña autenticado validando la contraseña actual.
- Solicitud y confirmación técnica de recuperación con token de un solo uso y expiración.
- Credenciales demo limitadas a entornos no productivos.

## Contrato JWT

```json
{
  "sub": "uuid del usuario",
  "name": "nombre visible",
  "roles": ["admin"],
  "company_uuid": "uuid del tenant"
}
```

## Contrato De Respuesta

```json
{
  "ok": true,
  "data": {},
  "message": null,
  "statusCode": 200
}
```

## Cuentas Demo

| Rol     | Email                | Contraseña     |
| ------- | -------------------- | -------------- |
| Admin   | `admin@olympx.local` | `Password123!` |
| Usuario | `user@olympx.local`  | `Password123!` |

Estas credenciales son únicamente para desarrollo y pruebas locales.

## Evidencia

- [`auth.controller.ts`](../../../olympx-api/src/modules/auth/auth.controller.ts): endpoints.
- [`auth.service.ts`](../../../olympx-api/src/modules/auth/auth.service.ts): reglas de autenticación.
- [`change-password.dto.ts`](../../../olympx-api/src/modules/auth/dto/change-password.dto.ts): validación del cambio de contraseña.
- [`request-password-reset.dto.ts`](../../../olympx-api/src/modules/auth/dto/request-password-reset.dto.ts): solicitud de recuperación.
- [`reset-password.dto.ts`](../../../olympx-api/src/modules/auth/dto/reset-password.dto.ts): confirmación de recuperación.
- [`login.dto.ts`](../../../olympx-api/src/modules/auth/dto/login.dto.ts): validación y normalización.
- [`auth.service.spec.ts`](../../../olympx-api/src/modules/auth/auth.service.spec.ts): pruebas del servicio.
- [`password-reset.service.spec.ts`](../../../olympx-api/src/modules/auth/password-reset.service.spec.ts): pruebas de tokens y expiración.
- [`Etapa2Checklist.md`](../../etapas/Etapa2Checklist.md): lista de verificación.

## Pendientes De Seguridad

- Entrega real de recuperación y validación del deep link con proveedor configurado.
- Refresh token y sesiones expiradas.
- Verificación de email.
- OAuth Google y Apple si el alcance final lo requiere.
- Alinear el PBKDF2 actual con RNF-002, que documenta bcrypt costo 12.
- Pruebas de integración y rate limiting bajo carga real.
