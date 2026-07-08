# OlympX MVP 2026 - Matriz de Documentacion

> Guia rapida para saber que documento actualizar segun el tipo de cambio.

## 1. Objetivo

Evitar duplicacion, mantener trazabilidad y asegurar que cada cambio actualice la fuente correcta.

## 2. Regla General

- Si cambia el negocio, actualiza `BaseRequerimientos.md`.
- Si cambia el alcance de una feature, actualiza el documento de alcance especifico.
- Si cambia el almacenamiento o relaciones, actualiza `ModeloRelacionalMVP.md`.
- Si cambia el presupuesto o etapas, actualiza `AnexoMVP.md`.
- Si cambia la guia operativa general del proyecto, actualiza `CLAUDE.md`.

## 3. Matriz Por Tipo De Cambio

| Tipo de cambio | Documento principal | Documentos secundarios | Ejemplo |
|----------------|---------------------|------------------------|---------|
| Nueva feature | `BaseRequerimientos.md` | `Alcance*.md`, `ModeloRelacionalMVP.md` | Agregar rangos de fuerza |
| Cambio de scope | `Alcance*.md` | `BaseRequerimientos.md` | Pasar de solo visualizacion a highlighter interactivo |
| Nuevo campo o entidad | `ModeloRelacionalMVP.md` | `BaseRequerimientos.md` | Agregar `Muscle` o `ExerciseMuscleTarget` |
| Cambio de regla de negocio | `BaseRequerimientos.md` | `Alcance*.md` | Definir si `otros` entra en ranking de fuerza |
| Cambio de UX/flujo | `BaseRequerimientos.md` | `Alcance*.md` | Agregar plantilla PDF compartible |
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
| `AlcanceMusculosYRangos.md` | Producto + UX | Cuando cambie el scope de esa feature |
| `AnexoMVP.md` | Producto + Delivery | Cuando cambie costo, etapas u horas |

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
- Planificacion: `AnexoMVP.md`
- Contexto general: `CLAUDE.md`
