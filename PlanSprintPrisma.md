# OlympX MVP 2026 - Plan Sprint Prisma

> Plan de ejecucion sprint a sprint para implementar Prisma desde el backlog tecnico.
> Este documento ya es de entrega tecnica, no de analisis.

## 1. Objetivo

Traducir el backlog tecnico Prisma a sprints ejecutables, con secuencia, entregables y validacion clara.

## 2. Cadencia Recomendada

- 1 sprint = 2 semanas.
- Cada sprint debe cerrar con schema estable, seeds o migracion valida, y una prueba de integracion minima.

## 3. Plan Sprint A Sprint

### Sprint 1 - Core Base

Incluye:
- BT-001
- BT-002
- BT-003

Entrega:
- `User`, `Gym`, `Exercise` normalizados.
- Tipos de datos corregidos.
- Primeras restricciones e indices base.

Validacion:
- Login, perfil y catalogo de ejercicio no se rompen.

### Sprint 2 - Entrenamiento I

Incluye:
- BT-004
- BT-005
- BT-006
- BT-012

Entrega:
- Rutinas por dia con ejercicios.
- Estados de sesion definidos.

Validacion:
- Una rutina se puede crear y leer de punta a punta.

### Sprint 3 - Entrenamiento II

Incluye:
- BT-007
- BT-008
- BT-009
- BT-010
- BT-011
- BT-013
- BT-014

Entrega:
- Sesiones, sets, PRs y check-ins funcionando.
- Ubicacion contextual lista.
- Seeds iniciales cargados.

Validacion:
- El MVP Core ya puede registrar progreso real.

### Sprint 4 - Rangos Y Competencia

Incluye:
- BT-015
- BT-016
- BT-017
- BT-018
- BT-019
- BT-020

Entrega:
- Rangos universales.
- Conquistas.
- Rivales.
- Queries de rankings.

Validacion:
- El usuario ya puede comparar y competir.

### Sprint 5 - Monetizacion

Incluye:
- BT-031
- BT-032
- BT-033
- BT-034
- BT-035
- BT-036
- BT-037
- BT-038

Entrega:
- Planes, trial, cupones y cupo Free.
- Versionado comercial definido.

Validacion:
- El producto puede cobrar y limitar acceso Free.

### Sprint 6 - Admin Y Auditoria

Incluye:
- BT-039
- BT-040

Entrega:
- Usuarios internos.
- Audit log.

Validacion:
- Operacion interna y trazabilidad listas.

### Sprint 7 - Retencion Y Coach

Incluye:
- BT-021
- BT-022
- BT-023
- BT-024
- BT-025

Entrega:
- Metas, coach, notificaciones y resúmenes.

Validacion:
- El usuario recibe acompañamiento y recordatorios.

### Sprint 8 - Social Y Moderacion

Incluye:
- BT-026
- BT-027
- BT-028
- BT-029
- BT-030

Entrega:
- Follow, posts, reacciones, comentarios y reportes.

Validacion:
- La capa social queda operativa y moderable.

## 4. Dependencias Entre Sprints

| Sprint | Bloqueante de |
|-------|----------------|
| 1 | Todos los demas |
| 2 | 3, 4, 7, 8 |
| 3 | 4, 7, 8 |
| 4 | 7, 8 |
| 5 | 6 |
| 6 | Ninguno |
| 7 | 8 |

## 5. Definition Of Done Por Sprint

- Migracion aplicada o schema validado.
- Relaciones probadas.
- Seeds o fixtures actualizados.
- Tests ajustados.
- Documentacion sincronizada.

## 6. Riesgos De Ejecucion

- Sprint 1 atrasado bloquea todo el plan.
- Monetizacion antes de core funcional puede degradar conversion.
- Coach y social sin limites claros pueden generar ruido.
