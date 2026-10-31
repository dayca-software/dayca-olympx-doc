# Etapa 5 - Checklist PRs, Progreso y Rankings

> Criterio minimo para considerar cerrada la Etapa 5.

## Entregables esperados

- Calculo automatico de PRs.
- Tonelaje total por sesion y acumulado.
- Grafica de volumen semanal.
- Rankings por ejercicio dentro del gimnasio.
- Comparacion entre usuarios del mismo gimnasio.

## Cobertura actual

- Base tecnica para 1RM estimado disponible.
- PRs persistidos por evento, con sesión de origen y backfill de históricos.
- Estadisticas basicas de usuario disponibles.
- Progreso semanal con volumen, comparación contra la semana anterior y filtros de ventana.
- Ranking competitivo por ejercicio con filtros global/gimnasio y periodo.
- Posición personal incluida aunque el usuario no esté en el top visible.
- Categorías demográficas operativas por sexo, edad, peso corporal e IMC.
- Reglas aprobadas: sexo `male/female/other`; edad `18–20`, bandas consecutivas de 3 años, tramo final `66–69` y `70+`; peso en bandas de 5 kg; IMC `<18.5`, `18.5–<25`, `25–<30` y `≥30`.
- Staging operativo con 32 migraciones aplicadas y sin migraciones pendientes.

## Pendientes de cierre

- Corregir los datos históricos seed: sus sesiones tienen `gymId=null`, por lo que `scope=gym` todavía devuelve un ranking vacío.
- Repetir la validación E2E y el benchmark con `scope=gym` después de corregir ese dato.

## Evidencia staging — 2026-10-31

- E2E autenticado aprobado con admin web, Sofia y Nico: `scope=global`, ejercicio Hip thrust, ambos usuarios del gimnasio `02000000-0000-0000-0000-000000000001`, posiciones 2 y 7.
- Benchmark aprobado sobre `GET /api/leaderboard/exercises/:exerciseId`: 50/50 respuestas `200`, concurrencia 5, p50 `207.84 ms`, p95 `804.35 ms`, p99 `896.46 ms`, máximo `896.46 ms`.
- La prueba respeta el rate limit de staging mediante lotes de 5 cada 2.6 s; no muta datos.
- La prueba equivalente con `scope=gym` queda bloqueada por el `gymId` nulo de las sesiones históricas seed, no por autenticación ni por falta de sets.

## Criterio de aprobacion

- El sistema debe registrar PRs de forma trazable.
- Los rankings deben poder actualizarse por periodo definido.
- El usuario debe ver su progreso comparado con su historial y con otros usuarios.
- La informacion debe quedar lista para alimentar conquistas en la siguiente etapa.
