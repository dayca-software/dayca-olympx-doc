# OlympX - Avance Global

> Foto ejecutiva del estado actual de API + mobile.

## 1. Objetivo

Tener una vista unica del avance real del producto, sin entrar en el detalle de implementacion de cada subproyecto.

## 2. Estado General

OlympX ya tiene una base funcional integrada entre backend y mobile.

El alcance elegido para el lanzamiento es el **MVP ampliado con red social**: entrenamiento y
progreso como core, más comunidad social, perfiles públicos, alertas y rankings. Multimedia
avanzada, stories, coach y retención avanzada quedan fuera de este corte.

Hoy el producto soporta:

- Login, registro y persistencia de sesion.
- Home unificado con perfil, gimnasios, feed y entrenos recientes.
- Busqueda, ranking y alertas con vistas persistidas.
- Perfiles publicos, reacciones fitness y reportes.
- Seguimiento social entre usuarios.
- Feed personalizado y actividad reciente de gimnasios.
- Listas sociales, logros y check-ins personales.
- Rutinas persistentes y sesiones desde plantilla.
- Onboarding obligatorio post-registro y límites comerciales rolling de 30 días.
- Editor mobile de días y ejercicios de rutina.
- Tab mobile dedicada para la comunidad y descubrimiento social.
- Ubicación de perfil ampliada con provincia persistente.
- Ranking competitivo por ejercicio y mejor 1RM estimado.
- Ranking general con filtros temporales, alcance por gimnasio y posición personal.
- Registro legal, bloqueo de cuentas suspendidas y check-in con proximidad validada.
- Webhook de RevenueCat protegido por secreto de integración.
- Moderación ejecuta acciones reales sobre contenido y cuentas sancionadas.
- Creacion de publicaciones.
- Creacion y seguimiento de entrenamientos.
- Historial con filtros y cache offline basica.
- Progreso de entrenamiento y mantenimiento de sesiones.
- Comentarios y likes en publicaciones.
- Alertas sociales y gestión de publicaciones propias.
- Rutinas con orden editable, objetivos y métricas visuales de progreso.
- Moderación social con bloqueo, edición, eliminación y reportes de comentarios.
- Alertas filtrables con estado persistente de lectura.
- Infraestructura preparada para tokens push FCM/APNs.
- Historial de récords personales por ejercicio.
- Rangos de fuerza configurados visibles desde el historial de PRs.
- Detalle de gimnasio, detalle de publicacion y detalle de sesion.
- Perfil editable y paywall basico.
- Gimnasio principal y check-in.

## 3. Cobertura Real

### Backend

La API cubre el core operativo del MVP:

- autenticacion
- home summary
- gimnasios
- search
- leaderboard
- notifications
- publicaciones
- comentarios
- likes
- perfil y stats
- sesiones de entrenamiento
- suscripciones y plans
- admin summary
- health check

### Mobile

La app mobile ya permite validar el producto en un flujo completo:

- entrar con credenciales
- registrar cuenta
- ver el estado del usuario
- revisar gimnasios sugeridos
- buscar contenido
- ver ranking
- revisar alertas y marcarlas como vistas
- abrir perfiles publicos desde el ranking
- publicar en el feed
- registrar entrenos
- revisar entrenos recientes
- revisar progreso, volumen y 1RM estimado
- editar o eliminar sesiones propias
- reaccionar y reportar publicaciones
- elegir gimnasio principal y hacer check-in
- abrir detalle de posts y gimnasios
- editar perfil
- revisar suscripcion y trial

## 4. Contrato y Datos

- Se usa `dayca-olympx-contracts` como fuente compartida de tipos.
- La API responde con `ApiEnvelope<T>`.
- Prisma ya incluye `User`, `Gym`, `Exercise`, `Post`, `PostComment`, `PostLike` y `TrainingSession`.
- El seed ya deja datos demo para probar el flujo completo.

## 5. Verificacion Reciente

Validaciones ejecutadas recientemente:

- typecheck de API
- typecheck de mobile
- check de formato
- prisma generate
- prisma push
- prisma seed
- Maestro iOS: core, límite Free, acciones de entrenamiento y suscripción
- Jest mobile: 12 tests pasando

## 6. Riesgos Actuales

- El home concentra demasiadas acciones.
- Todavia no hay tests de integracion cubriendo el flujo social completo.
- El acceso Prisma sigue teniendo algunos atajos con `any`.
- La cola offline actual cubre escrituras repetibles de ubicación; publicaciones y entrenos aún requieren validación física de reintento.
## 7. Proxima Prioridad

1. Completar E2E de comunidad, competencia y suscripciones.
2. Validar push iOS en dispositivo físico y TestFlight.
3. Configurar y confirmar RevenueCat Test Store en Android/iOS, incluyendo restauración de compras.
4. Agregar tests de integración para posts, training, notifications y suscripciones.
5. Ejecutar `format:check` y cerrar diferencias antes del MVP social.
6. Mantener multimedia avanzada, coach y retención avanzada fuera del core de este lanzamiento.

## 8. Documentos Detallados

- `doc/AvanceAPI.md`
- `doc/AvanceMobile.md`
