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
- El cierre de una sesión persiste automáticamente `first-session`, `ten-sessions`, `hundred-sets` y `tonnage-1000`, con sesión de origen y métrica.
- La creación de posts persiste `first-post` y `five-posts`; el check-in persiste `first-checkin`, siempre respetando la unicidad por usuario y logro.
- El usuario puede consultar logros y progreso desde `GET /api/users/me/achievements`.
- Admin puede crear un desbloqueo manual desde el detalle de usuario; la acción queda auditada.
- Cada desbloqueo nuevo aparece en la bandeja in-app y dispara el intento de push FCM/APNs.
- Revisions / reportes como soporte de moderación disponibles.

## Pendientes de cierre

- Validar notificaciones push reales en dispositivos físicos.
- Banners compartibles y vinculación ampliada con rankings/contenido quedan fuera del criterio mínimo actual.

## Criterio de aprobacion

- El usuario debe poder ver su resumen de stats.
- El sistema debe reaccionar a eventos importantes (PR, conquista, recordatorio).
- Las conquistas deben poder generarse de forma automática y trazable.
- El primer evento competitivo debe producir un desbloqueo persistido y visible.
- Las notificaciones deben llegar por un canal definido; la entrega push física sigue pendiente de validación.

## Estado de cierre funcional

- **Funcional:** completo para el catálogo actual de ocho logros y sus eventos de origen.
- **Operativo:** pendiente de credenciales Firebase/APNs, dispositivos físicos y validación de staging.
