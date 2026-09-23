# Etapa 6 - Checklist Conquistas, Estadisticas y Notificaciones

> Criterio minimo para considerar cerrada la Etapa 6.

## Entregables esperados

- Logros automáticos y trazables.
- Perfil con estadísticas básicas.
- Alertas push.

## Cobertura actual

- Perfil con estadísticas básicas disponible.
- Base de dashboard y notificaciones disponible.
- `AchievementUnlock` persistido con unicidad por usuario y clave de logro.
- El primer PR competitivo desbloquea `first-pr` dentro de la misma transacción de cierre de sesión.
- El usuario puede consultar logros y progreso desde `GET /api/users/me/achievements`.
- Admin puede crear un desbloqueo manual desde el detalle de usuario; la acción queda auditada.
- Las conquistas generan alerta in-app y quedan preparadas para push FCM/APNs.
- Revisions / reportes como soporte de moderación disponibles.

## Pendientes de cierre

- Automatizar el resto de logros (`sesiones`, `sets`, `tonelaje`, `posts` y `check-ins`) como eventos persistidos.
- Validar notificaciones push reales en dispositivos físicos.
- Banners o banners compartibles por logro.
- Ampliar la vinculación de conquistas con rankings, progreso y contenido compartible.

## Criterio de aprobacion

- El usuario debe poder ver su resumen de stats.
- El sistema debe reaccionar a eventos importantes (PR, conquista, recordatorio).
- Las conquistas deben poder generarse de forma automática y trazable.
- El primer evento competitivo debe producir un desbloqueo persistido y visible.
- Las notificaciones deben llegar por un canal definido; la entrega push física sigue pendiente de validación.
