# OlympX - Avance QA

> Estado actual de pruebas, cobertura y deuda de calidad.

## 1. Objetivo

Tener visibilidad clara de que esta probado hoy, que esta solo preparado y que falta para subir el nivel de confianza del producto.

## 2. Estado General

OlympX tiene una base de testing aun inicial. Hay pruebas smoke/minimas en web, admin y API, pero no existe todavia una estrategia completa de integracion o E2E para el flujo total del producto.

## 3. Cobertura Actual

### API

- Script de test: `vitest run`
- Script de cobertura: `vitest run --coverage`
- Test visible actualmente: smoke del modulo principal (`test/app.test.ts`)
- Typecheck y Prisma sync se usan como validacion adicional de calidad

### Web

- Script de test: `vitest run`
- Script de cobertura: `vitest run --coverage`
- Test visible actualmente: smoke del `App`

### Admin

- Script de test: `vitest run`
- Script de cobertura: `vitest run --coverage`
- Test visible actualmente: smoke del `App`

### Mobile

- Script de test: `jest`
- Script de typecheck: `tsc --noEmit`
- Hoy no se detectan tests committeados en `olympx-mobile`
- La calidad de mobile se valida por typecheck y formato, no por suite automatizada propia

## 4. Cobertura Por Tipo

### Unitaria

- Presente, pero muy basica.
- Cobertura de arranque del proyecto y de render/import smoke.

### Integracion

- No hay suite visible de integracion para API o frontend.
- No hay validacion automatizada de contratos entre mobile y API mas alla del tipado compartido.

### E2E

- No existe suite E2E versionada en el repo hoy.
- No hay Playwright/Cypress visible ni comandos raiz para ejecutarla.

## 5. Validaciones Que Si Se Estan Usando

- `pnpm --filter olympx-api typecheck`
- `pnpm --filter olympx-mobile typecheck`
- `pnpm run format:check`
- `pnpm --filter olympx-api run prisma:generate`
- `pnpm --filter olympx-api run prisma:push`
- `pnpm --filter olympx-api run prisma:seed`

## 6. Riesgos De Calidad

- La cobertura real es baja para un producto con varios flujos de negocio.
- No hay regression suite para login, home, posts, likes y training.
- No existe cobertura cross-browser ni validacion mobile E2E.
- La ausencia de tests en mobile aumenta el riesgo de regresiones de UI o navegación.

## 7. Prioridades De QA

1. Agregar tests de integracion para auth, home y posts en API.
2. Agregar tests de UI para `HomeScreen` y `PostDetailScreen`.
3. Introducir E2E para el flujo login -> home -> post -> training.
4. Medir cobertura y fijar un piso minimo para codigo nuevo.
5. Añadir smoke tests para mobile cuando el stack de pruebas quede definido.

## 8. Criterio De Cierre Del Bloque

Este bloque QA se puede considerar sano cuando:

- API tenga tests de integracion para los endpoints criticos.
- Web y admin tengan coverage util, no solo smoke.
- Mobile tenga al menos tests de pantalla y navegacion basica.
- Exista una suite E2E ejecutable desde el repo raiz.
