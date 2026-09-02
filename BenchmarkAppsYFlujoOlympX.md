# Benchmark De Apps Y Flujo OlympX

> Investigación de producto y UX para orientar la evolución del MVP. Revisión realizada el
> 2026-09-01 sobre páginas oficiales y el flujo actualmente implementado en OlympX.

## 1. Conclusión Ejecutiva

OlympX no debe posicionarse como otra aplicación para contar series. La oportunidad está en unir:

1. Registro de fuerza rápido y confiable.
2. Progreso personal visible.
3. Contexto del gimnasio elegido.
4. Competencia local voluntaria y justa.
5. Comunidad basada en logros reales.

La prioridad debe ser el loop:

```text
Elegir contexto opcional -> entrenar -> registrar -> entender progreso -> compartir o competir
```

El gimnasio, el GPS, el feed y los rankings deben enriquecer el entrenamiento, nunca bloquearlo.

## 2. Benchmark Competitivo

| Aplicacion | Fortaleza observada                                           | Aprendizaje para OlympX                                                   | No copiar ahora                                                          |
| ---------- | ------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Hevy       | Registro intuitivo, rutinas, PRs, historial y comunidad       | Precargar el ultimo peso, repetir rutinas y convertir logros en contenido | Intentar igualar toda su profundidad desde el primer release             |
| Strong     | Experiencia simple y rapida para registrar fuerza             | La sesion debe poder usarse con una mano y pocos toques                   | Formularios largos antes del primer set                                  |
| JEFIT      | Biblioteca amplia, planes, metricas y comunidad               | Catalogo curado, filtros y planes reutilizables                           | Sobrecargar al principiante con cientos de opciones                      |
| Fitbod     | Recomendaciones personalizadas, recuperacion y equipamiento   | Recomendaciones adaptativas son una oportunidad futura                    | IA antes de tener datos confiables de sesiones                           |
| Strava     | Registro, resumen posterior, feed, clubes, retos y privacidad | Registrar primero; compartir y competir despues                           | GPS continuo, ranking como primera experiencia o exposicion de ubicacion |
| Wellhub    | Descubrimiento por ubicacion, red de recintos y modelo B2B2C  | El gimnasio puede ser contexto y canal comercial                          | Convertirse ahora en marketplace de membresias                           |
| ClassPass  | Busqueda, disponibilidad, reserva y red de partners           | La busqueda debe dar contexto accionable del recinto                      | Reservas, creditos y operaciones de marketplace en el MVP                |

### Fuentes

- Hevy: https://www.hevyapp.com/
- Strong: https://www.strong.app/
- JEFIT: https://www.jefit.com/
- Fitbod: https://fitbod.me/
- Strava: https://www.strava.com/features
- Wellhub Chile: https://wellhub.com/es-cl/
- ClassPass: https://classpass.com/

Las cifras comerciales y de usuarios publicadas por cada empresa son declaraciones propias y no se
usan como validacion independiente de mercado.

## 3. Propuesta De Valor

> Registra tus entrenamientos sin friccion, demuestra tu progreso y compite opcionalmente con
> personas de tu gimnasio.

El segmento inicial recomendado es:

- Personas de 18 a 35 anos.
- Entrenan fuerza 3 a 5 veces por semana.
- Ya usan notas, Excel, Strong, Hevy o una app similar.
- Quieren progresar y toleran la comparacion si pueden controlarla.
- Frecuentan gimnasios con suficiente densidad local.

El lanzamiento debe concentrarse en 3 a 5 gimnasios piloto de una ciudad o zona, no en todo el
mercado fitness al mismo tiempo.

## 4. Flujo Recomendado

### Usuario Nuevo

```text
Registro minimo
  -> Perfil opcional
  -> Hoy sin permisos
  -> Iniciar primer entreno
  -> Guardar primer set
  -> Resumen personal
  -> Elegir gimnasio, compartir o competir opcionalmente
```

Reglas:

- Registro obligatorio: email, contrasena y nickname.
- Gimnasio, peso, altura, sexo, nivel y ubicacion pueden completarse despues.
- No solicitar GPS, camara ni notificaciones al abrir la app.
- El primer entrenamiento debe comenzar con una accion principal.
- Para el primer set solo son obligatorios ejercicio, peso y repeticiones.
- RPE, RIR, titulo, intensidad, notas y zonas musculares son opcionales.
- El check-in aparece como accion contextual y no bloquea la sesion.
- El resumen debe mostrar primero progreso personal y despues compartir/ranking.

### Usuario Recurrente

```text
Abrir Hoy
  -> Continuar sesion activa o repetir ultimo entreno
  -> Registrar sets con referencias anteriores
  -> Ver mejora personal
  -> Compartir o consultar ranking opt-in
```

La accion principal de Hoy debe ser, en este orden:

1. Continuar una sesion activa.
2. Iniciar entrenamiento.
3. Repetir ultimo entrenamiento.
4. Usar una rutina.

## 5. Gimnasio Y Check-in

- El usuario puede entrenar sin gimnasio seleccionado.
- Solicitar ubicacion solo al buscar gimnasios cercanos o confirmar un check-in.
- Mantener busqueda manual como alternativa permanente.
- Mostrar el gimnasio principal separado de la lista de gimnasios cercanos.
- Confirmar distancia aproximada antes de hacer check-in.
- Mantener radio de 100 metros y cooldown de 30 minutos, si Producto los confirma.
- Un check-in duplicado debe ser informativo, no bloquear el entrenamiento.
- El check-in exitoso debe ofrecer `Iniciar entrenamiento`.
- La ubicacion exacta y el momento de presencia nunca deben publicarse por defecto.

### Riesgo Google Places

Los resultados externos de Google Places usan `place_id`, mientras que el detalle actual espera un
UUID de un gimnasio local. Antes de permitir guardar o abrir resultados externos hay que elegir una
de estas opciones:

1. Persistir o vincular el lugar externo en OlympX antes de permitir selección.
2. Mostrarlo como resultado informativo y abrir Google Maps, sin permitir check-in local.
3. Ofrecer `Solicitar agregar gimnasio` y crear un `GymRequest`.

No se debe navegar a `GET /gyms/:id` con un `place_id` sin resolver este contrato.

## 6. Entrenamiento

El entrenamiento es el producto principal. El flujo mínimo recomendado es:

```text
Iniciar -> ejercicio -> peso/repeticiones -> guardar set -> siguiente set -> finalizar -> resumen
```

P0:

- Crear sesion rapida sin exigir metadatos secundarios.
- Precargar el ultimo peso y repeticiones del ejercicio.
- Guardar automaticamente cada set.
- Recuperar una sesion activa si la app se cierra.
- Permitir repetir la ultima sesion.
- Diferenciar borrador, sesion activa y sesion finalizada.
- Mostrar PR, volumen, series y comparacion personal al finalizar.

P1:

- Asociar formalmente `TrainingSession` con `gymId` cuando el modelo de negocio este confirmado.
- Agregar ejercicios desde una biblioteca curada y buscable.
- Permitir editar o eliminar sets.
- Compartir una tarjeta de progreso revisable antes de publicar.

## 7. Comunidad Y Competencia

La comunidad debe funcionar aunque el gimnasio tenga pocos usuarios.

- El feed debe incluir progreso propio, logros y contenido editorial identificado como OlympX.
- La vista `Siguiendo` debe tener un estado vacio util.
- La actividad del gimnasio debe ser agregada y retrasada si puede revelar presencia individual.
- Los rankings deben ser opt-in, por ejercicio, periodo y categoria.
- Si no hay suficiente participacion, mostrar progreso personal o referencia general, no un ranking
  vacio.
- Compartir debe ser explicito; ningun check-in o entrenamiento debe publicarse automaticamente.
- Peso, altura, sexo, IMC, ubicacion exacta y datos de sesiones deben ser privados por defecto.
- Deben existir bloquear, silenciar, dejar de seguir y reportar.

La competencia debe premiar constancia y mejora, no volumen extremo, riesgo o presencia permanente.

## 8. Fricciones Actuales Detectadas

1. El onboarding actual exige perfil fisico y gimnasio antes de entrar al producto.
2. Home solicita ubicacion durante la carga, aunque el usuario no la haya pedido.
3. Un resultado de Google Places puede romper al abrir el detalle local.
4. La busqueda textual puede exponer gimnasios no activos o no verificados.
5. Check-in no ofrece una transicion directa a iniciar entrenamiento.
6. El check-in actualiza el backend, pero la pantalla puede conservar el estado local anterior.
7. `TrainingSession` no tiene aun estado formal de sesion ni `gymId`.
8. El detalle de entrenamiento no tiene finalizacion explicita ni recuperacion offline completa.
9. `HomeFeedSection` existe, pero Home no lo renderiza actualmente.
10. Las metricas de Home usan listados limitados y pueden subestimar sesiones o progreso.
11. La biblioteca de ejercicios no tiene un flujo movil completo de detalle y seleccion.
12. La documentacion de avance y la implementacion no siempre reflejan el mismo estado.

## 9. Priorizacion

### P0: Activacion Y Retencion

- Onboarding progresivo y gimnasio opcional.
- Primer entrenamiento en menos de 2 minutos.
- Registro rapido de sets.
- Sesion activa recuperable.
- Progreso personal despues de cada sesion.
- Privacidad clara y permisos contextuales.
- Fallback manual para GPS y gimnasios.
- Resolver el contrato Google Places antes de exponer seleccion.
- Instrumentar registro -> primer set -> segunda sesion semanal.

### P1: Comunidad Local

- Feed visible y util con pocos usuarios.
- Rankings opt-in por ejercicio y categoria.
- Percentiles y distancia al siguiente objetivo.
- Logros y tarjetas compartibles.
- Historial de check-ins.
- Moderacion, bloqueo, reportes y notificaciones configurables.
- `GymRequest` con revision Admin.

### P2: Escala Y Negocio

- Perfil verificado y panel agregado para gimnasios.
- Retos patrocinados y beneficios locales.
- Multiples gimnasios.
- Integraciones con wearables.
- Recomendaciones adaptativas.
- Reservas o marketplace tipo Wellhub/ClassPass.

## 10. Metricas

### North Star

**Usuarios activos semanales que completan al menos dos sesiones registradas.**

Esta metrica representa uso recurrente y valor incluso cuando no hay actividad social local.

### Indicadores Iniciales

| Metrica                                 |         Objetivo inicial |
| --------------------------------------- | -----------------------: |
| Registro a primer entrenamiento         |                   >= 40% |
| Retencion D30 de usuarios activados     |                   >= 20% |
| Sesiones por usuario retenido/semana    |                     >= 2 |
| Tiempo hasta primer set                 |              < 2 minutos |
| Usuarios que consultan progreso         |      >= 50% de activados |
| Usuarios que activan ranking voluntario | Medir antes de optimizar |
| Reportes o bloqueos                     |  Guardrail, no maximizar |

No usar descargas, usuarios registrados o check-ins como North Star.

## 11. Skills Y Agentes Recomendados

### Para Producto Y UX

- `product-manager`: user stories, RICE/MoSCoW, funnel y roadmap.
- `ux-designer`: user journeys, estados vacios, permisos y pruebas con usuarios.
- `accessibility`: VoiceOver/TalkBack, targets tactiles, contraste y errores anunciables.
- `frontend-design`: transformar el flujo priorizado en una UI mobile distintiva y consistente.

### Para Arquitectura Y Backend

- `plan`: diseñar antes de modificar `TrainingSession`, `GymRequest` y contratos.
- `arquitecto`: revisar limites de dominio, Google Places, multi-gimnasio y escalabilidad.
- `developer-backend`: implementar endpoints, validaciones y envelope API.
- `nestjs-best-practices`: revisar modulos, guards, errores y ciclo de vida NestJS.
- `prisma-client-api` y `prisma-database-setup`: cambios de schema, migraciones e integridad.

### Para Calidad Y Riesgo

- `qa`: matriz de casos y smoke E2E del flujo completo.
- `security`: GPS spoofing, privacidad, tokens, uploads y moderacion.
- `reviewer`: detectar regresiones y desalineaciones entre API, mobile y contratos.

### Secuencia De Trabajo Recomendada

1. `product-manager` y `ux-designer` validan el flujo P0.
2. `plan` y `arquitecto` definen cambios de datos y contratos.
3. `developer-backend` y `developer-frontend` implementan una rebanada vertical.
4. `qa` valida el funnel completo y estados alternos.
5. `security` y `accessibility` hacen auditorias antes del piloto.

## 12. Fuentes Internas Revisadas

- `olympx-mobile/src/screens/OnboardingScreen.tsx`
- `olympx-mobile/src/screens/HomeScreen.tsx`
- `olympx-mobile/src/screens/GymDetailScreen.tsx`
- `olympx-mobile/src/screens/SearchScreen.tsx`
- `olympx-mobile/src/screens/TrainingSessionCreateScreen.tsx`
- `olympx-mobile/src/screens/TrainingSessionDetailScreen.tsx`
- `olympx-mobile/src/components/home/HomeView.tsx`
- `olympx-api/src/modules/gyms/gyms.controller.ts`
- `olympx-api/src/modules/home/home.controller.ts`
- `olympx-api/prisma/schema.prisma`
- `doc/etapas/PlanCierreEtapa3.md`
