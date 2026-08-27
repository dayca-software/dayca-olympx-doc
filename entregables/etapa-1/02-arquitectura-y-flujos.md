# Etapa 1 - Arquitectura Y Flujos

## Arquitectura Definida

| Componente    | Decisión                     |
| ------------- | ---------------------------- |
| API           | NestJS 11                    |
| Persistencia  | PostgreSQL con Prisma        |
| Mobile        | React Native 0.86+           |
| Web y Admin   | React 19, Vite y TailwindCSS |
| Contratos     | `dayca-olympx-contracts`     |
| Autenticación | JWT y `ApiEnvelope<T>`       |

## Dominios Iniciales

- Autenticación y perfiles.
- Gimnasios y ubicación.
- Biblioteca de ejercicios.
- Entrenamiento y progreso.
- Comunidad y competencia como ampliación posterior del alcance Core.

## Principios De Diseño

- El entrenamiento y el progreso son el flujo core.
- Las pantallas deben contemplar estados de carga, vacío y error.
- La navegación debe permitir volver al contexto anterior sin perder datos.
- El diseño debe poder crecer hacia comunidad y competencia sin bloquear el MVP Core.
- Los contratos compartidos evitan duplicar modelos entre API, mobile, web y admin.

## Evidencia Técnica

- [`ModeloRelacionalMVP.md`](../../ModeloRelacionalMVP.md): entidades y relaciones iniciales.
- [`ModeloRelacionalGlobal.md`](../../ModeloRelacionalGlobal.md): modelo global de datos.
- [`MatrizTrazabilidad.md`](../../MatrizTrazabilidad.md): relación entre visión, requisitos y datos.
- [`CLAUDE.md`](../../../CLAUDE.md): stack y estructura operativa del proyecto.

## Pendiente De Cierre

- Unificar los flujos implementados en web, admin y mobile en un prototipo maestro de Figma.
- Registrar la aprobación visual de Producto.
