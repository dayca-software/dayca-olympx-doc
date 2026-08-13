# OlympX - Carta Gantt MVP

> Cronograma ejecutivo del MVP en 8 semanas.

```mermaid
gantt
  title OlympX MVP Core - 8 semanas
  dateFormat  YYYY-MM-DD
  axisFormat   %d/%m

  section Fundacion
  Discovery, alcance y UX/UI        :a1, 2026-08-11, 14d

  section Autenticacion y Core
  Arquitectura, auth y perfil       :a2, after a1, 14d

  section Entrenamiento
  Gimnasios, GPS y biblioteca      :b1, after a2, 14d
  Rutinas, sesiones y PRs          :b2, after b1, 14d

  section Progreso y Competencia
  Fuerza                           :c1, after b2, 7d
  Comparacion                      :c2, after c1, 7d

  section Cierre
  QA, pulido visual y preparacion  :d1, after c2, 14d
```

## Hitos

- Hito 1: base de producto y autenticacion lista.
- Hito 2: entrenamiento y gimnasio operativo.
- Hito 3: progreso, PRs y comparacion funcional.
- Hito 4: QA, ajustes finales y entrega MVP.
