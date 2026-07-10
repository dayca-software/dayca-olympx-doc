# OlympX MVP 2026 - Backlog Tecnico Prisma

> Backlog accionable derivado de `PrismaPorFases.md` y `ModeloRelacionalGlobal.md`.
> Objetivo: convertir el alcance de datos en tareas implementables por fases, con dependencias y salida verificable.

## 1. Objetivo

Traducir el modelo global de datos en una secuencia de implementacion tecnica que el equipo pueda ejecutar sin ambiguedad.

## 2. Criterio De Priorizacion

- Primero el core que desbloquea el producto.
- Luego lo que agrega diferenciacion y revenue.
- Al final lo que opera, retiene y escala.

## 3. Backlog Por Fases

### Fase 1 - Core Producto

#### EPIC P1.1 - Base de entidades

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-001 | Normalizar `User` con `status` y tipos de peso/altura en `Decimal` | schema actual | Usuario consistente con modelo global |
| BT-002 | Normalizar `Gym` con `verified` y `status` | schema actual | Gimnasios listos para admin y ranking |
| BT-003 | Normalizar `Exercise` con `status` | schema actual | Catalogo estable y filtrable |

#### EPIC P1.2 - Entrenamiento

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-004 | Crear `WorkoutRoutine` | BT-001 | Rutinas persistibles |
| BT-005 | Crear `WorkoutRoutineDay` | BT-004 | Rutinas por dia |
| BT-006 | Crear `WorkoutRoutineExercise` | BT-005, BT-003 | Rutinas con ejercicios |
| BT-007 | Crear `TrainingSession` | BT-001, BT-002 | Sesiones registrables |
| BT-008 | Crear `TrainingSet` | BT-007, BT-003 | Sets persistidos |
| BT-009 | Crear `ExercisePR` | BT-007, BT-003 | PRs calculables |
| BT-010 | Crear `GymCheckin` | BT-001, BT-002 | Check-in por gimnasio |
| BT-011 | Crear `UserLocationSnapshot` | BT-001 | Ubicacion contextual |

#### EPIC P1.3 - Calidad de datos

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-012 | Definir enums para `TrainingSession.status` y `User.status` | BT-007, BT-001 | Estados controlados |
| BT-013 | Definir indexes para `email`, `nickname`, `gymId`, `userId` y relaciones de sesiones | BT-001 a BT-011 | Consultas mas rapidas |
| BT-014 | Crear seeds iniciales de ejercicios MVP | BT-003 | Catalogo base listo |

### Fase 2 - Rangos Y Competencia

#### EPIC P2.1 - Estandares de fuerza

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-015 | Crear `ExerciseStrengthStandard` | BT-003 | Estandar por ejercicio y sexo |
| BT-016 | Crear `ExerciseStrengthStandardBand` | BT-015 | Rangos por nivel |
| BT-017 | Definir seeds iniciales de estandares | BT-015, BT-016 | Rangos publicados |

#### EPIC P2.2 - Competencia local

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-018 | Crear `Conquest` | BT-007, BT-008, BT-015 | Conquistas semanales |
| BT-019 | Crear `Rivalry` | BT-001 | Rivales activos |
| BT-020 | Crear queries agregadas para rankings | BT-018, BT-015 | Rankings calculables |

### Fase 3 - Retencion Y Coach

#### EPIC P3.1 - Preferencias y objetivos

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-021 | Crear `UserGoal` | BT-001 | Metas semanales |
| BT-022 | Crear `CoachPreference` | BT-001 | Tono y nudges configurables |
| BT-023 | Crear `CoachEvent` | BT-022, BT-021 | Registro de decisiones del coach |

#### EPIC P3.2 - Notificaciones y resúmenes

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-024 | Crear `Notification` | BT-001 | Bandeja de notificaciones |
| BT-025 | Crear `ActivitySummary` | BT-007, BT-009, BT-018 | Resumenes compartibles |

### Fase 4 - Social Y Moderacion

#### EPIC P4.1 - Interaccion social

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-026 | Crear `UserFollow` | BT-001 | Seguimiento entre usuarios |
| BT-027 | Crear `Post` | BT-001 | Publicaciones temporales |
| BT-028 | Crear `PostReaction` | BT-027 | Reacciones fitness |
| BT-029 | Crear `PostComment` | BT-027 | Comentarios |

#### EPIC P4.2 - Moderacion

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-030 | Crear `Report` | BT-027, BT-029 | Reportes manuales |

### Fase 5 - Comercial

#### EPIC P5.1 - Planes y trials

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-031 | Crear `SubscriptionPlan` | - | Planes Free y Paid |
| BT-032 | Crear `PlanFeatureLimit` | BT-031 | Limites por plan |
| BT-033 | Crear `TrialPolicy` | BT-031 | Politica de trial |
| BT-034 | Crear `Subscription` | BT-031, BT-033 | Suscripciones activas y trials |
| BT-035 | Crear `Coupon` | BT-031 | Cupones promocionales |
| BT-036 | Crear `FreeSignupCap` como singleton configurado | BT-031, BT-033 | Cupo Free y fallback a trial |

#### EPIC P5.2 - Control comercial

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-037 | Definir reglas de versionado de plan y precios | BT-031 | Historial de cambios |
| BT-038 | Definir contador y migracion para cupo Free | BT-036 | Registro sin romper usuarios existentes |

### Fase 6 - Admin Y Auditoria

#### EPIC P6.1 - Operacion interna

| ID | Tarea | Dependencia | Salida |
|----|------|-------------|--------|
| BT-039 | Crear `AdminUser` | - | Acceso interno |
| BT-040 | Crear `AuditLog` | BT-039, BT-031, BT-030 | Trazabilidad completa |

## 4. Orden De Ejecucion

| Orden | Fase | Motivo |
|------|------|--------|
| 1 | P1 | Desbloquea el producto |
| 2 | P2 | Agrega competitividad |
| 3 | P5 | Habilita monetizacion |
| 4 | P6 | Asegura operacion y auditoria |
| 5 | P3 | Refuerza retencion |
| 6 | P4 | Escala comunidad y moderacion |

## 5. Definition Of Done Tecnica

- Modelo en Prisma creado o actualizado.
- Migracion o `db push` definida.
- Relaciones validadas.
- Seeds actualizados si aplica.
- Tests de integracion o unitarios ajustados si el dominio lo requiere.
- Documentacion sincronizada.

## 6. Riesgos Tecnicos

- Mezclar dominios en una sola migracion grande.
- Introducir enums antes de estabilizar los flujos.
- Romper contratos del frontend con cambios de tipo.
- Duplicar logica de Free/trial entre schema y admin.
