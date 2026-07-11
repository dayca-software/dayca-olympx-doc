# OlympX API - Avance Actual

> Estado tecnico y funcional de `olympx-api` al dia de hoy.

## 1. Objetivo

Documentar el avance real del backend para dejar claro que endpoints ya estan disponibles, que contratos soporta y que partes del MVP ya quedan cubiertas por la API.

## 2. Estado General

La API ya esta alineada con NestJS + Prisma + PostgreSQL y expone el contrato unificado basado en `ApiEnvelope<T>`.

Hoy cubre:

- Autenticacion con login y consulta de usuario actual.
- Resumen para home mobile.
- Catalogo y detalle de gimnasios.
- Feed social con publicaciones, comentarios y likes.
- Resumen de administracion.
- Registro y consulta de sesiones de entrenamiento.
- Health check y Swagger.

## 3. Modulos Implementados

### Auth

- `POST /api/auth/login`
- `GET /api/auth/me`
- Soporta token bearer y flujo de sesion para mobile.

### Users

- `GET /api/users/me`

### Home

- `GET /api/home/summary`
- Entrega usuario, gimnasios sugeridos, publicaciones recientes y sesiones recientes.

### Gyms

- `GET /api/gyms`
- `GET /api/gyms/:id`

### Posts

- `GET /api/posts`
- `POST /api/posts`
- `GET /api/posts/:id`
- `POST /api/posts/:id/comments`
- `POST /api/posts/:id/like`

### Training

- `GET /api/training/sessions`
- `POST /api/training/sessions`

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
- `TrainingSession`

## 6. Seeds Y Datos Demo

El seed actual deja listo el entorno con:

- usuarios demo admin y user
- publicaciones demo
- comentarios demo
- likes demo
- sesiones de entrenamiento demo

Eso permite validar el flujo completo sin depender de carga manual inicial.

## 7. Swagger Y Validacion

- Swagger esta habilitado en `/api/docs`.
- `ValidationPipe` global activo con `transform` y `whitelist`.
- Los DTOs cubren los flujos de escritura principales.

## 8. Decisiones Tecnicas

- Se priorizo contrato compartido para evitar divergencia con mobile.
- Se mantuvo `ApiEnvelope` como formato unico para todas las respuestas.
- El home agrega tanto feed como entrenos para reducir roundtrips en mobile.
- Las sesiones de entrenamiento viven como dominio propio, no como parte del feed.

## 9. Estado De Calidad

Verificado recientemente:

- `pnpm --filter olympx-api typecheck`
- `pnpm run format:check`
- `pnpm --filter olympx-api run prisma:generate`
- `pnpm --filter olympx-api run prisma:push`
- `pnpm --filter olympx-api run prisma:seed`

## 10. Pendientes Priorizados

1. Evitar el uso de `any` en queries Prisma y tipar el acceso al client generado.
2. Introducir DTOs y validaciones mas especificas en escrituras.
3. Separar mejor el dominio social del dominio entrenamiento si el producto crece.
4. Agregar tests de integracion para auth, posts y training.
5. Revisar paginacion si el volumen de datos crece.

## 11. Riesgos Y Deuda Actual

- El backend ya resuelve bastante del MVP, pero el tipado Prisma aun tiene atajos.
- Falta cobertura automatizada de endpoints.
- La consulta de likes en home/posts se resuelve con conteo adicional por item.
- Si el feed crece, se necesitara paginacion real para no cargar demasiados registros.

## 12. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y `me` funcionan de forma consistente.
- `home/summary` entrega todo lo que mobile necesita.
- Crear posts, comentarios, likes y sesiones responde bien.
- Prisma, seed y typecheck permanecen limpios.
