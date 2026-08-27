# OlympX - Anexo de Cotizacion y Alcance MVP

> Documento comercial y de delivery para el MVP de OlympX.

## 1. Control Del Documento

| Campo                         | Valor                           |
| ----------------------------- | ------------------------------- |
| Proyecto                      | OlympX                          |
| Documento                     | Anexo tecnico de cotizacion MVP |
| Version                       | 2.0                             |
| Fecha base                    | Junio 2026                      |
| Presupuesto total referencial | CLP $6.000.000                  |
| Horas de desarrollo           | 888 h                           |
| Duracion estimada             | 14 semanas / 3,5 meses          |
| Fuente de planificacion       | `CartaGanttMVP.md`              |
| Guia de mantenimiento         | `MatrizDocumentacion.md`        |

## 2. Proposito Y Lectura Del Anexo

Este documento define la linea base comercial de la cotizacion original: alcance, etapas, horas,
entregables, costos, supuestos y criterios de aceptacion.

No reemplaza el estado real de implementacion. Para avance, riesgos y validaciones ejecutadas se
deben consultar `CartaGanttMVP.md`, `AvanceGlobal.md`, `AvanceAPI.md`, `AvanceMobile.md` y
`AvanceQA.md`.

La cotizacion original fue estructurada para entregar un **MVP Core en 8 semanas** y completar una
fase extendida hasta la semana 14. La implementacion actual fue ampliada con capacidades sociales y
competitivas; si ese alcance forma parte del lanzamiento comercial, debe aprobarse como nueva linea
base de producto y no asumirse automaticamente dentro de las 888 horas originales.

## 3. Resumen Ejecutivo

| Concepto                       | Definicion                                                             |
| ------------------------------ | ---------------------------------------------------------------------- |
| MVP Core                       | Entrenamiento, progreso, perfil, gimnasios, ejercicios y autenticacion |
| Fase extendida                 | PRs avanzados, rankings, logros, estadisticas y notificaciones         |
| Alcance actual de ejecucion    | MVP ampliado con red social, segun la Carta Gantt vigente              |
| Desarrollo                     | 7 etapas, 888 h, CLP $4.000.000                                        |
| Contingencia e infraestructura | CLP $2.000.000                                                         |
| Total cotizado                 | CLP $6.000.000                                                         |

## 4. Modelo De Alcance

### 4.1 MVP Core - Validacion En 8 Semanas

El MVP Core valida el loop principal de valor: registrarse, configurar el contexto deportivo,
entrenar y comprobar progreso.

**Incluye:**

- Registro e inicio de sesion por email.
- Perfil basico y seleccion de gimnasio principal.
- Busqueda de gimnasios cercanos y check-in contextual por GPS.
- Biblioteca de ejercicios.
- Creacion de rutinas y registro de sesiones.
- Series, repeticiones, peso y finalizacion de sesiones.
- PRs, tonelaje, historial y progreso personal.
- Rangos de fuerza para ejercicios base.

**Criterios de exito:**

- El usuario puede crear una cuenta e iniciar sesion.
- El usuario puede completar su perfil y elegir un gimnasio.
- El usuario puede registrar una sesion con sus series.
- El usuario puede consultar historial, PRs y progreso.
- El flujo puede ser probado de punta a punta en gimnasios piloto.

### 4.2 Fase Extendida - Semanas 9 A 14

La fase extendida mejora comparacion, retencion y operacion del producto.

**Incluye:**

- Rankings por ejercicio y gimnasio.
- Rangos de fuerza segmentados cuando exista una fuente aprobada.
- Logros y estadisticas basicas.
- Notificaciones basicas.
- QA, estabilizacion y cierre de entrega.

### 4.3 Alcance Ampliado Actual

La ejecucion actual considera el **MVP ampliado con red social**, con entrenamiento como flujo core.
Ademas de lo anterior, se han implementado o preparado:

- Feed social y publicaciones.
- Comentarios, likes, reacciones y follows.
- Perfiles publicos y descubrimiento social.
- Alertas sociales.
- Compartir progreso semanal y logros como publicaciones.
- Ranking general, ranking por ejercicio y logros.
- Panel Admin y moderacion basica.

La inclusion comercial definitiva de esta ampliacion debe quedar registrada en la aprobacion de
alcance. Multimedia avanzada, stories, coach, IA, tracking continuo, heatmaps y retencion avanzada
permanecen fuera de este corte salvo aprobacion posterior.

## 5. Requisitos Y Criterios De Aceptacion

| Area           | Requisito minimo                  | Criterio de aceptacion                                              |
| -------------- | --------------------------------- | ------------------------------------------------------------------- |
| Autenticacion  | Registro, login y sesion          | El usuario puede entrar, salir y recuperar su sesion tras reiniciar |
| Perfil         | Datos basicos, avatar y ubicacion | Los cambios se guardan y se reflejan en la app                      |
| Gimnasios      | Busqueda, principal y check-in    | El check-in valida gimnasio disponible, proximidad y duplicados     |
| Ejercicios     | Catalogo consultable              | El usuario puede buscar y seleccionar ejercicios para entrenar      |
| Rutinas        | Dias, ejercicios y objetivos      | El usuario puede crear, editar y reutilizar una rutina              |
| Entrenamiento  | Sesiones y series                 | El usuario puede agregar sets, finalizar y consultar historial      |
| Progreso       | PRs, tonelaje y 1RM estimado      | Los calculos se muestran con casos borde controlados                |
| Competencia    | Rankings y rangos                 | La posicion y el rango se calculan con reglas documentadas          |
| Comunidad      | Publicaciones e interacciones     | El usuario puede publicar, comentar, reaccionar y seguir            |
| Notificaciones | Alertas y estado de lectura       | La alerta se persiste y puede marcarse como vista                   |
| Administracion | Control basico y moderacion       | El admin puede operar los modulos definidos y sus permisos          |
| Release        | QA y builds reproducibles         | API, mobile y contratos pasan sus validaciones obligatorias         |

Los requisitos funcionales detallados y sus IDs viven en `BaseRequerimientos.md`. Si existe una
contradiccion, la decision de alcance debe resolverse en conjunto entre Producto y Delivery antes de
comprometer una entrega.

## 6. Plan De Etapas

Las 888 horas se distribuyen en siete etapas secuenciales. Las semanas son relativas al inicio del
proyecto y pueden ajustarse mediante control de cambios.

### Etapa 1 - Discovery, Planificacion Y UX/UI

**Semanas:** 1-2 | **Total:** 120 h

| Modulo                                  |     Horas |
| --------------------------------------- | --------: |
| Discovery, planificacion y arquitectura |      40 h |
| Diseno UX/UI esencial                   |      80 h |
| **Total**                               | **120 h** |

**Entregables:**

- Documento de alcance y especificacion funcional.
- Arquitectura del sistema definida.
- Prototipo navegable de las pantallas clave.
- Criterios iniciales de aceptacion y prioridades.

### Etapa 2 - Backend, Datos Y Autenticacion

**Semanas:** 2-4 | **Total:** 160 h

| Modulo                              |     Horas |
| ----------------------------------- | --------: |
| Backend base y base de datos        |      80 h |
| Registro, login y perfil de usuario |      80 h |
| **Total**                           | **160 h** |

**Entregables:**

- Servidor NestJS operativo.
- Modelo de datos Prisma y PostgreSQL.
- API base con health check.
- Autenticacion JWT con registro, login y perfil.
- Envoltorio de respuesta `{ ok, data, message, statusCode }`.

### Etapa 3 - Gimnasios, GPS Y Biblioteca De Ejercicios

**Semanas:** 4-6 | **Total:** 140 h

| Modulo                           |     Horas |
| -------------------------------- | --------: |
| Gimnasios, check-in y GPS basico |      80 h |
| Biblioteca de ejercicios         |      60 h |
| **Total**                        | **140 h** |

**Entregables:**

- Seleccion de gimnasio principal.
- Check-in contextual por GPS.
- Catalogo de ejercicios con grupo muscular y equipamiento.
- API de ejercicios con filtros.

### Etapa 4 - Rutinas Y Registro De Entrenamiento

**Semanas:** 6-8 | **Total:** 120 h

| Modulo                              |     Horas |
| ----------------------------------- | --------: |
| Rutinas y registro de entrenamiento |     120 h |
| **Total**                           | **120 h** |

**Entregables:**

- Creacion y edicion de rutinas personalizadas.
- Registro de entrenamiento en vivo.
- Series, repeticiones, peso y objetivos.
- Finalizacion y guardado de sesiones.
- Historial de entrenamientos.

**Salida del MVP Core:** al completar esta etapa el producto debe permitir validar el loop de
registro y progreso personal en un piloto controlado.

### Etapa 5 - PRs, Progreso Y Rankings

**Semanas:** 8-10 | **Total:** 140 h

| Modulo                                    |     Horas |
| ----------------------------------------- | --------: |
| PRs, tonelaje y progreso semanal          |      80 h |
| Rankings basicos por gimnasio y ejercicio |      60 h |
| **Total**                                 | **140 h** |

**Entregables:**

- Calculo automatico de marcas personales.
- Tonelaje por sesion y acumulado.
- Progreso semanal.
- Rankings por ejercicio dentro del gimnasio.
- Rangos de fuerza por ejercicio cuando exista una regla aprobada.
- Comparacion de marcas entre usuarios del mismo gimnasio.

### Etapa 6 - Logros, Estadisticas Y Notificaciones

**Semanas:** 10-12 | **Total:** 118 h

| Modulo                          |     Horas |
| ------------------------------- | --------: |
| Logros simples por ejercicio    |      50 h |
| Perfil con estadisticas basicas |      40 h |
| Notificaciones basicas          |      28 h |
| **Total**                       | **118 h** |

**Entregables:**

- Logros automaticos por hitos de actividad y rendimiento.
- Resumen de estadisticas del usuario.
- Alertas basicas por recordatorios, PRs y logros.

### Etapa 7 - QA, Estabilizacion Y Cierre

**Semanas:** 12-14 | **Total:** 90 h

| Modulo                       |    Horas |
| ---------------------------- | -------: |
| QA, pruebas y estabilizacion |     50 h |
| Gestion de proyecto          |     40 h |
| **Total**                    | **90 h** |

**Entregables:**

- Pruebas funcionales y de integracion acordadas.
- Correccion de bugs bloqueantes.
- Estabilizacion del entorno de entrega.
- Coordinacion y cierre del proyecto.

## 7. Resumen De Horas Y Costos

El costo de desarrollo se calcula con un valor referencial aproximado de CLP $4.500 por hora. Los
montos por etapa se redondean a miles de pesos para facilitar la cotizacion.

|                Etapa | Descripcion                           | Semanas |     Horas |         Desarrollo |       Anticipo 50% |
| -------------------: | ------------------------------------- | ------: | --------: | -----------------: | -----------------: |
|                    1 | Discovery, planificacion y UX/UI      |     1-2 |     120 h |       CLP $540.000 |       CLP $270.000 |
|                    2 | Backend, datos y autenticacion        |     2-4 |     160 h |       CLP $720.000 |       CLP $360.000 |
|                    3 | Gimnasios, GPS y ejercicios           |     4-6 |     140 h |       CLP $630.000 |       CLP $315.000 |
|                    4 | Rutinas y entrenamiento               |     6-8 |     120 h |       CLP $540.000 |       CLP $270.000 |
|                    5 | PRs, progreso y rankings              |    8-10 |     140 h |       CLP $630.000 |       CLP $315.000 |
|                    6 | Logros, estadisticas y notificaciones |   10-12 |     118 h |       CLP $531.000 |       CLP $265.500 |
|                    7 | QA, estabilizacion y cierre           |   12-14 |      90 h |       CLP $409.000 |       CLP $204.500 |
| **Total desarrollo** |                                       |         | **888 h** | **CLP $4.000.000** | **CLP $2.000.000** |

### Presupuesto Total

| Concepto                       |              Monto |
| ------------------------------ | -----------------: |
| Desarrollo                     |     CLP $4.000.000 |
| Contingencia e infraestructura |     CLP $2.000.000 |
| **Total cotizado**             | **CLP $6.000.000** |

La contingencia no representa horas adicionales garantizadas de desarrollo. Se reserva para
servidores, infraestructura y eventualidades de operacion, y requiere aprobacion para ser utilizada.

## 8. Dependencias Y Supuestos

- El cliente entrega decisiones de alcance y feedback dentro de los plazos acordados.
- Las credenciales de servicios externos, cuentas de tiendas y configuraciones de infraestructura se
  entregan oportunamente.
- El desarrollo considera NestJS, PostgreSQL, Prisma, React y React Native como stack base.
- El MVP no depende de tracking continuo, IA, video avanzado ni mapa nacional.
- El GPS depende de permisos del dispositivo y disponibilidad de ubicacion.
- Las notificaciones push requieren configuracion de Firebase, APNs y pruebas en dispositivos reales.
- Los pagos y entitlements requieren configuracion de RevenueCat fuera del simple render del paywall.
- Las migraciones de base de datos deben ejecutarse y verificarse en cada entorno de entrega.
- Las fechas pueden moverse si se modifica el alcance, aparecen dependencias externas o se retrasa una
  aprobacion.

## 9. Fuera De Alcance De Esta Linea Base

- Historias o estados temporales.
- Subida y procesamiento avanzado de imagen o video.
- Coach, IA, nudges y retencion avanzada.
- Tracking continuo de ubicacion.
- Heatmaps y actividad local avanzada.
- Integraciones sociales externas.
- Exportaciones PDF y percentiles avanzados.
- Operacion productiva completa sin una etapa explicita de hardening y observabilidad.

Estas capacidades pueden incorporarse mediante una nueva etapa, una fase posterior o una orden de
cambio con estimacion independiente.

## 10. Control De Cambios

Todo cambio que afecte alcance, horas, costo, dependencias o fecha debe registrar:

1. Descripcion del cambio y motivo.
2. Requisitos y documentos impactados.
3. Estimacion de horas y costo adicional o ahorro.
4. Impacto en fechas y riesgos.
5. Aprobacion de Producto y Delivery.

La trazabilidad funcional se mantiene en `MatrizTrazabilidad.md`. Los cambios de negocio se reflejan
en `BaseRequerimientos.md`; los cambios de etapas, horas o presupuesto se reflejan en este anexo.

## 11. Criterios De Cierre

La linea base se considera entregada cuando:

- El alcance aprobado funciona de punta a punta.
- El MVP Core permite registrar entrenamiento y consultar progreso.
- Los errores bloqueantes conocidos fueron corregidos o aceptados formalmente.
- API, mobile y contratos pasan sus typechecks.
- Las migraciones requeridas están aplicadas en el entorno acordado.
- Los flujos criticos tienen pruebas documentadas y ejecutadas.
- Existe un build reproducible para el entorno de entrega.

Para el MVP ampliado, además se debe validar el flujo login, home, entrenamiento, publicación,
interacción social, competencia y notificaciones antes de declararlo listo para release.

## 12. Cronograma De Referencia

```text
Semana    01 02 03 04 05 06 07 08 09 10 11 12 13 14
Etapa 1   == ==
Etapa 2      == == ==
Etapa 3            == == ==
Etapa 4                  == == ==
Etapa 5                        == == ==
Etapa 6                              == == ==
Etapa 7                                    == == ==

Salida Core: semana 08
Salida extendida: semana 14
```

## 13. Documentos Relacionados

- `CartaGanttMVP.md`: calendario y avance ejecutivo.
- `BaseRequerimientos.md`: requisitos funcionales y reglas de negocio.
- `MatrizTrazabilidad.md`: relacion entre vision, requisitos y datos.
- `ChecklistCierreMVP.md`: checklist operativo de cierre.
- `AvanceGlobal.md`: estado real de API y mobile.
- `AvanceQA.md`: cobertura y riesgos de calidad.
- `MatrizDocumentacion.md`: reglas para mantener la documentacion.
