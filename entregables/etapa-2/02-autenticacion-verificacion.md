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
- [`login.dto.ts`](../../../olympx-api/src/modules/auth/dto/login.dto.ts): validación y normalización.
- [`auth.service.spec.ts`](../../../olympx-api/src/modules/auth/auth.service.spec.ts): pruebas del servicio.
- [`Etapa2Checklist.md`](../../etapas/Etapa2Checklist.md): lista de verificación.

## Pendientes De Seguridad

- Recuperación y cambio de contraseña.
- Refresh token y sesiones expiradas.
- Verificación de email.
- OAuth Google y Apple si el alcance final lo requiere.
- Pruebas de integración y rate limiting bajo carga real.
