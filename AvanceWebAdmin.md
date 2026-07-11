# OlympX Web y Admin - Avance Actual

> Estado tecnico y funcional de `olympx-web` y `olympx-admin` al dia de hoy.

## 1. Objetivo

Documentar el estado real de las apps web publicas y admin para dejar claro que ya esta implementado, que esta preparado y que sigue siendo pendiente.

## 2. Estado General

Las dos apps web existen, compilan y estan conectadas al contrato compartido `dayca-olympx-contracts`.

Hoy el avance es funcional pero aun minimo:

- Web publica: login, ruta protegida y home basico.
- Admin: login, ruta protegida y dashboard basico.
- Ambas consumen auth contra la API.
- Ambas usan Zustand para estado de sesion.

## 3. Cobertura Actual

### Web Publica

- `LoginPage` con autenticacion contra `POST /api/auth/login`.
- `ProtectedRoute` para bloquear acceso sin token.
- `HomePage` con saludo basico desde el usuario autenticado.
- Estructura lista para crecer hacia dashboard publico.

### Admin

- `LoginPage` con autenticacion contra `POST /api/auth/login`.
- `ProtectedRoute` para bloquear acceso sin token.
- `Dashboard` basico como punto de entrada del panel.
- Estructura lista para crecer hacia moderacion y control interno.

## 4. Integracion Con API

Ambas apps ya dependen del backend para autenticar y obtener usuario:

- `POST /api/auth/login`
- `GET /api/auth/me` o `GET /api/users/me` segun flujo interno

El transporte usa `axios` y los tipos compartidos para `ApiEnvelope<LoginResponse>`.

## 5. Estado De UI

### Web

- Visual simple, oscuro, sin sistema de componentes complejo.
- Layout inicial centrado en login y home.
- Aun no hay componentes de producto ricos ni navegación amplia.

### Admin

- Visual simple, oscuro, muy base.
- Solo cubre login y pantalla de dashboard placeholder.
- Falta la estructura real de panel operacional.

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

- Las dos apps estan demasiado cerca de un scaffold y aun no representan el producto final.
- Falta una experiencia de dashboard real para web y admin.
- No hay tests funcionales que cubran login o rutas protegidas.
- No existe una capa de diseño compartida entre ambas apps.

## 10. Pendientes Priorizados

1. Definir el contenido real del dashboard web publico.
2. Construir el panel admin con modulos operativos.
3. Extraer componentes y layout compartidos.
4. Agregar pruebas de routing y auth.
5. Alinear visualmente ambas apps con una guia de UI consistente.

## 11. Criterio De Cierre Del Bloque

Este bloque se puede considerar estable cuando:

- Login y rutas protegidas funcionan consistentemente.
- Web publica tenga contenido real de producto.
- Admin tenga modulos funcionales, no solo placeholder.
- Existan tests que cubran auth y navegacion basica.
