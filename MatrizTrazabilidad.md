# OlympX MVP 2026 - Matriz de Trazabilidad

> Mapa de referencia para PO, BA y engineering.

## 1. Objetivo

Conectar vision, requerimientos, etapas, datos y entrega para evitar ambiguedad de alcance.

## 2. Mapa General

| Capa | Documento fuente | Uso principal |
|------|------------------|---------------|
| Vision total | `GlobalProjecto.md` | PO / direccion de producto |
| Requerimientos base | `BaseRequerimientos.md` | BA / engineering |
| Planificacion | `AnexoMVP.md` | Delivery / presupuesto / fases |
| Datos | `ModeloRelacionalMVP.md` | Backend / DB / API |
| Extension muscular | `AlcanceMusculosYRangos.md` | Feature scope especifico |

## 3. Trazabilidad Por Mapa De Producto

| Tema | Vision | Requerimientos | Etapa | Datos |
|------|--------|----------------|-------|-------|
| Auth y perfil | `GlobalProjecto.md` seccion 5.3 y 5.4 | M01 | E2 | `User` |
| Gyms y GPS | `GlobalProjecto.md` seccion 6 | M02 | E3 | `Gym`, `GymCheckin`, `UserLocationSnapshot` |
| Biblioteca de ejercicios | `GlobalProjecto.md` seccion 5.4 y 8 | M03 | E3 | `Exercise` |
| Rutinas y tracking | `GlobalProjecto.md` seccion 4 y 9 | M04 | E4 | `WorkoutRoutine`, `WorkoutRoutineDay`, `WorkoutRoutineExercise`, `TrainingSession`, `TrainingSet` |
| PRs y progreso | `GlobalProjecto.md` seccion 9 | M05 | E5 | `ExercisePR` |
| Rangos de fuerza | `GlobalProjecto.md` seccion 9 y 10 | M11 | E5 | `ExerciseStrengthStandard`, `ExerciseStrengthStandardBand` |
| Conquistas | `GlobalProjecto.md` seccion 8 | M06 | E6 | derivado de `TrainingSet` y `ExercisePR` |
| Feed social | `GlobalProjecto.md` seccion 7 | M07 | E6 o post-MVP | `UserFollow` + entidad de posts futura |
| Notificaciones | `GlobalProjecto.md` seccion 11 | M08 | E6 | futura cola/eventos |
| Activity summary | `GlobalProjecto.md` seccion 12 | M09 | Post-MVP | derivado de sesiones/PRs/conquistas |
| Rivalidades y titles | `GlobalProjecto.md` seccion 13 | M10 | Post-MVP | derivado de usuarios, PRs y rankings |
| Coach y acompanamiento | `GlobalProjecto.md` objetivo psicologico y beneficios psicologicos | M12 | Fase 2 | derivado de sesiones, estados pre-sesion y preferencias |

## 4. Trazabilidad Por Fase

| Fase | Cobertura | Criterio de salida |
|------|-----------|--------------------|
| MVP Core | M01, M02, M03, M04, M05, M11 | El usuario puede registrarse, entrenar y ver progreso |
| Fase 2 | M06, M07, M08, M09, M10, M12 | El usuario puede competir, compartir, retenerse por comunidad y recibir acompanamiento |

## 5. Trazabilidad Cliente -> Modulo -> RF -> CA -> CB

| Necesidad del cliente | Modulo | RF clave | CA clave | CB clave |
|-----------------------|--------|----------|----------|----------|
| Registrar progreso sin friccion | M01, M04, M05 | RF-001, RF-005, RF-031, RF-033, RF-038 | CA-001, CA-002, CA-004, CA-005 | CB-001, CB-003, CB-004, CB-010 |
| Competir y compararse en gimnasio y categoria | M05, M06, M11 | RF-041, RF-042, RF-046, RF-047, RF-087, RF-089 | CA-005, CA-006, CA-008 | CB-006 |
| Identidad competitiva clara | M01, M06, M07, M09, M10 | RF-013, RF-046, RF-052, RF-061, RF-075, RF-082, RF-083 | CA-007 | CB-007, CB-009 |
| Monetizar con freemium sin frenar adopcion | M01, M05, M11 | RF-009, RF-089, RF-090 | CA-009 | CB-008 |
| Validar en 3-5 gimnasios piloto | M02, M05, M06 | RF-014, RF-015, RF-016, RF-018, RF-046 | CA-003, CA-008 | CB-001, CB-002 |
| Generar contenido compartible | M06, M08, M09 | RF-050, RF-052, RF-065, RF-068, RF-075, RF-076 | CA-007 | CB-007, CB-009 |
| No depender de tracking continuo ni IA | M02, M04, M07, M09 | RF-008, RF-011, RF-027, RF-054, RF-067, RF-075 | CA-007 | CB-001, CB-010 |
| Priorizar entrenamiento y progreso antes que red social | M04, M05, M11 | RF-031, RF-033, RF-038, RF-087, RF-091 | CA-004, CA-005, CA-006 | CB-004, CB-006 |
| Apoyo motivacional y adherencia | M12 | RF-092, RF-093, RF-094, RF-095, RF-096, RF-097, RF-099 | CA-010, CA-011, CA-012, CA-013 | CB-010, CB-011, CB-012, CB-013 |

## 6. Reglas de uso

- Si cambia una feature, actualiza `BaseRequerimientos.md` primero.
- Si cambia una entidad o relacion, actualiza `ModeloRelacionalMVP.md`.
- Si cambia el orden de entrega o la financiacion, actualiza `AnexoMVP.md`.
- Si cambia la vision, actualiza `GlobalProjecto.md`.

## 7. Observacion

La trazabilidad de `M07`, `M08`, `M09`, `M10` y `M12` existe en vision y requerimientos, pero su implementacion deberia considerarse posterior al MVP Core salvo decision explicita de ampliar alcance.
