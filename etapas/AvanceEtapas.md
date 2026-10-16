# OlympX - Avance por Etapas

> Estado real del plan definido en `doc/Estructura por etapas.md`.
> Fuente de verdad para seguimiento con cliente y equipo.

## Resumen Ejecutivo

| Etapa | Nombre                                    | Estado        | Cobertura real                                                                                                                     |
| ----- | ----------------------------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 1     | Discovery, planificación y UX/UI          | Parcial       | Documentación lista, Figma en curso                                                                                                |
| 2     | Backend, BD y autenticación               | Casi completa | API funcional, contratos, seed y registro                                                                                          |
| 3     | Gimnasios, GPS y biblioteca               | Casi completa | Gimnasios + GPS + ejercicios + check-in; happy path validado, faltan estados alternos                                              |
| 4     | Rutinas y registro de entrenamiento       | Casi completa | Sesiones, sets, historial y rutinas implementados; falta E2E físico y migración staging                                            |
| 5     | PRs, progreso y rankings                  | Implementación completa | PRs persistidos, progreso semanal y rankings por periodo/gimnasio/categoría; faltan E2E y cierre en staging             |
| 6     | Conquistas, estadísticas y notificaciones | Implementación completa; cierre operativo pendiente | Catálogo de 8 logros automático y trazable, perfil, bandeja in-app y push FCM/APNs preparado; falta validación física |
| 7     | QA, estabilización y cierre               | Parcial       | Smoke iOS, typecheck y unit tests; faltan integración, offline físico y release                                                    |

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
- Auth con login, registro, `me`, admin login, cambio de contraseña y token JWT.
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
- Check-in con radio de 100 metros, cooldown de 30 minutos y actualización de gimnasio principal.
- Actividad local pública, estados de disponibilidad y apertura de mapas implementados.
- API con 40 archivos y 245 tests pasando; mobile con 14 suites y 37 tests pasando.
- Build, instalación y lanzamiento nativo verificados en emulador Android Pixel 10 y simulador iOS iPhone 17 Pro.
- Smoke Maestro de búsqueda, detalle y selección de gimnasio principal pasado en iOS y Android.
- Smoke Maestro de check-in dentro del radio permitido pasado en iOS y Android.

### Pendiente clave

- Validación de estados alternos de check-in en iOS y Android físicos.
- Validación física de permisos GPS, cooldown, gimnasios no disponibles y apertura de mapas.

### Balance

- **Estado:** Casi completa
- **Observación:** gimnasios, GPS, ejercicios, check-in y actividad local están implementados; los smoke de búsqueda, selección y check-in happy path ya pasaron en ambos targets, pero faltan estados alternos y aprobación formal.

### Plan De Cierre

El cierre se ejecutará según [`PlanCierreEtapa3.md`](./PlanCierreEtapa3.md), priorizando reglas de
check-in, experiencia mobile, pruebas iOS/Android y aprobación formal.

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
- Las rutinas persistentes permiten días de la semana, orden de ejercicios, objetivos y sesiones desde plantilla.
- Los sets soportan peso, repeticiones, RPE, RIR y notas.
- La cola offline conserva sesiones, sets y cierre para sincronizar al recuperar conexión; la validación física sigue pendiente.
- La creación offline conserva un ID de cliente estable, actualiza sets localmente y permite llegar al resumen antes de sincronizar.
- El inicio desde rutina permite elegir y persistir un día semanal; el editor envía `dayOfWeek` al guardar.
- El límite de 50 sets está protegido en API y mobile, incluyendo serialización por sesión y mensaje
  de error explícito.
- La API tiene 49 tests de training pasando, con cobertura de plantillas desde sesión, selección de
  día por `dayOfWeek`, aislamiento por usuario y edición completa de rutinas; mobile cubre el editor
  de rutina (día, alta y reordenamiento de ejercicios) y la cola offline.

### Balance

- **Estado:** Implementación completa; cierre operativo pendiente
- **Observación:** el código y las pruebas locales cubren el loop completo; falta ejecutar evidencia E2E offline en dispositivos físicos y aplicar la migración en staging.

## Etapa 5 - PRs, Progreso y Rankings

### Entregables planificados

- Cálculo automático de PRs
- Tonelaje total por sesión y acumulado
- Gráfica de volumen semanal
- Rankings por ejercicio dentro del gimnasio
- Comparación entre usuarios

### Estado actual

- Hay estadísticas básicas de usuario.
- Existe leaderboard general y ranking competitivo por ejercicio con alcance global/gimnasio y periodo.
- Los PRs se persisten al finalizar sesiones, con sesión de origen y backfill de históricos.
- El progreso incluye volumen semanal, comparación contra la semana anterior y reglas competitivas consistentes.
- El ranking competitivo admite categorías por sexo, edad, peso corporal e IMC, usando los datos existentes del perfil.
- Las reglas aprobadas son sexo `male/female/other`, edad `18–20`, bandas consecutivas de 3 años, tramo final `66–69` y `70+`, peso en bandas de 5 kg e IMC por los umbrales documentados.
- Falta validar rendimiento/E2E con datos reales y aplicar la migración en staging.

### Balance

- **Estado:** Implementación completa; cierre operativo pendiente

## Etapa 6 - Conquistas, Estadísticas y Notificaciones

### Entregables planificados

- Logros automáticos
- Perfil con estadísticas básicas
- Alertas push

### Estado actual

- Perfil con stats básicas ya disponible.
- Notifications existe con vistas persistidas, registro de dispositivos y preparación FCM/APNs.
- `AchievementUnlock` persiste desbloqueos con unicidad por usuario y clave, referencias opcionales y backfill del primer PR histórico.
- El cierre de una sesión genera `first-pr` automáticamente cuando se crea el primer PR del usuario.
- El cierre de una sesión persiste también `first-session`, `ten-sessions`, `hundred-sets` y `tonnage-1000`, con sesión de origen y métrica.
- La creación de posts persiste `first-post`/`five-posts` y el check-in persiste `first-checkin`, sin duplicados por usuario.
- El perfil consulta logros y admin puede crear desbloqueos manuales desde el detalle de usuario, con auditoría y push preparado.
- Los desbloqueos nuevos quedan visibles en la bandeja in-app y disparan el intento de push; Firebase permanece opcional sin credenciales.
- Falta validar entrega push en dispositivo físico, migraciones en staging y completar banners/compartición fuera del criterio mínimo.

### Balance

- **Estado:** Implementación completa; cierre operativo pendiente

## Etapa 7 - QA, Estabilización y Cierre

### Entregables planificados

- Pruebas funcionales e integración
- Corrección de bugs
- Estabilización productiva
- Coordinación general

### Estado actual

- Hay smoke tests en API, web, admin y Maestro en mobile.
- iOS ya tiene smoke de core, límite Free, acciones de entrenamiento y suscripción.
- Jest mobile tiene 45 tests pasando en 15 suites y typecheck mobile pasa; API tiene 429 tests pasando en 51 archivos.
- Faltan suites de integración, offline físico, push físico y validaciones de seguridad/rendimiento.

### Balance

- **Estado:** Inicial

## Conclusión

El proyecto ya cubre con solidez la Etapa 2 y tiene la Etapa 3 casi completa: los smoke base de
gimnasios y check-in happy path pasaron en iOS y Android, pero los estados alternos aún requieren evidencia.
Las etapas 4, 5 y 6 tienen implementación funcional completa, con cierre operativo pendiente en E2E,
staging y dispositivos físicos. Etapa 1 sigue abierta formalmente por el Figma/prototipo navegable. El
siguiente foco es completar los smoke físicos del MVP.

## Recomendación de Prioridad

1. Cerrar evidencia E2E de rutinas, historial, límites y offline.
2. Ejecutar E2E de comunidad, competencia y suscripciones.
3. Validar push físico, RevenueCat Test Store, seguridad y rendimiento.
4. Mantener multimedia avanzada y retención fuera del corte actual.
