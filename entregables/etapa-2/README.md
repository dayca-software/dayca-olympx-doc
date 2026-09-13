# Entregables Etapa 2

## Backend, Base De Datos Y Autenticacion

| Campo              | Valor                                                       |
| ------------------ | ----------------------------------------------------------- |
| Duracion           | Semanas 2-4                                                 |
| Horas cotizadas    | 160 h                                                       |
| Estado             | Casi completa                                               |
| Criterio de cierre | Rutas críticas estables, contrato uniforme y seguridad base |

## Entregables

| Entregable                   | Documento                                                                | Estado                           |
| ---------------------------- | ------------------------------------------------------------------------ | -------------------------------- |
| Backend, datos y API         | [`01-backend-datos-api.md`](./01-backend-datos-api.md)                   | Cubierto                         |
| Autenticación y verificación | [`02-autenticacion-verificacion.md`](./02-autenticacion-verificacion.md) | Cubierto con hardening pendiente |
| Checklist técnico            | [`Etapa2Checklist.md`](../../etapas/Etapa2Checklist.md)                  | Disponible                       |
| Resumen para cliente         | [`Etapa2Cliente.md`](../../etapas/Etapa2Cliente.md)                      | Disponible                       |

## Criterio De Aprobacion

- `GET /api/health` responde correctamente.
- Login, registro y consulta de sesión entregan respuestas válidas.
- El login Admin valida rol y entrega token.
- El modelo Prisma sostiene autenticación y perfil.
- Las rutas principales responden mediante `ApiEnvelope<T>`.
- Hay validación de entrada, hash de contraseñas, headers de seguridad y rate limiting.

## Pendiente De Cierre

- OAuth Google y Apple, solo si se mantienen dentro del alcance aprobado.
- Hardening adicional y pruebas de regresión de autenticación.
- Entrega real de recuperación de contraseña y validación del deep link con proveedor configurado.
- Verificación de email y refresh token si se mantienen dentro del alcance aprobado.
- Alinear PBKDF2 con RNF-002, que actualmente exige bcrypt costo 12.
- OAuth solo si se mantiene dentro del alcance aprobado.
