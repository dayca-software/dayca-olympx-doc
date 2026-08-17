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
- Rutinas persistentes y sesiones iniciadas desde plantilla.
- Ranking competitivo por ejercicio basado en mejor 1RM estimado.
- Perfil editable con nickname, región, provincia y comuna persistidos.
- Edicion y eliminacion segura de sesiones propias.
- Suscripcion, trial y catalogo comercial.
- Resumen de administracion.
- Health check y Swagger.

## 3. Modulos Implementados

### Auth

- `POST /api/auth/login`
- `POST /api/auth/register`
- `GET /api/auth/me`
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
- `GET /api/gyms/:id/activity`

### Search

- `GET /api/search`

### Leaderboard

- `GET /api/leaderboard`

### Notifications

- `GET /api/notifications`
- `POST /api/notifications/viewed`

### Posts

- `GET /api/posts`
  - soporta `scope=all|following`
- `POST /api/posts`
- `GET /api/posts/:id`
- `POST /api/posts/:id/comments`
- `POST /api/posts/:id/like`
- `POST /api/posts/:id/reactions`

### Reports

- `POST /api/reports`

### Training

- `GET /api/training/routines`
- `GET /api/training/routines/:id`
- `POST /api/training/routines`
- `POST /api/training/routines/from-session/:sessionId`
- `PATCH /api/training/routines/:id`
- `POST /api/training/routines/:id/start`
- `GET /api/training/sessions`

### Leaderboard

- `GET /api/leaderboard/exercises/:exerciseId`
- `GET /api/training/progress`
- `GET /api/training/sessions/:id`
- `POST /api/training/sessions`
- `PATCH /api/training/sessions/:id`
- `DELETE /api/training/sessions/:id`
- `POST /api/training/sessions/:id/sets`

### Commercial

- `GET /api/commercial/plans`
- `GET /api/subscriptions/me`
- `POST /api/subscriptions/me/start-trial`

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
