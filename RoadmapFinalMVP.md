# OlympX MVP 2026 - Roadmap Final

> Ruta corta para convertir la base actual en un MVP publicable y medible.

## Fase 1 - Cierre Funcional

Objetivo: asegurar que el producto principal ya no tenga huecos de flujo.

- Login y registro.
- Home con feed, gimnasios y entrenos.
- Training con create, detail e historial.
- Search, leaderboard y notifications.
- Perfil editable y suscripcion basica.

## Fase 2 - Hardening

Objetivo: reducir deuda antes de pedir feedback externo.

- Cola de acciones offline para operaciones de escritura.
- Manejo de errores y estados vacios.
- Type safety mas estricto en Prisma y contracts.
- Smoke tests para auth, home, search y training.

## Fase 3 - Preparacion Comercial

Objetivo: dejar lista la capa paga sin tocar el core.

- Separar mejor Free, Trial y Paid.
- Refinar paywall y beneficios premium.
- Ajustar RevenueCat si cambia el catalogo.
- Definir metricas de activacion y conversion.

## Fase 4 - Validacion Con Usuarios

Objetivo: aprender con menos riesgo.

- Cerrar una beta pequena.
- Medir uso del home y del flujo de training.
- Revisar friccion de onboarding.
- Priorizar mejoras reales por evidencia.

## Criterio De Progreso

No avanzar de fase si:

- Rompe el flujo principal de entrenamiento.
- Introduce mas friccion en mobile.
- Agrega monetizacion antes de validar uso.
