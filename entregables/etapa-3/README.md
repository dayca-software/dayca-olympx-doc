# Entregables Etapa 3

## Gimnasios, GPS, Check-in Y Biblioteca De Ejercicios

| Campo              | Valor                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duración           | Semanas 4-6                                                                                                                                                       |
| Horas cotizadas    | 140 h                                                                                                                                                             |
| Estado             | Completada según el alcance aprobado                                                                                                                              |
| Criterio de cierre | El usuario puede encontrar gimnasios, consultar su información, elegir un gimnasio principal, realizar check-in contextual y utilizar la biblioteca de ejercicios |

## Alcance Validado

La etapa se considera entregada con los siguientes bloques:

- Catálogo y búsqueda de gimnasios.
- Uso puntual de la ubicación del usuario para encontrar gimnasios cercanos.
- Actualización de la última ubicación válida del usuario.
- Detalle de gimnasio con estado, ubicación y actividad local.
- Selección y persistencia del gimnasio principal.
- Check-in contextual con validación de distancia y disponibilidad.
- Protección contra check-ins duplicados recientes.
- Acceso a mapas desde el detalle del gimnasio.
- Biblioteca de ejercicios con búsqueda, filtros, metadatos y detalle.
- Identificación de ejercicios competitivos y no competitivos.
- Integración API, mobile, contratos compartidos y soporte administrativo.

## Decisión De Alcance

El equipamiento de los gimnasios o ejercicios no forma parte de la entrega cerrada de esta etapa. Se mantiene como trabajo planificado para una etapa posterior, por lo que no se considera una brecha de la Etapa 3.

La etapa tampoco incorpora tracking continuo de ubicación, navegación indoor, heatmaps avanzados, usuarios cercanos en tiempo real ni solicitudes de gimnasios ausentes del catálogo. Esos temas pertenecen a extensiones o etapas posteriores.

## Documentos

| Documento                                                        | Descripción                                                                        |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| [`01-especificacion-tecnica.md`](./01-especificacion-tecnica.md) | Arquitectura, datos, API, reglas de negocio, mobile, administración y validaciones |
| [`02-resumen-para-usuario.md`](./02-resumen-para-usuario.md)     | Explicación completa en lenguaje simple para personas sin perfil técnico           |

## Fuentes De Trazabilidad

- [`AnexoMVP.md`](../../AnexoMVP.md): planificación y entregables cotizados.
- [`BaseRequerimientos.md`](../../BaseRequerimientos.md): requisitos de gimnasios, GPS y ejercicios.
- [`MatrizTrazabilidad.md`](../../MatrizTrazabilidad.md): relación entre necesidades, módulos y datos.
- [`Etapa3Checklist.md`](../../etapas/Etapa3Checklist.md): checklist funcional de la etapa.
- [`PlanCierreEtapa3.md`](../../etapas/PlanCierreEtapa3.md): reglas y alcance de cierre.
- [`Etapa3Cliente.md`](../../etapas/Etapa3Cliente.md): resumen ejecutivo anterior de la etapa.

## Evidencia General

- API: 40 archivos de tests y 245 tests pasando.
- Mobile: 14 suites y 37 tests pasando.
- Typecheck y builds de los proyectos principales ejecutados correctamente.
- Flujos de búsqueda, detalle, selección de gimnasio principal y check-in verificados en los targets mobile documentados.
