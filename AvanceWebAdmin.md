# OlympX Web y Admin - Avance Actual

> Estado tecnico y funcional de `olympx-web` y `olympx-admin` al dia de hoy.

## 1. Objetivo

Documentar el estado real de las apps web publicas y admin para dejar claro que ya esta implementado, que esta preparado y que sigue siendo pendiente.

## 2. Estado General

Las dos apps web existen, compilan y estan conectadas al contrato compartido `dayca-olympx-contracts`.

Hoy el avance cubre los principales modulos operativos y comerciales:

- Web publica: login, ruta protegida y home basico.
- Admin: login, dashboard operativo, usuarios, gimnasios, moderacion, catalogos y comercial.
- Ambas consumen auth contra la API.
- Ambas usan Zustand para estado de sesion.

## 3. Cobertura Actual

### Web Publica

- `LoginPage` con autenticacion contra `POST /api/auth/login`.
- `ProtectedRoute` para bloquear acceso sin token.
- `HomePage` con saludo basico desde el usuario autenticado.
- Estructura lista para crecer hacia dashboard publico.

### Admin

- `LoginPage` con autenticacion contra `POST /api/auth/login/admin`.
- `ProtectedRoute` y `AdminRoute` para bloquear acceso sin token o rol admin.
- Dashboard operativo con metricas, alertas y health.
- Gestion de usuarios, gimnasios, reportes, planes, suscripciones y cupones.
- Catalogo de ejercicios y rangos de fuerza con acciones de publicacion.
- Las acciones de rangos de fuerza ya generan registros en `AuditLog`.

## 4. Integracion Con API

Ambas apps ya dependen del backend para autenticar y obtener usuario:

- `POST /api/auth/login`
- `POST /api/auth/login/admin` para Admin
- `GET /api/auth/me` o `GET /api/users/me` segun flujo interno

El transporte usa `axios` y los tipos compartidos para `ApiEnvelope<LoginResponse>`.

El Admin tambien consume dominios operativos y comerciales mediante `privateHttp`, incluyendo dashboard, usuarios, gimnasios, reportes, planes, suscripciones, catalogo de ejercicios y rangos de fuerza.

## 5. Estado De UI

### Web

- Visual simple, oscuro, sin sistema de componentes complejo.
- Layout inicial centrado en login y home.
- Aun no hay componentes de producto ricos ni navegación amplia.

### Admin

- Visual simple, oscuro, muy base.
- La estructura operacional ya esta modularizada por dominio.
- Falta completar cobertura E2E y validacion manual de operaciones criticas.

## 6. Contratos Compartidos Usados

- `ApiEnvelope`
- `LoginResponse`

## 7. Test Y Calidad

- Web tiene un smoke test de `App`.
- Admin tiene un smoke test de `App`.
- Ambas apps tienen `typecheck` y `vitest` configurados.
- No hay suite de integracion ni E2E para web/admin hoy.

## 8. Decisiones Tecnicas

- Se mantuvo una base minima para no frenar el avance del core mobile/API.
- Se reutilizo el contrato compartido para evitar duplicar login y tipos.
- Se opto por shells simples que validan autenticacion y routing antes de expandir UI.

## 9. Riesgos Y Deuda Actual

- Web publica sigue cerca de un scaffold y aun no representa el producto final.
- Admin ya tiene dashboard y modulos operativos, pero falta validacion E2E.
- No existe una suite E2E compartida para login, roles y acciones criticas.
- No existe una capa de diseño compartida entre ambas apps.

## 10. Pendientes Priorizados

1. Definir el contenido real del dashboard web publico.
2. Completar cobertura funcional del panel admin en los flujos restantes.
3. Construir consulta centralizada del historial de auditoria.
4. Extraer componentes y layout compartidos.
5. Agregar pruebas E2E de routing, auth y acciones criticas.
6. Alinear visualmente ambas apps con una guia de UI consistente.

## 11. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y rutas protegidas funcionan consistentemente.
- Web publica tenga contenido real de producto.
- Admin tenga modulos funcionales, no solo placeholder.
- Existan tests que cubran auth y navegacion basica.
