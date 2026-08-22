# OlympX Mobile - Avance Actual

> Estado tecnico y funcional de `olympx-mobile` al dia de hoy.

## 1. Objetivo

Documentar el avance real de la app mobile para tener una foto clara de lo que ya esta entregado, lo que depende de API y lo que falta para un MVP usable.

## 2. Estado General

La app mobile ya esta alineada con el stack Dayca y consume el contrato compartido `dayca-olympx-contracts`.

Hoy cubre:

- Autenticacion con persistencia local.
- Registro con aceptación persistida de términos y versión legal.
- Home con resumen de perfil, gimnasios, publicaciones y entrenos recientes.
- Busqueda global.
- Ranking de usuarios.
- Ranking con podio, filtros por periodo/alcance y posición personal.
- Alertas de actividad con persistencia backend de vistas.
- Perfil y edicion de perfil.
- Perfiles publicos desde el ranking.
- Seguir y dejar de seguir usuarios.
- Listas de seguidores y seguidos.
- Logros y conquistas calculados desde la actividad.
- Historial de check-ins del usuario.
- Detalle de gimnasio y detalle de publicacion.
- Historial, creacion y detalle de sesiones de entrenamiento.
- Historial con filtros por periodo e intensidad.
- Rutinas persistentes y creación desde sesiones.
- Ranking por ejercicio con mejor 1RM estimado.
- Tab dedicada de Comunidad en la navegación principal.
- Edición de nickname, región, provincia y comuna con catálogos de Chile.
- Cache local y fallback offline para Home e historial.
- Home con pull-to-refresh.
- Reacciones fitness, reportes y check-in de gimnasio.
- Check-in con solicitud de ubicación y validación de proximidad.
- Las cuentas suspendidas no pueden iniciar ni mantener sesión activa.
- Alertas sociales para likes, comentarios, reacciones y nuevos seguidores.
- Filtros de alertas y acción para marcar todo como leído.
- Firebase Messaging configurado para registrar tokens FCM/APNs, refrescarlos en la API y procesar pushes en foreground, background y apertura inicial.
- Android crea el canal nativo `olympx-social` para notificaciones de actividad social.
- iOS tiene Firebase/AppDelegate, capabilities APNs y entitlements por configuracion; CocoaPods ya integra Firebase Messaging y la build de simulador pasa. Las pruebas de entrega APNs en dispositivo físico quedan pendientes en `doc/E2EPushNotifications.md`.
- Edición y eliminación de publicaciones propias.
- Edición, eliminación y reporte de comentarios.
- Bloqueo y desbloqueo de usuarios desde perfiles públicos.
- Onboarding post-registro con datos mínimos, nivel y gimnasio principal.
- Redirección al onboarding antes de acceder al contenido principal.
- Contador de comentarios visible en el feed.
- Reordenamiento de ejercicios dentro de rutinas.
- Gráfico semanal de volumen y mejores marcas por ejercicio.
- Historial de récords personales por ejercicio.
- Historial de récords con rango actual y distancia al siguiente rango.
- Componente reutilizable de progreso de rango con barra visual, siguiente nivel y kilos restantes.
- Feed filtrable entre todo el contenido y usuarios seguidos.
- Actividades, alertas, check-ins y sesiones ordenadas de más reciente a más antigua también al paginar o usar datos cacheados.
- Cola offline conservadora para escrituras repetibles de ubicación, con coalescencia y reintento al recargar Home.
- Claves de idempotencia para publicar posts y crear sesiones sin duplicados al reintentar.
- Actividad reciente del gimnasio.
- Paywall con RevenueCat.
- Terminos y condiciones dentro de la app.
- Reintento explícito en errores de búsqueda, alertas e historial de entrenamiento.
- Estados vacíos de entrenamiento con CTA para registrar la primera sesión.

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
- Permite alternar feed general y feed de seguidos.

### Search

- Busca gimnasios, ejercicios y publicaciones.

### Leaderboard

- Muestra ranking por score social y entreno.
- Permite abrir el perfil publico de cada usuario.
- Permite seguir o dejar de seguir desde el perfil.

### Notifications

- Lista actividad reciente sobre publicaciones propias.
- Marca como vistas con sync a backend y fallback local.

### Gym Detail

- Muestra detalle del gimnasio seleccionado.
- Permite elegir gimnasio principal y registrar check-in.
- Muestra check-ins y publicaciones recientes del gimnasio.

### Post Detail

- Muestra contenido completo de la publicacion.
- Permite comentar.
- Permite dar like / unlike.
- Permite reacciones fitness y reportar la publicacion.
- Refresca estado local al recibir respuesta de la API.

### Training History

- Lista sesiones registradas.
- Entra al detalle de cada sesion.
- Filtra por periodo e intensidad.
- Muestra progreso, volumen, reps y 1RM estimado.
- Conserva el ultimo historial valido sin red.
- Permite acceder a la biblioteca de rutinas.

### Training Session Create

- Crea sesiones con plantillas rapidas.
- Permite seleccionar zonas musculares.

### Training Session Detail

- Muestra resumen, sets, volumen y progreso.
- Permite registrar sets nuevos.
- Permite editar y eliminar la sesion propia.
- Incluye ajustes avanzados opcionales de RPE y RIR.
- Permite compartir el resumen como publicación.
- Permite guardar la sesión como rutina.

### Routines

- Lista rutinas guardadas.
- Crea rutinas base.
- Edita el nombre, descripción, días, ejercicios, sets objetivo y reps objetivo.
- Inicia una sesión desde una rutina.

### Exercise Leaderboard

- Muestra los mejores sets competitivos por ejercicio.
- Se abre desde el detalle de una sesión.

### Community

- Feed social dedicado con filtros Todos/Siguiendo.
- Publicación de posts, likes y paginación.
- Accesos rápidos a búsqueda de atletas y ranking general.
- Interfaz visual tipo red social con historias de seguidos, composer compacto y tarjetas de actividad.

### Profile

- Muestra datos basicos del usuario autenticado.
- Carga estadisticas de usuario y suscripcion.
- Muestra logros, conquistas y check-ins recientes.

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
- `POST /api/posts/:id/reactions`
- `POST /api/reports`
- `GET /api/gyms`
- `GET /api/gyms/nearby`
- `GET /api/gyms/:id`
- `POST /api/gyms/:id/check-in`
- `GET /api/search`
- `GET /api/leaderboard`
- `GET /api/notifications`
- `GET /api/users/me`
- `GET /api/users/me/stats`
- `GET /api/users/:id`
- `PATCH /api/users/me`
- `PATCH /api/users/me/gym`
- `POST /api/users/me/avatar`
- `PATCH /api/users/me/location`
- `GET /api/subscriptions/me`
- `POST /api/subscriptions/me/start-trial`
- `GET /api/commercial/plans`
- `GET /api/training/sessions`
- `POST /api/training/sessions`
- `GET /api/training/sessions/:id`
- `POST /api/training/sessions/:id/sets`
- `GET /api/training/prs` devuelve rango actual y siguiente rango por ejercicio.

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
- Home e historial guardan el ultimo estado valido para tolerar fallos de red.
- Home agrupa el contenido operativo para reducir navegacion y acelerar validacion de MVP.

## 7. Estado De Calidad

Verificado recientemente:

- typecheck de mobile
- check de formato
- test unitario de progreso de rango
- tests unitarios de ordenamiento de actividad reciente
- tests unitarios de validacion del formulario de autenticacion
- smoke flow Maestro para Login -> Home -> publicar -> Training -> guardar usando `testID` estables
- smoke iOS de entrenamiento: sets, edición, compartir y guardar rutina
- smoke iOS de comunidad: publicar contenido y validar actividad
- smoke iOS de competencia: posición personal y filtros de ranking
- smoke iOS de suscripción: Paywall Free y activación Trial
- cola offline con flush al iniciar y al volver a foreground
- `testID` para estado de ubicación, límites comerciales, acciones Core, tabs, comunidad y competencia.

## 8. Pendientes Priorizados

1. Ejecutar los smoke sociales y de competencia también en Android con credenciales de prueba.
2. Separar mejor el composer de publicaciones y el composer de entrenos.
3. Validar en dispositivo la sincronizacion offline de ubicación, publicaciones y entrenos.
4. Evaluar analitica de uso mobile.

## 9. Riesgos Y Deuda Actual

- El home concentra demasiadas acciones en una sola pantalla.
- No hay analitica de uso mobile aun.
- El smoke E2E requiere Maestro, un dispositivo/emulador y credenciales de prueba; no se ejecuta en Jest.
- El entorno actual tiene Maestro instalado, emulador Android y simulador iOS disponibles.
- Smoke Maestro Core, límite Free, entrenamiento, comunidad, competencia y suscripción ejecutados correctamente en iOS.
- La validación Android de los nuevos smoke sociales y de competencia sigue pendiente.
- La cola offline requiere validación en dispositivo; el flush global se ejecuta al iniciar y al volver a foreground.

## 10. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y persistencia funcionan de forma consistente.
- Home carga resumen completo sin errores.
- Crear publicaciones, comentarios, likes y entrenos refresca el contenido visible.
- Detalle de post y gimnasio siguen navegando correctamente.
- Search, leaderboard, perfil y suscripcion responden sin friccion.
