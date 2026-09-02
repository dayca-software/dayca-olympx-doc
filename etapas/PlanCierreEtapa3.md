# Plan De Cierre - Etapa 3

## Gimnasios, GPS Y Biblioteca De Ejercicios

> Plan operativo para cerrar la Etapa 3 sin ampliar el alcance del MVP.

## 1. Estado De Partida

La etapa tiene una cobertura funcional alta:

- Catálogo de gimnasios y búsqueda cercana implementados.
- Actualización de ubicación del usuario implementada.
- Biblioteca de ejercicios con filtros y detalle implementada.
- Endpoint de check-in por gimnasio implementado.
- Validación de radio de 100 metros implementada.
- Bloqueo de check-ins duplicados durante 30 minutos implementado.
- Selección de gimnasio principal implementada en el detalle.

El cierre formal requiere demostrar que esos flujos funcionan juntos desde la experiencia mobile y
que los estados alternos están cubiertos.

## 2. Objetivo De Cierre

Permitir que un usuario pueda:

1. Encontrar un gimnasio por GPS o búsqueda manual.
2. Abrir su detalle y revisar información básica.
3. Guardarlo como gimnasio principal.
4. Registrar un check-in únicamente si está dentro del radio permitido.
5. Recibir un estado claro cuando el gimnasio no está disponible, el GPS falla o existe un duplicado.
6. Buscar y seleccionar ejercicios para continuar hacia el flujo de entrenamiento.

## 3. Alcance De Cierre

### Must Have

- Gimnasio principal persistido y visible en la interfaz.
- Búsqueda cercana con radio configurable.
- Búsqueda manual de gimnasios.
- Check-in únicamente para gimnasios activos y verificados.
- Validación de coordenadas y radio de 100 metros.
- Bloqueo de duplicado reciente.
- Permiso GPS denegado, ubicación no disponible y error de red con mensajes útiles.
- Detalle de gimnasio con acciones de principal y check-in.
- Biblioteca de ejercicios con búsqueda, filtros y detalle.
- Pruebas API y smoke mobile del flujo completo.

### Should Have

- Abrir la ubicación del gimnasio en la aplicación de mapas del dispositivo.
- Mostrar actividad local reciente sin exponer cuentas Admin, suspendidas o datos innecesarios.
- Mostrar fecha y estado del último check-in del usuario.

### Fuera De Este Cierre

- Tracking continuo de ubicación.
- Heatmaps.
- Usuarios cercanos en tiempo real.
- Navegación indoor.
- Integraciones completas con Google Places como requisito obligatorio.
- Check-out o permanencia dentro del gimnasio.

### Extension Documentada: GymRequest

La solicitud de un gimnasio que no aparece en el catálogo queda documentada como extensión de esta
etapa, pero no bloquea su cierre funcional. El flujo previsto es:

1. El usuario busca por nombre o ubicación y no encuentra el gimnasio.
2. La app ofrece solicitarlo indicando nombre, dirección y referencia opcional de Google Maps.
3. La API registra la solicitud con estado `PENDING` y evita duplicados abiertos para el mismo lugar.
4. Admin revisa la solicitud, la aprueba creando o vinculando un gimnasio, o la rechaza indicando el
   motivo.
5. La app informa al usuario el estado de la solicitud.

Contrato mínimo pendiente de implementar:

- `POST /api/gym-requests` para crear la solicitud autenticada.
- `GET /api/gym-requests/me` para consultar solicitudes propias.
- Estados: `PENDING`, `APPROVED`, `REJECTED`, `DUPLICATE`.
- Campos mínimos: `name`, `address`, `city`, `region`, `lat`, `lng`, `googlePlaceId`, `notes` y
  `status`.
- Permisos Admin para revisar y resolver solicitudes.

Mientras esta extensión no esté implementada, la búsqueda manual y cercana solo debe permitir
seleccionar gimnasios existentes y activos/verificados para el flujo de check-in.

## 4. Plan De Trabajo

### Paso 1 - Cerrar Reglas De Negocio

**Estimación:** 2-3 h

- Confirmar radio por defecto de 100 metros.
- Confirmar cooldown de duplicado de 30 minutos.
- Confirmar que solo gimnasios `isActive = true` y `verificationStatus = VERIFIED` aceptan check-in.
- Confirmar que el check-in actualiza el gimnasio principal.
- Confirmar que el GPS se usa de forma puntual y no como tracking continuo.

**Salida:** reglas aprobadas y sin ambigüedad para QA.

### Paso 2 - Endurecer Y Verificar API

**Estimación:** 6-8 h

- Revisar filtros de `GET /api/gyms/nearby` para no priorizar gimnasios inactivos o no verificados.
- Validar latitud, longitud, radio y accuracy cuando corresponda.
- Mantener la política de 100 metros en `POST /api/gyms/:id/check-in`.
- Cubrir gimnasio inexistente, inactivo, pendiente de verificación y sin coordenadas.
- Cubrir check-in fuera de radio y duplicado reciente.
- Confirmar que el límite comercial se evalúa antes de crear el check-in.
- Revisar que la actividad pública excluya usuarios no públicos.

**Salida:** contrato API estable y errores funcionales documentados.

### Paso 3 - Cerrar Flujo Mobile

**Estimación:** 8-12 h

- Desde resultados cercanos, abrir detalle de gimnasio.
- Desde búsqueda manual, abrir detalle de gimnasio.
- Mostrar correctamente si es el gimnasio principal actual.
- Permitir seleccionar y persistir el gimnasio principal.
- Ejecutar check-in con lectura puntual de GPS.
- Mostrar éxito con hora del check-in.
- Mostrar mensajes accionables para permiso denegado, fuera de radio, duplicado y gimnasio no disponible.
- Agregar acceso a mapas mediante deep link si se confirma como `Should Have`.
- Revisar loading, empty, error y retry en búsqueda, detalle y check-in.

**Salida:** flujo mobile completo sin navegación muerta ni acciones ambiguas.

### Paso 4 - Validar Biblioteca De Ejercicios

**Estimación:** 3-4 h

- Verificar carga del catálogo.
- Verificar filtros por nombre y grupo muscular.
- Verificar detalle de ejercicio.
- Verificar estado vacío y error de red.
- Confirmar que un ejercicio puede seleccionarse desde el flujo de rutina o entrenamiento.

**Salida:** biblioteca lista para entregar el contexto a la Etapa 4.

### Paso 5 - Pruebas Y Evidencia

**Estimación:** 5-7 h

- Ampliar pruebas API de check-in y gimnasios.
- Crear smoke Maestro iOS para gimnasio principal y check-in.
- Crear smoke Maestro Android para gimnasio principal y check-in.
- Validar permiso GPS denegado.
- Validar check-in dentro y fuera de radio.
- Validar duplicado reciente.
- Validar gimnasio inactivo o pendiente.
- Validar navegación gimnasio -> ejercicio -> entrenamiento.
- Registrar resultado, dispositivo, fecha y evidencia de cada flujo.

**Salida:** evidencia reproducible para aprobar la etapa.

### Paso 6 - Documentación Y Aprobación

**Estimación:** 2-3 h

- Actualizar `Etapa3Checklist.md`.
- Actualizar `Etapa3Cliente.md`.
- Actualizar `AvanceEtapas.md`.
- Registrar decisiones de radio, cooldown y mapas.
- Obtener aprobación de Producto/Delivery.

**Salida:** Etapa 3 marcada como completada o con pendientes explícitos de fase posterior.

## 5. Estimación Consolidada

| Bloque                       |       Horas |
| ---------------------------- | ----------: |
| Reglas de negocio            |       2-3 h |
| API                          |       6-8 h |
| Mobile                       |      8-12 h |
| Biblioteca de ejercicios     |       3-4 h |
| QA y evidencia               |       5-7 h |
| Documentación y aprobación   |       2-3 h |
| **Total estimado de cierre** | **26-37 h** |

La estimación puede bajar a 24-32 horas si se mantiene el modelo actual, se excluyen mapas del
Must Have y no aparecen cambios de esquema.

## 6. Orden Recomendado De Ejecución

```text
Reglas aprobadas
      |
      v
API endurecida y probada
      |
      v
Flujo mobile principal + check-in
      |
      v
Biblioteca de ejercicios
      |
      v
Smoke iOS + Android
      |
      v
Documentación y aprobación
```

No conviene avanzar a validaciones mobile finales mientras las reglas de radio, disponibilidad y
duplicado no estén cerradas en API.

## 7. Casos De Aceptación

### Flujo Feliz

- Dado un usuario autenticado y un gimnasio activo/verificado, cuando abre el detalle y está dentro
  de 100 metros, entonces el check-in se crea y el gimnasio queda como principal.

### Fuera De Radio

- Dado un gimnasio válido, cuando la distancia supera 100 metros, entonces no se crea el check-in y
  se informa la distancia o el límite requerido.

### Duplicado

- Dado un check-in creado en los últimos 30 minutos, cuando el usuario intenta repetirlo, entonces la
  API responde conflicto y la app mantiene el estado anterior.

### Gimnasio No Disponible

- Dado un gimnasio inactivo, pendiente de verificación o sin coordenadas, cuando el usuario intenta
  hacer check-in, entonces la API rechaza la operación con un mensaje accionable.

### GPS Denegado

- Dado que el usuario rechaza el permiso de ubicación, cuando intenta buscar o hacer check-in,
  entonces la app permite reintentar o continuar por búsqueda manual sin romper la navegación.

### Biblioteca

- Dado un catálogo disponible, cuando el usuario busca y filtra ejercicios, entonces puede abrir el
  detalle y continuar hacia una rutina o sesión.

## 8. Definition Of Done

- [ ] Reglas de radio, cooldown y disponibilidad aprobadas.
- [ ] `nearby` no expone gimnasios no utilizables para el flujo principal.
- [ ] Check-in exitoso validado dentro de 100 metros.
- [ ] Check-in fuera de radio rechazado.
- [ ] Check-in duplicado rechazado.
- [ ] Gimnasio principal persistido y visible.
- [ ] GPS denegado y ubicación no disponible tienen salida útil.
- [ ] Búsqueda manual y detalle funcionan.
- [ ] Biblioteca y filtros funcionan.
- [ ] Smoke iOS ejecutado y registrado.
- [ ] Smoke Android ejecutado y registrado.
- [ ] Tests API en verde.
- [ ] Checklist y resumen para cliente actualizados.
- [ ] Aprobación de Producto/Delivery registrada.

## 9. Archivos Relacionados

- `Etapa3Cliente.md`: resumen para cliente.
- `Etapa3Checklist.md`: checklist de cierre.
- `AvanceEtapas.md`: avance global por etapa.
- `../../olympx-api/src/modules/gyms/gyms.controller.ts`: endpoints y reglas de check-in.
- `../../olympx-api/src/modules/gyms/gyms.controller.spec.ts`: pruebas actuales de check-in.
- `../ModeloRelacionalActual.md`: modelo real de `Gym` y `GymCheckIn`.
