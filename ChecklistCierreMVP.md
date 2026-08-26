# OlympX MVP 2026 - Checklist De Cierre

> Lista ejecutable para cerrar el MVP con foco en mobile, API y validacion final.

> Convencion: `[x]` significa implementado y validado por typecheck/tests o build. Los flujos E2E fisicos se mantienen pendientes hasta ejecutarlos manualmente.

> Nota de alcance: `AnexoMVP.md` define un MVP Core centrado en entrenamiento, mientras que la implementacion actual tambien incluye funciones sociales. La decision entre MVP Core y MVP ampliado debe quedar cerrada antes del lanzamiento.

## 0. Alcance Y Cuenta

- [x] El lanzamiento corresponde al MVP ampliado con red social; el entrenamiento sigue siendo el flujo core.
- [ ] Confirmar si Google OAuth y Apple OAuth forman parte del lanzamiento.
- [ ] Implementar verificacion de email, si se exige para el lanzamiento.
- [ ] Implementar recuperacion y cambio de contraseña.
- [ ] Implementar eliminacion de cuenta y datos personales.
- [ ] Validar consentimiento legal, version de terminos y regla para usuarios menores de edad.
- [ ] Validar refresh token y comportamiento de sesiones expiradas.

### Decision De Alcance

El MVP de lanzamiento incluye entrenamiento, progreso, comunidad social, perfiles publicos,
publicaciones, comentarios, likes, reacciones, follows, alertas y rankings. Multimedia avanzada,
stories, coach y funcionalidades de retencion avanzada quedan fuera de este corte salvo decision
posterior.

## 1. Base Funcional

- [x] Login y registro funcionando en mobile.
- [x] Persistencia de sesion implementada tras reinicio.
- [x] Home carga summary, feed y entrenos recientes.
- [x] Search devuelve gimnasios, ejercicios y posts.
- [x] Leaderboard responde sin errores.
- [x] Perfil y edicion de perfil guardan cambios.
- [x] Subir y visualizar imagen de avatar desde mobile.
- [x] Las cuentas `admin` quedan fuera de rankings, feed, perfiles y relaciones públicas.
- [x] Onboarding post-registro obliga a completar perfil mínimo y gimnasio.

## 2. Entrenamiento

- [x] Crear sesion de entrenamiento.
- [x] Abrir detalle de sesion.
- [x] Agregar sets con peso y repeticiones.
- [x] Ver volumen, progreso y sets recientes.
- [x] Ver historial de sesiones.
- [ ] Validar rutinas por dias, orden de ejercicios, plantillas reutilizables y edicion completa.
- [ ] Validar captura de RPE, RIR, notas y escala pre-sesion cuando corresponda al alcance.
- [ ] Validar limites de sets, unidades, pesos y repeticiones con mensajes de error claros.
- [x] Resolver cola offline conservadora para ubicación y escrituras repetibles.
- [x] Añadir idempotencia API antes de reintentar publicaciones o creación de entrenos offline.

## 2.1 Progreso Y Competencia

- [x] Validar formulas de PR, 1RM estimado y tonelaje con casos borde en API.
- [x] Mostrar rango actual y kilogramos faltantes para el siguiente rango desde el historial de PRs.
- [ ] Validar rankings por gimnasio, ejercicio y categorias demograficas incluidas en el alcance.
- [ ] Validar frecuencia de actualizacion de rankings y consistencia de posiciones.
- [ ] Calibrar rangos por sexo con una fuente de datos aprobada.
- [ ] Implementar percentil y tarjeta compartible/PDF, o dejarlos explicitamente para Fase 2.

## 2.2 Gimnasios Y GPS

- [x] Validar radio de check-in de 100 metros en backend.
- [ ] Validar expiracion del check-in y bloqueo de duplicados.
- [ ] Validar busqueda manual, seleccion desde resultados y apertura en mapas.
- [ ] Confirmar si actividad local, usuarios cercanos y heatmaps entran en el lanzamiento.

## 3. Social

- [x] Crear publicaciones desde home.
- [x] Compartir progreso semanal desde Home como publicación social con un toque.
- [x] Compartir logros desbloqueados desde Perfil como publicación social.
- [ ] Definir si las publicaciones del MVP admiten imagen adjunta; actualmente solo soportan texto.
- [ ] Definir si el MVP incluye estados/stories temporales; no hay flujo implementado actualmente.
- [x] Abrir detalle de publicacion.
- [x] Comentar publicaciones.
- [x] Dar like y unlike.
- [x] Reacción rápida de fuego directamente desde el feed.
- [x] Notificaciones con estado de visto persistido.
- [ ] Validar compartir publicaciones, logros y banners fuera de la app.
- [ ] Implementar o excluir del lanzamiento publicaciones automaticas por PR/conquista.

## 3.1 Multimedia Y Estados

- [ ] Implementar subida de imagen adjunta en publicaciones, si entra en el MVP ampliado.
- [ ] Implementar estados/stories con expiracion de 24 horas, si entran en el MVP ampliado.
- [ ] Implementar subida de video desde galeria con limite de 60 segundos y 50 MB, si entra en el alcance.
- [ ] Implementar compresion y eliminacion automatica de multimedia expirada, si entra en el alcance.
- [ ] Validar MIME, tamaño, extension y almacenamiento seguro de archivos subidos.

## 4. Monetizacion

- [x] Ver planes comerciales activos.
- [x] Cargar paywall sin bloquear el core.
- [x] Activar trial desde home.
- [ ] Confirmar acceso a premium con RevenueCat.
- [x] Configurar Firebase Messaging y sincronización de tokens FCM/APNs.
- [x] Definir periodo rolling de 30 días para límites comerciales.
- [ ] Implementar eventos de uso para exportaciones y compartición cuando existan esos flujos.
- [x] Incluir flujo de restauracion de compras en el paywall.
- [ ] Validar restauracion y sincronizacion de entitlements con RevenueCat Test Store.
- [ ] Validar cancelacion, expiracion, renovacion y perdida de acceso premium.
- [ ] Confirmar limites Free, Trial y Paid en API, mobile y panel admin.

## 5. Calidad

- [x] Agregar smoke tests para onboarding y training con límite comercial.
- [x] Agregar smoke test de Home autenticado y rechazo de sesión inválida.
- [x] Cubrir al menos un test de notifications.
- [x] Verificar typecheck de API.
- [x] Verificar typecheck de mobile.
- [ ] Verificar format check general.
- [x] Check-in valida GPS, gimnasio disponible y duplicados recientes.
- [x] Búsqueda, alertas e historial ofrecen reintento o acción útil en estados vacíos/error.
- [x] Ejecutar `.maestro/core-smoke.yaml` en iOS y `.maestro/core-android-smoke.yaml` en Android con usuario Trial y API local.
- [x] Ejecutar `.maestro/free-limit-smoke.yaml` con usuario Free y comprobar bloqueo de creación.
- [x] Agregar tests mobile automatizados para login, home, training, comunidad, competencia y navegacion critica.
- [ ] Agregar tests de integracion para auth, posts, training, notifications y suscripciones.
- [ ] Validar rendimiento de endpoints criticos bajo conexion 4G.
- [ ] Validar rate limiting, HTTPS, backups, logs y monitoreo de produccion.

## 6. Web Y Admin

- [ ] Construir dashboard web con contenido real de producto o dejarlo fuera del lanzamiento.
- [ ] Construir dashboard admin operativo con KPIs basicos.
- [ ] Implementar gestion admin de usuarios, suspensiones y reactivaciones.
- [ ] Implementar moderacion de reportes y contenido con auditoria.
- [ ] Implementar gestion admin de gimnasios y catalogo de ejercicios.
- [ ] Implementar gestion admin de planes, trials, cupones y limites Free.
- [ ] Agregar tests de auth, roles y rutas protegidas de web/admin.
- [x] Admin puede crear, editar, publicar y eliminar borradores de rangos de fuerza.
- [ ] Admin puede consultar auditoria por entidad, actor y fecha.
- [x] La cuenta `admin` queda excluida de las superficies publicas de la app.

## 7. Validacion Final

- [ ] Ejecutar E2E manual de login -> home -> post -> training.
- [ ] Ejecutar E2E manual de push Android en foreground, background y app terminada.
- [ ] Ejecutar E2E manual de push iOS en dispositivo físico y TestFlight.
- [ ] Confirmar `PushDevice` y navegación desde like, comentario, reacción y follow.
- [ ] Configurar una clave publica RevenueCat valida para Android Test Store y confirmar compra premium.
- [ ] Ejecutar `format:check` general y corregir cualquier diferencia.
- [ ] Agregar al menos una prueba de integración para posts/training/notifications.

## 8. Fase 2 O Fuera Del Core

- [ ] Eventos de uso para exportaciones y compartición cuando existan esos endpoints.
- [ ] Automatización E2E desde el repo raíz.
- [ ] Suite de tests mobile de pantallas y navegación.
- [ ] Coach, nudges, metas semanales y streaks.
- [ ] Rivalidades, Top del Dia y titulos.
- [ ] Activity summaries automaticos.
- [ ] Heatmaps y actividad local avanzada.

## 9. Definition Of Done

El MVP se puede dar por cerrado cuando:

- El alcance funcional seleccionado en la seccion 0 funciona end to end.
- Si la red social forma parte del lanzamiento, login, home, social y training funcionan end to end.
- Notifications quedan sincronizadas entre backend y mobile.
- No hay bloqueos de pago sobre el flujo core.
- Hay al menos un set minimo de tests para los caminos criticos.
