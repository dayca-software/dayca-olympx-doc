# Etapa 4 - Checklist Rutinas y Registro de Entrenamiento

> Criterio mínimo para considerar cerrada la implementación de la Etapa 4.

## Entregables esperados

- Creacion de rutinas personalizadas.
- Registro de entrenamiento en vivo.
- Ingreso de series, repeticiones, peso, RPE, RIR y notas.
- Finalizacion y guardado de sesiones.
- Historial de entrenamientos.

## Cobertura actual

- Creacion y edicion de rutinas persistentes disponible.
- Organizacion de dias por semana disponible.
- Inicio de sesiones desde una rutina disponible.
- Plantillas reutilizables desde una sesión registrada, con sets y repeticiones promedio derivados.
- Aislamiento por usuario en consulta y edición de rutinas (404 sobre rutinas ajenas).
- Selección de día por `dayId` o `dayOfWeek` al iniciar una rutina.
- Registro de sets disponible con peso, repeticiones, RPE, RIR y notas.
- Captura de RPE, RIR y notas validada de punta a punta en el flujo de registro (DTO y detalle).
- Finalizacion, resumen e historial de entrenamientos disponible.
- Cola offline para crear sesiones, registrar sets y solicitar el cierre, con claves de idempotencia.
- Sesiones offline completas desde la UI con IDs de cliente estables y actualización optimista de sets.
- Catálogo de ejercicios cacheado para continuar registrando sets sin conexión.
- Selección y persistencia del día de rutina al iniciar una sesión.
- Migración de día de rutina aplicada automáticamente al arrancar el contenedor de API.
- Flujo Maestro online actualizado para registrar, editar, finalizar y revisar historial.
- Flujo Maestro offline preparado para validar pérdida y recuperación de conexión.
- Base tecnica para calculo de volumen y 1RM estimado.
- API de training: 9 archivos y 49 tests pasando, incluyendo plantillas desde sesión, selección de
  día, aislamiento por usuario y edición completa de rutinas.
- Mobile: 14 suites y 41 tests pasando, incluyendo historial paginado, ranking por ejercicio, editor
  de rutina (día semanal, alta y reordenamiento de ejercicios), cola offline y resumen.
- Migración Prisma aplicada con `prisma migrate deploy` sobre PostgreSQL local; no quedaron migraciones pendientes.

## Pendientes de validación operativa

- Ejecutar E2E completo de rutina en Android e iOS físicos.
- Validar reconexión offline real con sets y cierre de sesión en dispositivo.
- Publicar y aplicar la migración Prisma en staging; el contenedor ya ejecuta `prisma migrate deploy`.

## Criterio de aprobacion

- [x] El usuario puede crear una rutina, asignar días y reutilizarla.
- [x] El usuario puede registrar una sesión completa sin fricción en línea.
- [x] Los sets soportan RPE, RIR, peso y notas.
- [x] El historial refleja sesiones y progreso agregado.
- [ ] El flujo completo está validado E2E en dispositivos físicos.

La implementación de código está completa; estos tres puntos requieren infraestructura y hardware
que no están disponibles en el entorno local.
