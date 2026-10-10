# Etapa 4 - Especificación Técnica

## 1. Alcance implementado

La Etapa 4 cubre el loop completo de entrenamiento personal:

1. Crear una rutina y organizar sus días.
2. Iniciar una sesión desde una rutina o desde un entreno rápido.
3. Registrar sets durante la sesión.
4. Finalizar la sesión y consultar el resumen.
5. Consultar historial, progreso agregado y sesiones anteriores.

## 2. API de entrenamiento

### Rutinas

- `GET /api/training/routines`: lista las rutinas propias.
- `GET /api/training/routines/:id`: devuelve días, orden y objetivos.
- `POST /api/training/routines`: crea una rutina persistente.
- `PATCH /api/training/routines/:id`: reemplaza de forma transaccional sus días y ejercicios.
- `POST /api/training/routines/:id/start`: inicia una sesión para un día específico mediante `dayId` o `dayOfWeek`.
- `POST /api/training/routines/from-session/:sessionId`: guarda una sesión como rutina reutilizable.

Las sesiones iniciadas desde una rutina persisten `routineDayId`, evitando mezclar los ejercicios de todos los días de la semana.

### Sesiones y sets

- `POST /api/training/sessions`: crea una sesión. Acepta `Idempotency-Key` y `clientSessionId`.
- `GET /api/training/sessions`: historial paginado por cursor.
- `GET /api/training/sessions/:id`: detalle con sets.
- `POST /api/training/sessions/:id/sets`: registra peso, reps, RPE, RIR, tipo y notas.
- `PATCH /api/training/sessions/:id/finish`: finaliza una sesión con al menos un set.
- `PATCH /api/training/sessions/:id/cancel`: cancela una sesión activa.
- `DELETE /api/training/sessions/:id`: elimina una sesión propia.
- `GET /api/training/progress`: devuelve volumen, reps y evolución semanal.

## 3. Funcionamiento offline

La app conserva la secuencia de acciones en AsyncStorage:

1. La creación genera un `clientSessionId` estable y encola la sesión.
2. Los sets usan ese mismo ID en su URL y conservan su clave de idempotencia.
3. El cierre se encola después de los sets.
4. La cola conserva hasta 100 acciones, suficiente para una sesión de 50 sets más creación y cierre.
5. Al recuperar conectividad, `foregroundSync` envía las acciones en orden por usuario.
6. El detalle actualiza los sets localmente y puede mostrar el resumen antes de la sincronización.

El catálogo de ejercicios se cachea después de una carga online para poder registrar sets sin conexión.

## 4. Persistencia

La migración `20261010120000_training_routine_day_sessions` agrega la relación opcional entre una
sesión y el día de rutina seleccionado. El contenedor de API ejecuta `prisma migrate deploy` antes de iniciar NestJS mediante `deploy/start.sh`.

El seed asigna lunes, martes y miércoles a las rutinas de ejemplo; no deja todos los días en lunes.

## 5. Validación

- API: typecheck y tests del flujo de training, incluyendo idempotencia, selección de día y cierre.
- Mobile: typecheck, tests de cola offline, editor de rutina, historial y resumen.
- Maestro: flujo online actualizado para registrar, editar, compartir, guardar rutina, finalizar y abrir historial.
- Maestro: flujo offline preparado en `olympx-mobile/.maestro/training-offline-smoke.yaml`.

La ejecución de Maestro en Android/iOS físicos y la aplicación de migraciones contra staging son
validaciones operativas pendientes de credenciales, dispositivos y URL HTTPS reales.
