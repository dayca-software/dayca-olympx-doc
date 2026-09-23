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

## Pendientes de cierre

- Categorias por sexo/edad/peso/IMC.
- Validación E2E y de rendimiento con datos reales.
- Aplicación de la migración en staging.

## Criterio de aprobacion

- El sistema debe registrar PRs de forma trazable.
- Los rankings deben poder actualizarse por periodo definido.
- El usuario debe ver su progreso comparado con su historial y con otros usuarios.
- La informacion debe quedar lista para alimentar conquistas en la siguiente etapa.
