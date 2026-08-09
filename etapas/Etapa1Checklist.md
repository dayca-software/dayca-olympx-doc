# Etapa 1 - Checklist Figma

> Criterio minimo para dar por aprobada la etapa de Discovery, Planificacion y UX/UI.

## Pantallas

- Splash
- Login
- Registro
- Completar perfil
- Home
- Gimnasios cercanos
- Detalle de gimnasio
- Biblioteca de ejercicios
- Detalle de ejercicio
- Registrar entrenamiento
- Historial de entrenos
- Perfil

## Estados

- Loading
- Empty
- Error
- GPS denegado
- Sin resultados
- Sesion expirada

## Flujos

- Login -> Home
- Registro -> Completar perfil -> Home
- Home -> Gimnasios -> Detalle
- Home -> Entrenamiento -> Guardar
- Home -> Perfil
- Home -> Biblioteca -> Detalle

## Criterio de aprobacion

- Cada flujo debe poder recorrerse completo.
- Cada pantalla debe tener estado normal.
- Las pantallas que dependen de datos deben tener loading, empty y error.
- No incluir social, rankings ni conquistas en esta etapa.

## Estado actual

- Etapa 1 sigue en progreso por el Figma/prototipo navegable.
- La documentacion funcional y la arquitectura ya estan alineadas.
