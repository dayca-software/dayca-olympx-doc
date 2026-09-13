# OlympX - Validaciones Reales E Integraciones

> Registro operativo del punto 4 del plan de cierre. Separa comprobaciones locales reproducibles de
> validaciones que requieren dispositivos, cuentas externas o credenciales que no deben commitearse.

## Estado Actual

| Area                   | Estado                | Evidencia                                                                                         |
| ---------------------- | --------------------- | ------------------------------------------------------------------------------------------------- |
| Push lifecycle mobile  | Automatizado          | `pushNotifications.test.ts` cubre permisos, token, refresh, foreground, opened, initial y cleanup |
| Cola offline           | Automatizado          | `offlineQueue.test.ts` cubre payload de training, `scope` e `Idempotency-Key`                     |
| Android nativo         | Validado              | `./gradlew assembleDebug` exitoso con Firebase Messaging y RevenueCat autolinked                  |
| iOS nativo             | Validado en simulador | `xcodebuild` exitoso para simulador arm64 con Firebase Messaging y RevenueCat                     |
| Push FCM/APNs real     | Pendiente             | Requiere dos usuarios, Firebase Admin y dispositivo con permisos                                  |
| RevenueCat Test Store  | Pendiente             | Requiere claves publicas, productos y entitlement configurados                                    |
| Offline en dispositivo | Pendiente             | Requiere ejecutar perdida/restauracion de red en Android e iOS                                    |

## Validaciones Automatizadas

Desde `olympx-mobile`:

```bash
npm test
npm run typecheck
npm run lint -- --quiet
```

Desde `olympx-mobile/android`:

```bash
./gradlew assembleDebug
```

Para iOS, abrir siempre el workspace despues de instalar Pods:

```bash
cd ios
pod install
open olympxmobile.xcworkspace
```

## Push Real

Requisitos:

- `GOOGLE_APPLICATION_CREDENTIALS` configurado en `olympx-api/.env`.
- `google-services.json` y `GoogleService-Info.plist` del proyecto correcto.
- Dos cuentas de prueba y dos dispositivos con `cl.conquest.app` instalado.
- Permisos de notificaciones concedidos.

Ejecutar API y mobile:

```bash
npm run dev:api
cd olympx-mobile
npm start
npm run android
```

Ejecutar la guia existente:

```bash
maestro test .maestro/community-smoke.yaml
```

Despues validar los casos de `doc/E2EPushNotifications.md` en foreground, background y app
terminada. La app debe dejar un `PushDevice` activo por dispositivo y desactivar tokens invalidos.

## RevenueCat Test Store

Requisitos:

- `REVENUECAT_ANDROID_API_KEY` y `REVENUECAT_IOS_API_KEY` publicas en el `.env` local de mobile.
- Producto mensual configurado en RevenueCat y en las tiendas de prueba.
- El `billing.productId` del plan API debe coincidir con el identificador del producto RevenueCat.
- Entitlement premium configurado y asociado al producto.

Casos mínimos:

1. Abrir `Paywall` y confirmar que aparece el plan activo.
2. Comprar el producto Test Store y confirmar `tier=PAID` en `/api/subscriptions/me`.
3. Cerrar sesión, iniciar con la misma cuenta y ejecutar `Restaurar compra`.
4. Confirmar que el entitlement restaurado mantiene acceso premium.
5. Simular expiración/cancelación y confirmar pérdida de acceso según el webhook.

No se deben marcar estos casos como ejecutados solo porque la app compile o el paywall renderice.

## Offline En Dispositivo

Para entrenamiento:

1. Iniciar una sesión con conexión.
2. Cortar la red antes de guardar la sesión.
3. Confirmar el mensaje de guardado local y que no se pierde `focusAreas`.
4. Restaurar red y volver a foreground.
5. Confirmar una sola sesión creada en API usando el `Idempotency-Key`.
6. Repetir el caso con una respuesta HTTP `422` y confirmar que no queda en cola.

Para posts y ubicación, repetir el flujo usando sus claves de coalescencia y scopes de usuario.

## Criterio De Cierre

- [ ] Push validado en Android foreground/background/terminated.
- [ ] Push validado en iOS físico foreground/background/terminated.
- [ ] Compra Test Store validada en Android.
- [ ] Compra/restauración validada en iOS.
- [ ] Expiración y cancelación reflejadas en acceso premium.
- [ ] Offline training validado en Android y iOS.
- [x] Build nativa Android reproducible.
- [x] Build nativa iOS de simulador reproducible.
