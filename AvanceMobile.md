# OlympX Mobile - Avance Actual

> Estado tecnico y funcional de `olympx-mobile` al dia de hoy.

## 1. Objetivo

Documentar el avance real de la app mobile para tener una foto clara de lo que ya esta entregado, lo que depende de API y lo que falta para un MVP usable.

## 2. Estado General

La app mobile ya esta alineada con el stack Dayca y consume el contrato compartido `dayca-olympx-contracts`.

Hoy cubre:

- Autenticacion con persistencia local.
- Home con resumen de perfil, gimnasios, publicaciones y entrenos recientes.
- Busqueda global.
- Ranking de usuarios.
- Alertas de actividad con persistencia backend de vistas.
- Perfil y edicion de perfil.
- Detalle de gimnasio y detalle de publicacion.
- Historial, creacion y detalle de sesiones de entrenamiento.
- Paywall con RevenueCat.
- Terminos y condiciones dentro de la app.

## 3. Pantallas Implementadas

### Login

- Pantalla de entrada para credenciales.
- Permite login y registro.
- Guarda token y usuario en Zustand + AsyncStorage.

### Home

- Saludo con datos del usuario.
- Seccion para publicar en el feed.
- Seccion para registrar entrenos.
- Listado de gimnasios sugeridos.
- Listado de entrenos recientes.
- Feed de publicaciones.
- Obtiene ubicacion para gimnasios cercanos.

### Search

- Busca gimnasios, ejercicios y publicaciones.

### Leaderboard

- Muestra ranking por score social y entreno.

### Notifications

- Lista actividad reciente sobre publicaciones propias.
- Marca como vistas con sync a backend y fallback local.

### Gym Detail

- Muestra detalle del gimnasio seleccionado.

### Post Detail

- Muestra contenido completo de la publicacion.
- Permite comentar.
- Permite dar like / unlike.
- Refresca estado local al recibir respuesta de la API.

### Training History

- Lista sesiones registradas.
- Entra al detalle de cada sesion.

### Training Session Create

- Crea sesiones con plantillas rapidas.
- Permite seleccionar zonas musculares.

### Training Session Detail

- Muestra resumen, sets, volumen y progreso.
- Permite registrar sets nuevos.
- Incluye ajustes avanzados opcionales de RPE y RIR.

### Profile

- Muestra datos basicos del usuario autenticado.
- Carga estadisticas de usuario y suscripcion.

### Edit Profile

- Edita datos personales y avatar.
- Permite subir imagen desde galeria.

### Paywall

- Lista planes comerciales activos.
- Integra compra con RevenueCat.

### Terms

- Pantalla de terminos y condiciones dentro de la app.

## 4. Integracion Con API

La app consume estos flujos principales:

- `POST /api/auth/login`
- `POST /api/auth/register`
- `GET /api/home/summary`
- `GET /api/posts`
- `POST /api/posts`
- `GET /api/posts/:id`
- `POST /api/posts/:id/comments`
- `POST /api/posts/:id/like`
- `GET /api/gyms`
- `GET /api/gyms/nearby`
- `GET /api/gyms/:id`
- `GET /api/search`
- `GET /api/leaderboard`
- `GET /api/notifications`
- `GET /api/users/me`
- `GET /api/users/me/stats`
- `PATCH /api/users/me`
- `POST /api/users/me/avatar`
- `PATCH /api/users/me/location`
- `GET /api/subscriptions/me`
- `POST /api/subscriptions/me/start-trial`
- `GET /api/commercial/plans`
- `GET /api/training/sessions`
- `POST /api/training/sessions`
- `GET /api/training/sessions/:id`
- `POST /api/training/sessions/:id/sets`

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
- `SubscriptionAccessResponse`
- `CommercialPlanSummary`
- `SearchResponse`
- `LeaderboardResponse`
- `NotificationResponse`
- `UserProfile`
- `UserProfileStats`
- `UpdateProfileRequest`
- `TrainingSessionSummary`
- `TrainingSessionDetail`
- `TrainingSetSummary`
- `CreateTrainingSetRequest`
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

- typecheck de mobile
- check de formato

## 8. Pendientes Priorizados

1. Agregar cache local para reducir llamadas al summary y a listados.
2. Sumar tests basicos de mobile para login, home y training.
3. Separar mejor el composer de publicaciones y el composer de entrenos.
4. Mejorar estados vacios, errores y loading para resiliencia offline.
5. Evaluar analitica de uso mobile.

## 9. Riesgos Y Deuda Actual

- El home concentra demasiadas acciones en una sola pantalla.
- Falta una capa de cache para mejorar experiencia offline o con red inestable.
- No hay analitica de uso mobile aun.
- No hay tests automatizados para mobile.

## 10. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y persistencia funcionan de forma consistente.
- Home carga resumen completo sin errores.
- Crear publicaciones, comentarios, likes y entrenos refresca el contenido visible.
- Detalle de post y gimnasio siguen navegando correctamente.
- Search, leaderboard, perfil y suscripcion responden sin friccion.
