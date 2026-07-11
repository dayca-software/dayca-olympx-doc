# OlympX Mobile - Avance Actual

> Estado tecnico y funcional de `olympx-mobile` al dia de hoy.

## 1. Objetivo

Documentar el avance real de la app mobile para tener una foto clara de lo que ya esta entregado, lo que depende de API y lo que falta para un MVP usable.

## 2. Estado General

La app mobile ya esta alineada con el stack Dayca y consume el contrato compartido `dayca-olympx-contracts`.

Hoy cubre:

- Autenticacion con persistencia local.
- Home con resumen de perfil, gimnasios, publicaciones y entrenos recientes.
- Detalle de gimnasio.
- Feed social con detalle de publicacion, likes y comentarios.
- Registro de publicaciones desde el home.
- Registro de entrenamientos desde el home.

## 3. Pantallas Implementadas

### Login

- Pantalla de entrada para credenciales.
- Guarda token y usuario en Zustand + AsyncStorage.

### Home

- Saludo con datos del usuario.
- Seccion para publicar en el feed.
- Seccion para registrar entrenos.
- Listado de gimnasios sugeridos.
- Listado de entrenos recientes.
- Feed de publicaciones.

### Gym Detail

- Muestra detalle del gimnasio seleccionado.

### Post Detail

- Muestra contenido completo de la publicacion.
- Permite comentar.
- Permite dar like / unlike.
- Refresca estado local al recibir respuesta de la API.

### Profile

- Muestra datos basicos del usuario autenticado.

## 4. Integracion Con API

La app consume estos flujos principales:

- `POST /api/auth/login`
- `GET /api/home/summary`
- `GET /api/posts`
- `POST /api/posts`
- `GET /api/posts/:id`
- `POST /api/posts/:id/comments`
- `POST /api/posts/:id/like`
- `GET /api/gyms`
- `GET /api/gyms/:id`
- `GET /api/training/sessions`
- `POST /api/training/sessions`

La base de la integracion usa `axios` con interceptor de `Authorization` y `ApiEnvelope<T>` como contrato de respuesta.

## 5. Contratos Compartidos Usados

- `AuthUser`
- `LoginResponse`
- `ApiEnvelope`
- `GymSummary`
- `GymDetail`
- `PostSummary`
- `PostDetail`
- `CommentSummary`
- `HomeSummary`
- `TrainingSessionSummary`
- `CreatePostRequest`
- `CreateTrainingSessionRequest`

## 6. Decisiones Tecnicas

- Se priorizo mobile-first sobre web para validar el core del producto.
- Se reutiliza el paquete privado de contratos para evitar drift entre API y mobile.
- El estado de auth se centraliza en Zustand.
- La persistencia local usa AsyncStorage para mantener sesion entre aperturas.
- Home agrupa el contenido operativo para reducir navegacion y acelerar validacion de MVP.

## 7. Estado De Calidad

Verificado recientemente:

- `pnpm --filter olympx-mobile typecheck`
- `pnpm run format:check`

## 8. Pendientes Priorizados

1. Crear vistas dedicadas para historial de entrenos.
2. Agregar edicion / borrado de entrenos si el producto lo necesita.
3. Separar mejor el composer de publicaciones y el composer de entrenos.
4. Introducir manejo de estados vacios mas visual.
5. Evaluar cache local para reducir llamadas al summary.

## 9. Riesgos Y Deuda Actual

- El home concentra demasiadas acciones en una sola pantalla.
- Falta una capa de cache para mejorar experiencia offline o con red inestable.
- No hay analitica de uso mobile aun.
- El flujo de entrenos todavia es simple y requiere evolucion si se convierte en feature central.

## 10. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y persistencia funcionan de forma consistente.
- Home carga resumen completo sin errores.
- Crear publicaciones y entrenos refresca el contenido visible.
- Detalle de post y gimnasio siguen navegando correctamente.
