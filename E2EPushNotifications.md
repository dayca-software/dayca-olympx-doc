# OlympX - Prueba E2E De Notificaciones Push

> Procedimiento manual para validar registro de tokens, envio dirigido, recepcion y navegacion desde una notificacion push.

## 1. Objetivo

Comprobar el flujo completo entre dos usuarios:

```text
Accion social -> API -> PushDevice -> Firebase Admin -> FCM/APNs -> Mobile -> pantalla destino
```

Esta guia cubre likes, comentarios, reacciones y follows.

## 2. Estado

- Implementacion: preparada.
- Ejecucion E2E: pendiente de realizar manualmente.
- Requiere al menos dos sesiones autenticadas y un dispositivo/emulador con Firebase configurado.

## 3. Requisitos

- Node.js 22+.
- Dependencias instaladas con pnpm.
- PostgreSQL disponible.
- Firebase Mobile configurado para `cl.conquest.app`.
- Archivo de credencial Firebase Admin en:

```text
olympx-api/path/to/conquest.json
```

- La credencial no debe commitearse ni enviarse por chat.

## 4. Configuracion

En `olympx-api/.env` debe existir:

```env
GOOGLE_APPLICATION_CREDENTIALS=path/to/conquest.json
```

La ruta es relativa al directorio de trabajo `olympx-api`. La API carga `.env` al arrancar y Firebase Admin usa Application Default Credentials cuando esta variable esta presente.

Antes de iniciar:

```bash
cd olympx-api
pnpm run prisma:generate
pnpm run prisma:push
```

En otra terminal, desde la raiz:

```bash
npm run dev:api
```

En otra terminal para mobile:

```bash
pnpm --filter olympx-mobile start
pnpm --filter olympx-mobile android
```

Para iOS:

```bash
cd ios
pod install
cd ..
pnpm --filter olympx-mobile ios
```

El target iOS debe abrirse desde `ios/olympxmobile.xcworkspace`, no desde el `.xcodeproj`. `pod install` es obligatorio despues de agregar o actualizar Firebase Messaging.

## 5. Preparar Usuarios

Usar dos cuentas distintas:

| Rol | Descripcion |
| --- | --- |
| Usuario A | Receptor de las notificaciones. Debe tener al menos un post. |
| Usuario B | Actor que ejecuta likes, comentarios, reacciones y follow. |

En cada dispositivo:

1. Iniciar sesion con la cuenta correspondiente.
2. Aceptar permisos de notificaciones.
3. Mantener la app abierta unos segundos para registrar el token.
4. Confirmar en Prisma que existe un registro `PushDevice` con `enabled=true`.

Se puede revisar el modelo con:

```bash
cd olympx-api
pnpm exec prisma studio
```

Cada dispositivo debe tener un token distinto. Si una cuenta usa dos dispositivos, ambos deben quedar registrados.

## 6. Casos E2E

### 6.1 Like

1. Usuario A crea o tiene un post.
2. Usuario B abre el post de A.
3. B pulsa like.
4. A debe recibir una notificacion con `type=like`.
5. Al pulsar `Ver`, debe abrirse el detalle del post de A.
6. B quita el like.
7. No debe generarse un segundo push por quitar el like.

Payload esperado:

```json
{
  "type": "like",
  "notificationId": "like-<id>",
  "postId": "<post-id>",
  "actorId": "<user-b-id>"
}
```

### 6.2 Comentario

1. B comenta el post de A.
2. A debe recibir un push con el texto del comentario.
3. Al pulsar `Ver`, debe abrirse el post correspondiente.
4. El comentario debe aparecer en el detalle.

### 6.3 Reaccion

1. B agrega una reaccion fitness al post de A.
2. A debe recibir un push indicando el tipo de reaccion.
3. Al pulsar `Ver`, debe abrirse el post correspondiente.
4. B quita la reaccion.
5. Quitarla no debe generar push.

### 6.4 Follow

1. B entra al perfil publico de A.
2. B pulsa seguir.
3. A debe recibir un push de nuevo seguidor.
4. Al pulsar `Ver`, debe abrirse el perfil publico de B.
5. B deja de seguir.
6. Dejar de seguir no debe generar push.

Payload esperado:

```json
{
  "type": "follow",
  "notificationId": "follow-<id>",
  "actorId": "<user-b-id>"
}
```

## 7. Estados Mobile

Repetir cada caso, al menos una vez, en estos estados:

| Estado | Resultado esperado |
| --- | --- |
| App en foreground | Aparece alerta con acciones `Cerrar` y `Ver`. |
| App en background | El sistema muestra la notificacion. `Ver` abre el destino. |
| App terminada | El sistema muestra la notificacion. Al abrirla se navega al destino. |

## 8. Validaciones Adicionales

- Un usuario no debe recibir push por su propia accion sobre su propio contenido.
- Todos los dispositivos activos del receptor deben recibir el push.
- Un token invalido debe quedar `enabled=false` en `PushDevice`.
- Un error de Firebase no debe devolver error 5xx en la accion social.
- La notificacion in-app de `GET /api/notifications` debe seguir apareciendo aunque el push falle.
- Al cerrar sesion, el token del dispositivo debe desactivarse.

## 9. Diagnostico

### No existe `PushDevice`

- Revisar permisos del sistema.
- Revisar `google-services.json` o `GoogleService-Info.plist`.
- Confirmar que mobile usa la API correcta y que la sesion esta autenticada.
- Reiniciar la app despues de conceder permisos.

### Existe token, pero no llega el push

- Confirmar que la API fue reiniciada despues de modificar `.env`.
- Confirmar la ruta `path/to/conquest.json` desde `olympx-api`.
- Confirmar que la credencial pertenece al proyecto Firebase de la app.
- Revisar logs de `PushNotificationService`.
- Confirmar que el token sigue `enabled=true`.

### Llega el push, pero no navega

- Revisar `postId` para likes, comentarios y reacciones.
- Revisar `actorId` para follows.
- Confirmar que la app esta autenticada al procesar el evento.
- Confirmar que `NavigationContainer` esta listo.

### Android no muestra la notificacion

- Confirmar permiso de notificaciones en Android 13+.
- Confirmar que la app y el JSON Firebase usan `cl.conquest.app`.
- Probar con la app en background, no solo foreground.

### iOS no muestra la notificacion

- Confirmar que `Podfile.lock` contiene Firebase y RNFB Messaging.
- Confirmar que `pod install` termino correctamente y que se abre el workspace.
- Confirmar permisos de alert, badge y sonido.
- Confirmar capability Push Notifications y Background Modes.
- Confirmar APNs configurado en Firebase.
- Reinstalar pods si la configuracion nativa cambio.

## 10. Criterios De Aceptacion

- [ ] Los dos usuarios registran token correctamente.
- [ ] Like entrega push al propietario del post.
- [ ] Comentario entrega push al propietario del post.
- [ ] Reaccion entrega push al propietario del post.
- [ ] Follow entrega push al usuario seguido.
- [ ] No se envian pushes por unlike, quitar reaccion o unfollow.
- [ ] Foreground muestra alerta y permite navegar.
- [ ] Background navega al destino correcto.
- [ ] App terminada navega al destino correcto.
- [ ] Build iOS usa `aps-environment=development` en Debug y `production` en Release.
- [ ] Tokens invalidos se desactivan.
- [ ] La accion social continua funcionando si Firebase falla.
- [ ] La credencial no aparece en Git ni en logs.

## 11. Pruebas iOS Pendientes

La build de simulador valida compilacion, pero no sustituye la validacion de APNs en hardware real.

- [ ] Ejecutar en iPhone fisico con build Debug y `aps-environment=development`.
- [ ] Confirmar permiso de alert, sonido y badge.
- [ ] Confirmar registro del token APNs/FCM en `PushDevice`.
- [ ] Probar push con app en foreground.
- [ ] Probar push con app en background.
- [ ] Probar push con app terminada.
- [ ] Confirmar apertura de `PostDetail` para like, comentario y reaccion.
- [ ] Confirmar apertura de `PublicProfile` para follow.
- [ ] Ejecutar build Release/TestFlight con `aps-environment=production`.
- [ ] Repetir al menos un caso desde TestFlight.

## 12. Registro De Ejecucion

Completar despues de ejecutar la prueba:

| Campo | Valor |
| --- | --- |
| Fecha | Pendiente |
| Version/commit | Pendiente |
| Dispositivo Android | Pendiente |
| Dispositivo iOS | Pendiente |
| Usuario A | Pendiente |
| Usuario B | Pendiente |
| Resultado | Pendiente |
| Incidencias | Pendiente |
