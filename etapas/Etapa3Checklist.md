# Etapa 3 - Checklist Gimnasios, GPS y Biblioteca

> Criterio minimo para considerar cerrada la Etapa 3.

> Plan operativo: [`PlanCierreEtapa3.md`](./PlanCierreEtapa3.md).

## Entregables esperados

- Seleccion de gimnasio principal.
- Check-in por GPS al llegar al recinto.
- Catalogo de ejercicios con metadatos.
- API de ejercicios con filtros.

## Cobertura actual

- Catalogo de gimnasios disponible.
- Busqueda de gimnasios cercanos disponible.
- Actualizacion de ubicacion del usuario activa.
- Biblioteca de ejercicios con filtros y detalle disponible.
- Check-in formal con validación de radio de 100 metros disponible.
- Bloqueo de check-in duplicado reciente disponible.
- Selección y persistencia de gimnasio principal disponible.

## Pendientes de cierre

- Ejecutar smoke E2E del flujo completo en iOS y Android.
- Validar estados de permiso GPS denegado y ubicación no disponible.
- Validar gimnasio inactivo, no verificado y sin coordenadas desde la interfaz.
- Actividad del gym con contexto local y usuarios públicos.
- Confirmar apertura de mapas si se mantiene dentro del alcance.

## Extension fuera del cierre

- `GymRequest` para solicitar gimnasios ausentes queda documentado en el plan de cierre y se
  implementará después de validar el flujo de búsqueda, selección y check-in de gimnasios existentes.

## Criterio de aprobacion

- El usuario debe poder elegir y guardar un gimnasio principal.
- El GPS debe soportar busqueda y contexto local sin tracking continuo.
- La biblioteca de ejercicios debe poder filtrarse y recorrerse con fluidez.
- Debe existir consistencia entre API, mobile y Figma para estos flujos.
