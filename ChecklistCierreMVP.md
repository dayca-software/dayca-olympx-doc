# OlympX MVP 2026 - Checklist De Cierre

> Lista ejecutable para cerrar el MVP con foco en mobile, API y validacion final.

## 1. Base Funcional

- [ ] Login y registro funcionando en mobile.
- [ ] Persistencia de sesion confirmada tras reinicio.
- [ ] Home carga summary, feed y entrenos recientes.
- [ ] Search devuelve gimnasios, ejercicios y posts.
- [ ] Leaderboard responde sin errores.
- [ ] Perfil y edicion de perfil guardan cambios.

## 2. Entrenamiento

- [ ] Crear sesion de entrenamiento.
- [ ] Abrir detalle de sesion.
- [ ] Agregar sets con peso y repeticiones.
- [ ] Ver volumen, progreso y sets recientes.
- [ ] Ver historial de sesiones.

## 3. Social

- [ ] Crear publicaciones desde home.
- [ ] Abrir detalle de publicacion.
- [ ] Comentar publicaciones.
- [ ] Dar like y unlike.
- [ ] Notificaciones con estado de visto persistido.

## 4. Monetizacion

- [ ] Ver planes comerciales activos.
- [ ] Cargar paywall sin bloquear el core.
- [ ] Activar trial desde home.
- [ ] Confirmar acceso a premium con RevenueCat.

## 5. Calidad

- [ ] Agregar smoke tests para auth, home y training.
- [ ] Cubrir al menos un test de notifications.
- [ ] Verificar typecheck de API.
- [ ] Verificar typecheck de mobile.
- [ ] Verificar format check general.

## 6. Definition Of Done

El MVP se puede dar por cerrado cuando:

- Login, home, social y training funcionan end to end.
- Notifications quedan sincronizadas entre backend y mobile.
- No hay bloqueos de pago sobre el flujo core.
- Hay al menos un set minimo de tests para los caminos criticos.
