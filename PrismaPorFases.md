# OlympX MVP 2026 - Prisma Por Fases

> Plan de implementacion Prisma derivado de `ModeloRelacionalGlobal.md`.
> Objetivo: llevar el alcance total a la base de datos sin mezclar dominios ni romper el MVP.
> El backlog tecnico ejecutable vive en `BacklogTecnicoPrisma.md`.

## 1. Objetivo

Dividir el modelo global en fases implementables, con orden de entrega, dependencias y criterios de salida claros.

## 2. Principio De Corte

- La fase siguiente no bloquea el valor de la fase anterior.
- Cada fase debe ser migrable y testeable por separado.
- El MVP Core se mantiene util aun sin social completo, coach completo o BI completo.

## 3. Fases Prisma

### Fase 1 - Core Producto

Incluye:

- `User`
- `Gym`
- `Exercise`
- `WorkoutRoutine`
- `WorkoutRoutineDay`
- `WorkoutRoutineExercise`
- `TrainingSession`
- `TrainingSet`
- `ExercisePR`
- `GymCheckin`
- `UserLocationSnapshot`

Objetivo:

- Permitir registro, entrenamiento, progreso y contexto de gimnasio.

Salida esperada:

- El usuario puede registrarse, entrenar y ver su progreso.

### Fase 2 - Rangos Y Competencia

Incluye:

- `ExerciseStrengthStandard`
- `ExerciseStrengthStandardBand`
- `Conquest`
- `Rivalry`

Objetivo:

- Habilitar comparacion universal, conquistas y competencia local.

Salida esperada:

- El usuario puede comparar rendimiento por ejercicio y ver titulos competitivos.

### Fase 3 - Retencion Y Coach

Incluye:

- `UserGoal`
- `CoachPreference`
- `CoachEvent`
- `Notification`
- `ActivitySummary`

Objetivo:

- Aumentar adherencia, retorno y acompanamiento sin terapia clinica.

Salida esperada:

- El usuario recibe recordatorios, refuerzo positivo y resuemenes de progreso.

### Fase 4 - Social Y Moderacion

Incluye:

- `UserFollow`
- `Post`
- `PostReaction`
- `PostComment`
- `Report`

Objetivo:

- Habilitar red social, interaccion y moderacion manual.

Salida esperada:

- El usuario puede seguir, publicar, reaccionar, comentar y reportar.

### Fase 5 - Comercial

Incluye:

- `SubscriptionPlan`
- `PlanFeatureLimit`
- `TrialPolicy`
- `Subscription`
- `Coupon`
- `FreeSignupCap`

Objetivo:

- Monetizar Freemium, trials y limites de acceso.

Salida esperada:

- El sistema puede cobrar, limitar Free y ofrecer trial con reglas comerciales.

### Fase 6 - Admin Y Auditoria

Incluye:

- `AdminUser`
- `AuditLog`

Objetivo:

- Habilitar operacion interna, moderacion y trazabilidad.

Salida esperada:

- El equipo interno puede operar, auditar y controlar el sistema.

## 4. Orden Recomendado De Implementacion

| Orden | Fase   | Motivo                              |
| ----- | ------ | ----------------------------------- |
| 1     | Fase 1 | Desbloquea el MVP Core              |
| 2     | Fase 2 | Agrega diferenciacion competitiva   |
| 3     | Fase 5 | Permite monetizacion temprana       |
| 4     | Fase 6 | Asegura operacion y soporte         |
| 5     | Fase 3 | Refuerza retencion y acompanamiento |
| 6     | Fase 4 | Maximiza viralidad y comunidad      |

> Nota: si el negocio exige monetizar antes, Fase 5 puede subirse antes que Fase 2, pero no debe romper el MVP Core.

## 5. Reglas De Implementacion Prisma

| Regla | Descripcion                                                                               |
| ----- | ----------------------------------------------------------------------------------------- |
| R-001 | Cada fase debe poder agregarse sin reescribir el core existente                           |
| R-002 | Las relaciones nuevas no deben romper el contrato actual del frontend                     |
| R-003 | Los enums deben consolidarse al final de cada fase                                        |
| R-004 | Los campos opcionales se usan para evitar migraciones costosas al principio               |
| R-005 | Las tablas de auditoria y comercio deben quedar listas antes de activar monetizacion real |

## 6. Mapeo A Prisma Actual

| Entidad actual en `schema.prisma` | Fase destino |
| --------------------------------- | ------------ |
| `User`                            | Fase 1       |
| `Gym`                             | Fase 1       |
| `Exercise`                        | Fase 1       |

## 7. Pendientes Tecnicos

- Definir si se mantiene un solo `schema.prisma` por fases o si se documenta un split logico por dominios.
- Alinear tipos `Float` actuales con `Decimal` donde aplique para pesos y monetizacion.
- Definir enums finales para `status`, `role`, `tone`, `eventType`, `subscriptionStatus`, `featureKey`.
- Planificar seeds por fase.
