# Solicitud De Gimnasio

> Especificacion funcional para que los usuarios puedan proponer gimnasios ausentes del catalogo y
> para que Admin los revise, registre y publique.

## 1. Objetivo

Cuando un usuario no encuentra su gimnasio en OlympX, debe poder solicitar su incorporacion sin
inventar datos ni abandonar el flujo. La solicitud no crea inmediatamente un gimnasio utilizable:
queda pendiente de revision Admin.

El objetivo es mantener la calidad del catalogo y, al mismo tiempo, capturar demanda territorial
real para priorizar nuevos gimnasios.

## 2. Actores

| Actor   | Responsabilidad                                                               |
| ------- | ----------------------------------------------------------------------------- |
| Usuario | Buscar, proponer un gimnasio ausente y consultar el estado de sus solicitudes |
| Admin   | Revisar, validar, aprobar, rechazar o marcar duplicada una solicitud          |
| Sistema | Detectar duplicados, proteger datos, notificar cambios y auditar decisiones   |

## 3. Cuando Aparece La Accion

La accion `Solicitar agregar gimnasio` aparece cuando:

- La busqueda por nombre no entrega resultados relevantes.
- Los resultados de Google Maps contienen un lugar que aun no existe en el catalogo local.
- El usuario pulsa explicitamente `No encuentro mi gimnasio`.

La accion no debe aparecer como alternativa principal si ya existe un gimnasio local activo y
verificado que coincide con la busqueda.

## 4. Flujo De Usuario

```text
Buscar gimnasio
  -> No encuentro mi gimnasio
  -> Completar o revisar datos
  -> Enviar solicitud
  -> Estado pendiente
  -> Admin revisa
  -> Aprobada, rechazada o duplicada
```

### 4.1 Datos Del Formulario

Obligatorios:

- `name`: nombre comercial del gimnasio.
- `address`: direccion o referencia suficiente para ubicarlo.

Opcionales:

- `city`.
- `region`.
- `lat` y `lng` obtenidos de Google Maps o del usuario.
- `googlePlaceId`.
- `chain`.
- `notes`.
- URL publica del lugar.

La app debe mostrar una confirmacion antes de enviar:

> Revisaremos los datos antes de habilitar este gimnasio para seleccion y check-in.

### 4.2 Estados Para El Usuario

| Estado      | Significado                                    | Accion disponible                             |
| ----------- | ---------------------------------------------- | --------------------------------------------- |
| `PENDING`   | Solicitud recibida y aun no revisada           | Ver detalle o cancelar si se habilita         |
| `APPROVED`  | Se creo o vinculo un gimnasio local            | Abrir gimnasio y seleccionarlo                |
| `REJECTED`  | No cumple requisitos o no se pudo validar      | Ver motivo y enviar nueva solicitud corregida |
| `DUPLICATE` | Ya existe una solicitud o gimnasio equivalente | Abrir el gimnasio vinculado                   |

No se debe prometer un tiempo de aprobacion si no existe un SLA operativo.

## 5. Reglas De Negocio

1. Una solicitud no aprobada no puede ser gimnasio principal.
2. Una solicitud no aprobada no puede aceptar check-in.
3. Solo gimnasios locales `isActive = true` y `verificationStatus = VERIFIED` pueden entrar al
   flujo principal.
4. Si existe `googlePlaceId`, se usa como primera clave de duplicado.
5. Si no existe `googlePlaceId`, se compara nombre normalizado, direccion y distancia aproximada.
6. No se crean solicitudes duplicadas abiertas para el mismo usuario y lugar.
7. Admin debe poder vincular una solicitud con un gimnasio existente en lugar de crear otro.
8. La aprobacion debe crear o actualizar el gimnasio y dejarlo pendiente de verificacion si faltan
   datos obligatorios.
9. La decision Admin debe quedar auditada con usuario, fecha, estado anterior, estado nuevo y nota.
10. La ubicacion exacta del usuario que envia la solicitud no se publica.
11. Google Maps sirve para identificar el lugar, no reemplaza la validacion del catalogo OlympX.
12. Una solicitud rechazada no bloquea que el usuario continue entrenando sin gimnasio.

## 6. Contrato API Propuesto

### Usuario

`POST /api/gym-requests`

```json
{
  "name": "OlympX Centro",
  "address": "Av. Central 100",
  "city": "Santiago",
  "region": "RM",
  "lat": -33.4489,
  "lng": -70.6693,
  "googlePlaceId": "ChIJ...",
  "chain": null,
  "notes": "Entrada por calle lateral"
}
```

Respuesta: `201` con la solicitud y estado `PENDING`.

`GET /api/gym-requests/me`

- Devuelve las solicitudes propias, ordenadas por `createdAt desc`.
- Incluye estado, nota de revision, fecha de revision y gimnasio vinculado si existe.

`GET /api/gym-requests/me/:id`

- Devuelve una solicitud propia.
- No permite consultar solicitudes de otros usuarios.

### Admin

`GET /api/admin/gym-requests?status=PENDING`

- Lista paginada para la bandeja de revision.
- Filtros por estado, ciudad, region, fecha y `googlePlaceId`.

`GET /api/admin/gym-requests/:id`

- Devuelve todos los datos de la solicitud y coincidencias sugeridas.

`PATCH /api/admin/gym-requests/:id/approve`

```json
{
  "gymId": null,
  "name": "OlympX Centro",
  "address": "Av. Central 100",
  "lat": -33.4489,
  "lng": -70.6693,
  "verificationStatus": "VERIFIED",
  "reviewNote": "Datos confirmados en sitio oficial"
}
```

- Si `gymId` existe, vincula la solicitud.
- Si `gymId` es `null`, crea un gimnasio nuevo.
- La operacion debe ser idempotente.

`PATCH /api/admin/gym-requests/:id/reject`

```json
{
  "reviewNote": "Direccion insuficiente para validar"
}
```

`PATCH /api/admin/gym-requests/:id/duplicate`

```json
{
  "gymId": "gym-existente",
  "reviewNote": "Coincide con la sede existente"
}
```

## 7. Modelo De Datos Propuesto

Entidad `GymRequest`:

| Campo           | Tipo          | Null | Descripcion                                    |
| --------------- | ------------- | ---- | ---------------------------------------------- |
| `id`            | uuid          | No   | Identificador                                  |
| `requestedById` | uuid          | No   | Usuario solicitante                            |
| `name`          | varchar       | No   | Nombre informado                               |
| `address`       | varchar       | No   | Direccion informada                            |
| `city`          | varchar       | Si   | Ciudad                                         |
| `region`        | varchar       | Si   | Region                                         |
| `lat`           | decimal(10,7) | Si   | Latitud del lugar                              |
| `lng`           | decimal(10,7) | Si   | Longitud del lugar                             |
| `googlePlaceId` | varchar       | Si   | Identificador externo                          |
| `chain`         | varchar       | Si   | Cadena                                         |
| `notes`         | text          | Si   | Contexto aportado por usuario                  |
| `status`        | enum          | No   | `PENDING`, `APPROVED`, `REJECTED`, `DUPLICATE` |
| `reviewNote`    | text          | Si   | Motivo o comentario Admin                      |
| `reviewedById`  | uuid          | Si   | Admin que resolvio                             |
| `resolvedGymId` | uuid          | Si   | Gimnasio creado o vinculado                    |
| `createdAt`     | timestamptz   | No   | Fecha de solicitud                             |
| `updatedAt`     | timestamptz   | No   | Ultima modificacion                            |
| `reviewedAt`    | timestamptz   | Si   | Fecha de resolucion                            |

Indices recomendados:

- `(requestedById, createdAt)`.
- `(status, createdAt)`.
- `googlePlaceId` cuando no sea nulo.
- Coordenadas para apoyar deteccion de coincidencias geograficas.

## 8. Privacidad Y Seguridad

- El usuario solo ve sus propias solicitudes.
- Las coordenadas del lugar solicitado no equivalen a la ubicacion en tiempo real del usuario.
- No se debe publicar automaticamente quien solicito un gimnasio.
- Se deben limitar solicitudes repetitivas por usuario y por lugar.
- Admin debe tener permisos y acciones auditadas.
- La clave de Google Maps permanece solo en backend.
- Los errores al consultar Google no deben impedir una solicitud manual.

## 9. Criterios De Aceptacion

- El usuario puede solicitar un gimnasio ausente desde la busqueda.
- El formulario permite enviar una solicitud manual sin `googlePlaceId`.
- La app puede precargar nombre, direccion y coordenadas desde Google Maps.
- Una solicitud nueva queda en `PENDING`.
- El usuario puede consultar el estado de sus solicitudes.
- Una solicitud aprobada queda vinculada a un gimnasio local.
- Una solicitud duplicada muestra el gimnasio existente.
- Una solicitud rechazada muestra un motivo accionable.
- Las solicitudes pendientes no pueden usarse para check-in ni gimnasio principal.
- Admin puede filtrar y resolver solicitudes.
- Aprobar dos veces no crea gimnasios duplicados.
- Todas las decisiones quedan auditadas.
- Denegar GPS no impide enviar la solicitud manual.

## 10. Alcance Y Prioridad

### Etapa 3 - Documentado

- Modelo funcional.
- Contrato API.
- Estados y reglas.
- Flujo Admin.
- Criterios de aceptacion.

### P1 - Implementar Despues Del Flujo Base

- Persistencia Prisma.
- Endpoints usuario y Admin.
- Formulario mobile.
- Bandeja Admin.
- Notificaciones de cambio de estado.
- Deteccion de duplicados y auditoria.

### Fuera De La Primera Implementacion

- Alta automatica desde Google sin revision.
- Edicion colaborativa por usuarios.
- Reseñas publicas del gimnasio.
- Reservas, membresias o pagos.
- Tracking continuo de ubicacion.

## 11. Documentos Relacionados

- `BaseRequerimientos.md`: RF de catalogo, busqueda y solicitud.
- `ModeloRelacionalMVP.md`: entidad propuesta y relaciones.
- `AdminRequerimientos.md`: bandeja y acciones de revision.
- `etapas/PlanCierreEtapa3.md`: extension documentada de Etapa 3.
- `BenchmarkAppsYFlujoOlympX.md`: riesgo Google Places y priorizacion.
