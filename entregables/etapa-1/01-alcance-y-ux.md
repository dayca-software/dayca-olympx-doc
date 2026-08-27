# Etapa 1 - Alcance Y UX/UI

## Objetivo

Definir el producto inicial, sus prioridades y la experiencia mínima que permite recorrer el flujo
core de OlympX: registro, configuración de perfil, selección de gimnasio, entrenamiento y consulta
de progreso.

## Alcance De La Etapa

- Discovery y definición de prioridades.
- Especificación funcional del MVP Core.
- Identificación de actores, módulos y dependencias.
- Diseño de los flujos principales.
- Definición de estados de interfaz y casos vacíos o de error.

## Pantallas Clave

- Splash.
- Login y registro.
- Completar perfil.
- Home.
- Gimnasios cercanos y detalle de gimnasio.
- Biblioteca y detalle de ejercicio.
- Registrar entrenamiento.
- Historial de entrenamientos.
- Perfil.

## Flujos Mínimos

```text
Login ------------------------------> Home
Registro -> Completar perfil -------> Home
Home ----> Gimnasios ---------------> Detalle de gimnasio
Home ----> Entrenamiento -----------> Guardar sesión
Home ----> Biblioteca --------------> Detalle de ejercicio
Home ----> Perfil
```

## Estados De Interfaz

- Loading.
- Empty.
- Error.
- GPS denegado.
- Sin resultados.
- Sesión expirada.

## Evidencia Y Fuentes

- [`BaseRequerimientos.md`](../../BaseRequerimientos.md): requisitos funcionales y reglas.
- [`AnexoMVP.md`](../../AnexoMVP.md): alcance y entregables cotizados.
- [`Etapa1Checklist.md`](../../etapas/Etapa1Checklist.md): checklist de pantallas y estados.
- [`Etapa1Cliente.md`](../../etapas/Etapa1Cliente.md): resumen de entrega para cliente.

## Estado

La definición funcional y la arquitectura base están cubiertas. La etapa continúa parcial hasta
consolidar el prototipo navegable en Figma como artefacto único de aprobación.
