# Etapa 3 - Checklist Gimnasios, GPS y Biblioteca

> Criterio minimo para considerar cerrada la Etapa 3.

> Plan operativo: [`PlanCierreEtapa3.md`](./PlanCierreEtapa3.md).

## Entregables esperados

- Seleccion de gimnasio principal.
- Check-in por GPS al llegar al recinto.
- Catalogo de ejercicios con metadatos.
- API de ejercicios con filtros.

## Cobertura implementada

- Catalogo de gimnasios disponible.
- Busqueda de gimnasios cercanos disponible.
- Actualizacion de ubicacion del usuario activa.
- Biblioteca de ejercicios con filtros y detalle disponible.
- Check-in formal con validacion de radio de 100 metros disponible.
- Bloqueo de check-in duplicado durante 30 minutos disponible.
- Check-in transaccional con actualizacion de gimnasio principal disponible.
- Estados de gimnasio inactivo, no verificado y sin coordenadas representados en el detalle.
- Actividad local limitada a 7 dias y usuarios publicos disponible.
- Apertura de mapas mediante deep link disponible.

## Evidencia automatizada

- API: 34 archivos y 228 tests pasando; typecheck y build pasando.
- Mobile: 9 suites y 21 tests pasando; typecheck y lint sin errores.
- Contracts: build pasando.
- Android: build, instalacion y lanzamiento verificados en emulador Pixel 10.
- iOS: build, instalacion y lanzamiento verificados en simulador iPhone 17 Pro.

## Pendientes de cierre

- Ejecutar smoke E2E del flujo completo en iOS y Android.
- Validar en dispositivo estados de permiso GPS denegado y ubicacion no disponible.
- Validar en dispositivo gimnasio inactivo, no verificado y sin coordenadas desde la interfaz.
- Confirmar en dispositivo la apertura de mapas y el flujo completo de check-in.

## Extension fuera del cierre

- `GymRequest` para solicitar gimnasios ausentes queda documentado en el plan de cierre y se
  implementará después de validar el flujo de búsqueda, selección y check-in de gimnasios existentes.

## Criterio de aprobacion

- El usuario debe poder elegir y guardar un gimnasio principal.
- El GPS debe soportar busqueda y contexto local sin tracking continuo.
- La biblioteca de ejercicios debe poder filtrarse y recorrerse con fluidez.
- Debe existir consistencia entre API, mobile y Figma para estos flujos.
