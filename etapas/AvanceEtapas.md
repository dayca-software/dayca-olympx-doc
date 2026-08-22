# OlympX - Avance por Etapas

> Estado real del plan definido en `doc/Estructura por etapas.md`.
> Fuente de verdad para seguimiento con cliente y equipo.

## Resumen Ejecutivo

| Etapa | Nombre | Estado | Cobertura real |
| --- | --- | --- | --- |
| 1 | Discovery, planificación y UX/UI | Parcial | Documentación lista, Figma en curso |
| 2 | Backend, BD y autenticación | Casi completa | API funcional, contratos, seed y registro |
| 3 | Gimnasios, GPS y biblioteca | Parcial alta | Gimnasios + ubicación + ejercicios |
| 4 | Rutinas y registro de entrenamiento | Parcial alta | Sesiones, sets, historial y rutinas implementados; falta validación completa |
| 5 | PRs, progreso y rankings | Parcial media | Progreso, 1RM, rangos y rankings implementados; falta calibración y cobertura |
| 6 | Conquistas, estadísticas y notificaciones | Parcial media | Stats, logros base y push preparado; falta validación física y automatización completa |
| 7 | QA, estabilización y cierre | Parcial | Smoke iOS, typecheck y unit tests; faltan integración, offline físico y release |

## Etapa 1 - Discovery, planificación y UX/UI

### Entregables planificados
- Documento de alcance y especificación funcional
- Arquitectura del sistema definida
- Prototipado navegable de pantallas clave

### Estado actual
- Documentación de producto completa y estructurada en `doc/`.
- Arquitectura base definida para API, web, admin, mobile y contratos.
- Hay pantallas reales en web, admin y mobile, pero el prototipo UX no está consolidado como artefacto único.
- El Figma de Etapa 1 sigue en construcción y es el entregable faltante para cierre formal.

### Balance
- **Estado:** Parcial
- **Observación:** la parte documental está sólida; la UX navegable existe por subproyecto, no como un prototipo maestro.

## Etapa 2 - Backend, Base de Datos y Autenticación

### Entregables planificados
- Servidor NestJS operativo
- Modelo de datos Prisma + PostgreSQL
- API base con health check
- Autenticación JWT
- Envoltorio de respuesta estandarizado

### Estado actual
- NestJS operativo con `health`, Swagger, CORS, Helmet y throttling.
- Prisma activo con seed funcional.
- Auth con login, registro, `me`, admin login y token JWT.
- Envelope `ApiEnvelope<T>` implementado.
- La Etapa 2 ya cubre el core backend de la validacion inicial; faltan solo detalles de cierre y endurecimiento.

### Balance
- **Estado:** Casi completa
- **Observación:** faltan endurecimientos y algunos ajustes de modelo, pero el core ya está entregado.

## Etapa 3 - Gimnasios, GPS y Biblioteca de Ejercicio

### Entregables planificados
- Selección de gimnasio principal
- Check-in por GPS
- Catálogo de ejercicios con metadatos
- API de ejercicios con filtros

### Estado actual
- Catálogo de gimnasios y búsqueda cercana implementados.
- Actualización de ubicación del usuario y geolocalización en mobile.
- Biblioteca de ejercicios con filtros y detalle implementada.

### Pendiente clave
- Check-in formal como entidad/flujo separado.
- Actividad del gym y validación de check-in por distancia.

### Balance
- **Estado:** Parcial alta
- **Observación:** ya hay base funcional para gimnasios, GPS y ejercicios; falta formalizar check-in y actividad local.

## Etapa 4 - Rutinas y Registro de Entrenamiento

### Entregables planificados
- Rutinas personalizadas
- Registro en vivo
- Series, reps, peso, RPE, RIR y notas
- Finalización y guardado de sesiones
- Historial de entrenamientos

### Estado actual
- Se pueden crear sesiones y sets.
- El historial de sesiones ya existe.
- Las rutinas persistentes permiten días, orden de ejercicios, objetivos y sesiones desde plantilla.
- Ya existe la base completa del flujo de registro; falta cerrar validaciones de límites, errores y escenarios offline.

### Balance
- **Estado:** Parcial alta
- **Observación:** la funcionalidad está implementada; el pendiente principal es la evidencia E2E y la validación de casos borde.

## Etapa 5 - PRs, Progreso y Rankings

### Entregables planificados
- Cálculo automático de PRs
- Tonelaje total por sesión y acumulado
- Gráfica de volumen semanal
- Rankings por ejercicio dentro del gimnasio
- Comparación entre usuarios

### Estado actual
- Hay estadísticas básicas de usuario.
- Existe leaderboard general y por ejercicio, progreso, PRs y rangos de fuerza publicados.
- Se calcula `estimated1rmKg` en sets y se muestran rango actual, siguiente rango y distancia restante.
- La capa funcional está implementada; falta validar calibración por sexo, categorías y actualización de posiciones.

### Balance
- **Estado:** Parcial media

## Etapa 6 - Conquistas, Estadísticas y Notificaciones

### Entregables planificados
- Logros automáticos
- Perfil con estadísticas básicas
- Alertas push

### Estado actual
- Perfil con stats básicas ya disponible.
- Notifications existe con vistas persistidas, registro de dispositivos y preparación FCM/APNs.
- Hay logros base y estadísticas visibles, pero falta validar entrega push en dispositivo físico y ampliar automatizaciones.
- La Etapa 6 está funcionalmente avanzada, pero no cerrada para release.

### Balance
- **Estado:** Parcial media

## Etapa 7 - QA, Estabilización y Cierre

### Entregables planificados
- Pruebas funcionales e integración
- Corrección de bugs
- Estabilización productiva
- Coordinación general

### Estado actual
- Hay smoke tests en API, web, admin y Maestro en mobile.
- iOS ya tiene smoke de core, límite Free, acciones de entrenamiento y suscripción.
- Jest mobile tiene 12 tests pasando y typecheck mobile pasa.
- Faltan suites de integración, offline físico, push físico y validaciones de seguridad/rendimiento.

### Balance
- **Estado:** Inicial

## Conclusión

El proyecto ya cubre con solidez las etapas 2 y 3, y tiene implementada una parte importante de las
etapas 4, 5 y 6. Etapa 1 sigue abierta formalmente por el Figma/prototipo navegable. El siguiente
foco es cerrar la validación de entrenamiento y los E2E del MVP social antes de entrar en release.

## Recomendación de Prioridad

1. Cerrar evidencia E2E de rutinas, historial, límites y offline.
2. Ejecutar E2E de comunidad, competencia y suscripciones.
3. Validar push físico, RevenueCat Test Store, seguridad y rendimiento.
4. Mantener multimedia avanzada y retención fuera del corte actual.
