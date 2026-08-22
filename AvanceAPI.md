# OlympX API - Avance Actual

> Estado tecnico y funcional de `olympx-api` al dia de hoy.

## 1. Objetivo

Documentar el avance real del backend para dejar claro que endpoints ya estan disponibles, que contratos soporta y que partes del MVP ya quedan cubiertas por la API.

## 2. Estado General

La API ya esta alineada con NestJS + Prisma + PostgreSQL y expone el contrato unificado basado en `ApiEnvelope<T>`.

Hoy cubre:

- Autenticacion con login, registro y consulta de usuario actual.
- Resumen para home mobile.
- Catalogo, busqueda y detalle de gimnasios.
- Feed social con publicaciones, comentarios y likes.
- Reacciones fitness y reportes de publicaciones.
- Ranking de usuarios.
- Alertas sobre actividad en publicaciones con marcado de vistas.
- Perfil, avatar y ubicacion del usuario.
- Perfiles publicos con estadisticas y publicaciones.
- Seguimiento entre usuarios.
- Feed personalizado por usuarios seguidos.
- Actividad reciente de gimnasios.
- Registro y consulta de sesiones de entrenamiento.
- Progreso de entrenamiento con volumen, reps, semanas y 1RM estimado.
- Rangos configurados de fuerza en los PRs: rango actual, siguiente rango y kilogramos restantes.
- Rutinas persistentes y sesiones iniciadas desde plantilla.
- Ranking competitivo por ejercicio basado en mejor 1RM estimado.
- Perfil editable con nickname, región, provincia y comuna persistidos.
- Edicion y eliminacion segura de sesiones propias.
- Suscripcion, trial y catalogo comercial.
- Webhook RevenueCat valida el entitlement configurado y mantiene acceso hasta el fin del periodo cuando hay cancelacion.
- Límites comerciales rolling de 30 días aplicados para sesiones, gimnasios y ejercicios.
- Endpoint de uso comercial: `GET /api/subscriptions/me/limits`.
- Onboarding persistido con validación de perfil mínimo y gimnasio principal.
- Resumen de administracion.
- Health check y Swagger.

## 3. Modulos Implementados

### Auth

- `POST /api/auth/login`
- `POST /api/auth/register`
- `GET /api/auth/me`
- `PATCH /api/users/me/onboarding/complete`
- Soporta token bearer y flujo de sesion para mobile.

### Users

- `GET /api/users/me`
- `PATCH /api/users/me`
- `POST /api/users/me/avatar`
- `PATCH /api/users/me/location`
- `GET /api/users/me/stats`
- `GET /api/users/me/achievements`
- `GET /api/users/me/check-ins`
- `GET /api/users/:id`
- `PATCH /api/users/me/gym`
- `POST /api/users/:id/follow`
- `GET /api/users/:id/followers`
- `GET /api/users/:id/following`

### Home

- `GET /api/home/summary`
- Entrega usuario, gimnasios sugeridos, publicaciones recientes y sesiones recientes.

### Gyms

- `GET /api/gyms`
- `GET /api/gyms/nearby`
- `GET /api/gyms/:id`
- `POST /api/gyms/:id/check-in`
- exige coordenadas, gimnasio activo/verificado, distancia máxima configurable y evita duplicados durante 30 minutos.
- `GET /api/gyms/:id/activity`

### Search

- `GET /api/search`

### Leaderboard

- `GET /api/leaderboard`
- acepta `period=all|30d` y `scope=global|gym`.
- devuelve la posición y puntuación del usuario actual.

### Notifications

- `GET /api/notifications`
- `POST /api/notifications/viewed`
- Las alertas incluyen likes, comentarios, reacciones fitness y nuevos seguidores.
- `GET /api/notifications?type=all|like|comment|reaction|follow`
- `POST /api/notifications/viewed/all`
- `POST /api/notifications/devices`
- `POST /api/notifications/devices/disable`
- Firebase Admin envia notificaciones dirigidas a todos los `PushDevice` activos del usuario.
- Los tokens invalidos se desactivan automaticamente sin romper la accion social.

### Posts

- `GET /api/posts`
  - soporta `scope=all|following`
- `POST /api/posts`
- `PATCH /api/posts/:id`
- `DELETE /api/posts/:id`
- `GET /api/posts/:id`
- `POST /api/posts/:id/comments`
- `POST /api/posts/:id/like`
- `POST /api/posts/:id/reactions`
- Likes, comentarios y reacciones disparan push al propietario del post cuando corresponde.

### Reports

- `POST /api/reports`
- Aprobar un reporte ejecuta la acción: elimina post/comentario o suspende al usuario.

### Training

- `GET /api/training/routines`
- `GET /api/training/routines/:id`
- `POST /api/training/routines`
- `POST /api/training/routines/from-session/:sessionId`
- `PATCH /api/training/routines/:id`
- `POST /api/training/routines/:id/start`
- Al iniciar una rutina, el mobile carga sus ejercicios y objetivos en la sesión.
- `GET /api/training/sessions`

### Leaderboard

- `GET /api/leaderboard/exercises/:exerciseId`
- Los rankings excluyen usuarios suspendidos.
- `GET /api/training/progress`
- `GET /api/training/prs`
  - incluye rango actual, siguiente rango, progreso y kilogramos restantes cuando existen rangos publicados.
- `GET /api/training/sessions/:id`
- `POST /api/training/sessions`
- `PATCH /api/training/sessions/:id`
- `DELETE /api/training/sessions/:id`
- `POST /api/training/sessions/:id/sets`

### Commercial

- `GET /api/commercial/plans`
- `GET /api/subscriptions/me`
- `POST /api/subscriptions/me/start-trial`
- `POST /api/billing/revenuecat/webhook` protegido por `REVENUECAT_WEBHOOK_SECRET`.

### Admin

- `GET /api/admin/summary`

### Health

- `GET /api/health`

## 4. Contrato Tecnico

La API responde con el envelope estandar:

```ts
{ ok: true, data?: T, message?: string, statusCode: number }
```

Eso permite mantener consistencia con mobile y con cualquier consumidor futuro.

## 5. Modelo De Datos Ya Cubierto

Entidades actuales en Prisma:

- `User`
- `Gym`
- `Exercise`
- `Post`
- `PostComment`
- `PostLike`
- `PostReaction`
- `TrainingSession`
- `TrainingSet`
- `GymCheckIn`

## 6. Flujos Ya Cubiertos Por Mobile

- Login y registro.
- Home con summary y feed.
- Busqueda de gimnasios, ejercicios y posts.
- Ranking y notificaciones con estado de visto.
- Perfil editable con avatar y stats.
- Crear sesion, agregar sets y revisar detalle.
- Consultar progreso de los ultimos 30 dias.
- Editar y eliminar sesiones propias.
- Trial y paywall basico.

## 7. Seeds Y Datos Demo

El seed actual deja listo el entorno con:

- usuarios demo admin y user
- publicaciones demo
- comentarios demo
- likes demo
- sesiones de entrenamiento demo

Eso permite validar el flujo completo sin depender de carga manual inicial.

## 8. Swagger Y Validacion

- Swagger esta habilitado en `/api/docs`.
- `ValidationPipe` global activo con `transform` y `whitelist`.
- Los DTOs cubren los flujos de escritura principales.

## 9. Decisiones Tecnicas

- Se priorizo contrato compartido para evitar divergencia con mobile.
- Se mantuvo `ApiEnvelope` como formato unico para todas las respuestas.
- El home agrega tanto feed como entrenos para reducir roundtrips en mobile.
- Las sesiones de entrenamiento viven como dominio propio, no como parte del feed.

## 10. Estado De Calidad

Verificado recientemente:

- typecheck de API
- check de formato
- prisma generate
- prisma push
- prisma seed

## 11. Pendientes Priorizados

1. Evitar el uso de `any` en queries Prisma y tipar el acceso al client generado.
2. Introducir DTOs y validaciones mas especificas en escrituras.
3. Agregar tests de integracion para auth, posts, search, training y commercial.
4. Revisar paginacion y performance del feed si el volumen de datos crece.
5. Tipar mejor los selects complejos de Prisma.

## 12. Riesgos Y Deuda Actual

- El backend ya resuelve bastante del MVP, pero el tipado Prisma aun tiene atajos.
- Falta cobertura automatizada de endpoints.
- La consulta de likes en home/posts se resuelve con conteo adicional por item.
- Si el feed crece, se necesitara paginacion real para no cargar demasiados registros.

## 13. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y `me` funcionan de forma consistente.
- `home/summary` entrega todo lo que mobile necesita.
- Crear posts, comentarios, likes, search y sesiones responde bien.
- Prisma, seed y typecheck permanecen limpios.
