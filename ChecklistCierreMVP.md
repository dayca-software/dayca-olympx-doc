# OlympX MVP 2026 - Checklist De Cierre

> Lista ejecutable para cerrar el MVP con foco en mobile, API y validacion final.

> Convencion: `[x]` significa implementado y validado por typecheck/tests o build. Los flujos E2E fisicos se mantienen pendientes hasta ejecutarlos manualmente.

## 1. Base Funcional

- [x] Login y registro funcionando en mobile.
- [x] Persistencia de sesion implementada tras reinicio.
- [x] Home carga summary, feed y entrenos recientes.
- [x] Search devuelve gimnasios, ejercicios y posts.
- [x] Leaderboard responde sin errores.
- [x] Perfil y edicion de perfil guardan cambios.
- [x] Subir y visualizar imagen de avatar desde mobile.
- [x] Onboarding post-registro obliga a completar perfil mínimo y gimnasio.

## 2. Entrenamiento

- [x] Crear sesion de entrenamiento.
- [x] Abrir detalle de sesion.
- [x] Agregar sets con peso y repeticiones.
- [x] Ver volumen, progreso y sets recientes.
- [x] Ver historial de sesiones.

## 3. Social

- [x] Crear publicaciones desde home.
- [ ] Definir si las publicaciones del MVP admiten imagen adjunta; actualmente solo soportan texto.
- [ ] Definir si el MVP incluye estados/stories temporales; no hay flujo implementado actualmente.
- [x] Abrir detalle de publicacion.
- [x] Comentar publicaciones.
- [x] Dar like y unlike.
- [x] Notificaciones con estado de visto persistido.

## 4. Monetizacion

- [x] Ver planes comerciales activos.
- [x] Cargar paywall sin bloquear el core.
- [x] Activar trial desde home.
- [ ] Confirmar acceso a premium con RevenueCat.
- [x] Configurar Firebase Messaging y sincronización de tokens FCM/APNs.
- [x] Definir periodo rolling de 30 días para límites comerciales.
- [ ] Implementar eventos de uso para exportaciones y compartición cuando existan esos flujos.

## 5. Calidad

- [x] Agregar smoke tests para onboarding y training con límite comercial.
- [x] Agregar smoke test de Home autenticado y rechazo de sesión inválida.
- [x] Cubrir al menos un test de notifications.
- [x] Verificar typecheck de API.
- [x] Verificar typecheck de mobile.
- [ ] Verificar format check general.
- [x] Check-in valida GPS, gimnasio disponible y duplicados recientes.
- [x] Búsqueda, alertas e historial ofrecen reintento o acción útil en estados vacíos/error.

## 7. Pendientes Reales Para Core

- [ ] Ejecutar E2E manual de login -> home -> post -> training.
- [ ] Ejecutar E2E manual de push Android en foreground, background y app terminada.
- [ ] Ejecutar E2E manual de push iOS en dispositivo físico y TestFlight.
- [ ] Confirmar `PushDevice` y navegación desde like, comentario, reacción y follow.
- [ ] Configurar una clave publica RevenueCat valida para Android Test Store y confirmar compra premium.
- [ ] Ejecutar `format:check` general y corregir cualquier diferencia.
- [ ] Agregar al menos una prueba de integración para posts/training/notifications.

## 8. Fuera Del Core Actual

- [ ] Eventos de uso para exportaciones y compartición cuando existan esos endpoints.
- [ ] Automatización E2E desde el repo raíz.
- [ ] Suite de tests mobile de pantallas y navegación.

## 9. Definition Of Done

El MVP se puede dar por cerrado cuando:

- Login, home, social y training funcionan end to end.
- Notifications quedan sincronizadas entre backend y mobile.
- No hay bloqueos de pago sobre el flujo core.
- Hay al menos un set minimo de tests para los caminos criticos.
