# OlympX MVP 2026 - Matriz de Documentacion

> Guia rapida para saber que documento actualizar segun el tipo de cambio.

## 1. Objetivo

Evitar duplicacion, mantener trazabilidad y asegurar que cada cambio actualice la fuente correcta.

## 2. Regla General

- Si cambia el negocio, actualiza `BaseRequerimientos.md`.
- Si cambia el alcance de una feature, actualiza el documento de alcance especifico.
- Si cambia el almacenamiento o relaciones, actualiza `ModeloRelacionalMVP.md`.
- Si cambia el almacenamiento o relaciones a nivel global, actualiza `ModeloRelacionalGlobal.md`.
- Si cambia la estrategia de implementacion Prisma por fases, actualiza `PrismaPorFases.md`.
- Si cambia el backlog tecnico Prisma, actualiza `BacklogTecnicoPrisma.md`.
- Si cambia el plan sprint Prisma, actualiza `PlanSprintPrisma.md`.
- Si cambia el presupuesto o etapas, actualiza `AnexoMVP.md`.
- Si cambia la guia operativa general del proyecto, actualiza `CLAUDE.md`.
- Si cambia la priorizacion ejecutiva, actualiza `ResumenEjecutivoPO.md`.
- Si cambia el panel interno de administracion, actualiza `AdminRequerimientos.md`.
- Si cambia el modulo de coach o acompanamiento, actualiza `CoachRequerimientos.md`.
- Si cambia la trazabilidad entre vision, requerimientos y datos, actualiza `MatrizTrazabilidad.md`.

## 3. Matriz Por Tipo De Cambio

| Tipo de cambio | Documento principal | Documentos secundarios | Ejemplo |
|----------------|---------------------|------------------------|---------|
| Nueva feature | `BaseRequerimientos.md` | `Alcance*.md`, `ModeloRelacionalMVP.md` | Agregar rangos de fuerza |
| Cambio de scope | `Alcance*.md` | `BaseRequerimientos.md` | Pasar de solo visualizacion a highlighter interactivo |
| Nuevo campo o entidad | `ModeloRelacionalMVP.md` | `BaseRequerimientos.md` | Agregar `Muscle` o `ExerciseMuscleTarget` |
| Nuevo campo o entidad global | `ModeloRelacionalGlobal.md` | `ModeloRelacionalMVP.md`, `BaseRequerimientos.md` | Agregar `CoachEvent` o `SubscriptionPlan` |
| Cambio de estrategia Prisma | `PrismaPorFases.md` | `ModeloRelacionalGlobal.md`, `ModeloRelacionalMVP.md` | Reordenar fases o dominios |
| Cambio de backlog tecnico Prisma | `BacklogTecnicoPrisma.md` | `PrismaPorFases.md`, `ModeloRelacionalGlobal.md` | Dividir Fase 1 en tareas BT-001..BT-040 |
| Cambio de plan sprint Prisma | `PlanSprintPrisma.md` | `BacklogTecnicoPrisma.md` | Reordenar BTs en sprints |
| Cambio de regla de negocio | `BaseRequerimientos.md` | `Alcance*.md` | Definir si `otros` entra en ranking de fuerza |
| Cambio de UX/flujo | `BaseRequerimientos.md` | `Alcance*.md` | Agregar plantilla PDF compartible |
| Cambio de coach/acompanamiento | `CoachRequerimientos.md` | `BaseRequerimientos.md` | Mensajes de animo, nudges o estados pre-sesion |
| Cambio de etapas/horas | `AnexoMVP.md` | `BaseRequerimientos.md` | Mover rangos de fuerza de E5 a E6 |
| Cambio tecnico operativo | `CLAUDE.md` | `BaseRequerimientos.md` | Ajustar comandos, stack o estructura |
| Cambio de API contract | `BaseRequerimientos.md` | `ModeloRelacionalMVP.md` | Cambiar envelope o estructura de respuesta |
| Cambio de seeds/catalogos | `ModeloRelacionalMVP.md` | `BaseRequerimientos.md` | Lista inicial de ejercicios o musculos |

## 4. Dueño Del Documento

| Documento | Dueño | Frecuencia de revision |
|-----------|-------|------------------------|
| `CLAUDE.md` | Contexto del proyecto | Cuando cambie el proyecto o stack |
| `BaseRequerimientos.md` | Producto / Analisis | Cada cambio funcional |
| `ModeloRelacionalMVP.md` | Backend / Datos | Cada cambio en entidades o relaciones |
| `ModeloRelacionalGlobal.md` | Backend / Datos | Cuando cambie el alcance global de datos |
| `PrismaPorFases.md` | Backend / Datos | Cuando cambie la estrategia de implementacion Prisma |
| `BacklogTecnicoPrisma.md` | Backend / Datos | Cuando cambie el backlog tecnico de implementacion Prisma |
| `PlanSprintPrisma.md` | Backend / Datos | Cuando cambie la ejecucion sprint a sprint |
| `AlcanceMusculosYRangos.md` | Producto + UX | Cuando cambie el scope de esa feature |
| `AnexoMVP.md` | Producto + Delivery | Cuando cambie costo, etapas u horas |
| `ResumenEjecutivoPO.md` | Producto | Cuando cambie el mensaje ejecutivo o la prioridad |
| `AdminRequerimientos.md` | Operaciones / Admin | Cuando cambie el panel interno, moderacion o soporte |
| `CoachRequerimientos.md` | Producto / Retencion | Cuando cambie el acompanamiento, nudges o bienestar ligero |
| `MatrizTrazabilidad.md` | Producto + BA + Engineering | Cuando cambie la relacion entre vision, requisitos y datos |

## 5. Checklist Antes De Cerrar Un Cambio

- [ ] El cambio esta reflejado en el documento principal.
- [ ] No hay contradicciones con otros documentos.
- [ ] El alcance del MVP sigue siendo claro.
- [ ] El modelo de datos soporta la funcionalidad.
- [ ] Las etapas y horas siguen siendo coherentes si aplica.

## 6. Documentos Fuente De Verdad

- Negocio: `BaseRequerimientos.md`
- Alcance feature: `AlcanceMusculosYRangos.md`
- Datos: `ModeloRelacionalMVP.md`
- Datos globales: `ModeloRelacionalGlobal.md`
- Prisma por fases: `PrismaPorFases.md`
- Backlog tecnico Prisma: `BacklogTecnicoPrisma.md`
- Plan sprint Prisma: `PlanSprintPrisma.md`
- Planificacion: `AnexoMVP.md`
- Contexto general: `CLAUDE.md`
- Admin interno: `AdminRequerimientos.md`
- Coach interno: `CoachRequerimientos.md`
