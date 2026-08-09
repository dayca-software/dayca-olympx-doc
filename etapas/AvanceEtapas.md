# OlympX - Avance por Etapas

> Estado real del plan definido en `doc/Estructura por etapas.md`.
> Fuente de verdad para seguimiento con cliente y equipo.

## Resumen Ejecutivo

| Etapa | Nombre | Estado | Cobertura real |
| --- | --- | --- | --- |
| 1 | Discovery, planificación y UX/UI | Parcial | Documentación lista, Figma en curso |
| 2 | Backend, BD y autenticación | Casi completa | API funcional, contratos y seed |
| 3 | Gimnasios, GPS y biblioteca | Parcial alta | Gimnasios + ubicación + ejercicios |
| 4 | Rutinas y registro de entrenamiento | Parcial media | Sesiones y sets, sin rutinas completas |
| 5 | PRs, progreso y rankings | Parcial baja | Progreso básico y leaderboard inicial |
| 6 | Conquistas, estadísticas y notificaciones | Parcial baja | Notificaciones y stats base, sin capa full |
| 7 | QA, estabilización y cierre | Inicial | Smoke tests y typecheck, falta integración |

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
- Auth con login, `me`, admin login y token JWT.
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
- El modelo todavía no incluye rutinas semanales completas.
- Ya existe la base para registrar entrenamientos, pero la planificación semanal sigue pendiente.

### Balance
- **Estado:** Parcial media
- **Observación:** el flujo base de entrenamiento existe, pero la parte de rutinas sigue pendiente.

## Etapa 5 - PRs, Progreso y Rankings

### Entregables planificados
- Cálculo automático de PRs
- Tonelaje total por sesión y acumulado
- Gráfica de volumen semanal
- Rankings por ejercicio dentro del gimnasio
- Comparación entre usuarios

### Estado actual
- Hay estadísticas básicas de usuario.
- Existe base de leaderboard y progreso, pero no un sistema completo de PRs/rankings.
- Se calcula `estimated1rmKg` en sets, útil como base técnica.
- La capa de PRs y rankings todavía está en una fase inicial de base técnica.

### Balance
- **Estado:** Parcial baja

## Etapa 6 - Conquistas, Estadísticas y Notificaciones

### Entregables planificados
- Logros automáticos
- Perfil con estadísticas básicas
- Alertas push

### Estado actual
- Perfil con stats básicas ya disponible.
- Notifications existe como módulo, pero todavía no representa una capa completa de push/realtime.
- No hay sistema formal de conquistas completo.
- La Etapa 6 sigue en una base inicial: stats están, pero faltan conquistas automáticas y alertas push reales.

### Balance
- **Estado:** Parcial baja

## Etapa 7 - QA, Estabilización y Cierre

### Entregables planificados
- Pruebas funcionales e integración
- Corrección de bugs
- Estabilización productiva
- Coordinación general

### Estado actual
- Hay smoke tests en API, web y admin.
- Typecheck y format están funcionando en los subproyectos validados.
- Faltan suites de integración y E2E amplias.
- La Etapa 7 sigue inicial: la base de QA existe, pero falta cobertura suficiente para estabilización real.

### Balance
- **Estado:** Inicial

## Conclusión

El proyecto ya cubre con solidez la base de la Etapa 2 y una parte importante de la Etapa 3. Etapa 1 sigue abierta solo por el Figma/prototipo navegable; cuando se complete, puede cerrarse formalmente. El siguiente foco razonable es cerrar Etapa 4 y dejar PRs/rankings como siguiente bloque, mientras QA sigue creciendo en paralelo.

## Recomendación de Prioridad

1. Cerrar rutina completa y flujo de entrenamiento.
2. Completar check-in/GPS como flujo real.
3. Consolidar PRs y rankings.
4. Subir cobertura QA antes de expandir conquistas y notificaciones avanzadas.
