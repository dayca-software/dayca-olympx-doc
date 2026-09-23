# Etapa 4 - Checklist Rutinas y Registro de Entrenamiento

> Criterio minimo para considerar cerrada la Etapa 4.

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
- Registro de sets disponible con peso, repeticiones, RPE, RIR y notas.
- Finalizacion, resumen e historial de entrenamientos disponible.
- Cola offline para crear sesiones, registrar sets y solicitar el cierre, con claves de idempotencia.
- Base tecnica para calculo de volumen y 1RM estimado.
- API de training: 7 archivos y 31 tests pasando.
- Mobile: 12 suites y 35 tests pasando, incluyendo editor de rutina, cola offline y resumen.
- Migración Prisma validada con `prisma migrate deploy` sobre PostgreSQL efímero; una segunda ejecución no dejó migraciones pendientes.

## Pendientes de cierre

- Ejecutar E2E completo de rutina en Android e iOS físicos.
- Validar reconexión offline real con sets y cierre de sesión en dispositivo.
- Decidir si el historial debe ampliarse con paginación más allá de las 10 sesiones actuales.
- Publicar y aplicar la migración Prisma en staging; la validación local efímera ya está completada.

## Criterio de aprobacion

- [x] El usuario puede crear una rutina, asignar días y reutilizarla.
- [x] El usuario puede registrar una sesión completa sin fricción en línea.
- [x] Los sets soportan RPE, RIR, peso y notas.
- [x] El historial refleja sesiones y progreso agregado.
- [ ] El flujo completo está validado E2E en dispositivos físicos.
