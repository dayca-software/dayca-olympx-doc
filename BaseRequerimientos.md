# OlympX MVP 2026 — Base de Requerimientos

> Documento maestro de requerimientos funcionales, no funcionales, reglas de negocio y flujos de usuario.
> Basado en: GlobalProjecto.md · AnexoMVP.md · AnalisisMercadoNegocio.md · ADRs Dayca
> Versión: 1.0 · Fecha: Junio 2026
> Guia de mantenimiento: `MatrizDocumentacion.md`

---

## Índice de Módulos

| Módulo | ID | Prioridad | Fase |
|--------|----|-----------|------|
| Autenticación y Perfil | M01 | Crítica | 1 |
| Gimnasios y GPS | M02 | Alta | 1 |
| Biblioteca de Ejercicios | M03 | Alta | 1 |
| Rutinas y Registro de Entrenamiento | M04 | Alta | 1 |
| PRs, Progreso y Rankings | M05 | Alta | 1 |
| Conquistas | M06 | Alta | 2 |
| Feed Social | M07 | Media | 2 |
| Notificaciones | M08 | Media | 2 |
| Activity Summary | M09 | Baja | 2 |
| Rivalidades, Top del Día y Títulos | M10 | Baja | 2 |
| Rangos de Fuerza Universales | M11 | Alta | 1 |

---

## M01 — Autenticación y Perfil

### 1. Descripción
Gestión de registro, inicio de sesión, perfil de usuario, niveles de experiencia y permisos de dispositivo. Puerta de entrada al ecosistema OlympX.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-001 | El sistema debe permitir registro con email + contraseña | Crítica | — |
| RF-002 | El sistema debe permitir inicio de sesión con Google OAuth | Alta | — |
| RF-003 | El sistema debe permitir inicio de sesión con Apple OAuth | Alta | — |
| RF-004 | El sistema debe solicitar aceptación de términos y condiciones y políticas de privacidad en el registro | Crítica | RF-001 |
| RF-005 | El sistema debe permitir al usuario completar su perfil: nickname (obligatorio, único), edad, sexo, peso, altura, región, comuna, gimnasio principal, nivel fitness (Principiante/Intermedio/Avanzado) | Alta | RF-001 |
| RF-006 | El sistema debe permitir subir foto de avatar | Media | RF-005 |
| RF-007 | El sistema debe mostrar una splash screen animada (2-3s) al abrir la app con logo, slogan "Conquista. Entrena. Comparte." y carga de sesión | Media | — |
| RF-008 | El sistema debe mostrar pantalla de bienvenida con opciones: Crear cuenta, Iniciar sesión, Explorar versión limitada | Alta | — |
| RF-009 | El sistema debe permitir exploración limitada sin registro: ver rankings públicos, explorar gimnasios, ver ejemplos de conquistas, ver interfaz social básica | Media | — |
| RF-010 | El sistema debe restringir en modo exploración: competir, registrar entrenamientos, conquistar máquinas, publicar contenido | Alta | RF-009 |
| RF-011 | El sistema debe solicitar permisos de GPS, cámara y notificaciones post-registro | Alta | RF-001 |
| RF-012 | El sistema debe implementar sistema de niveles de usuario: Madera, Hierro, Bronce, Plata, Oro, Platino, Diamante, Rubí, Maestro | Media | — |
| RF-013 | El perfil público debe mostrar: avatar, nickname, gimnasio principal, nivel, estadísticas, historial, PRs, conquistas, seguidores, ranking, badges | Alta | RF-005 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-001 | El nickname debe ser único en todo el sistema | — |
| RN-002 | El email debe ser único en todo el sistema | — |
| RN-003 | La contraseña debe tener mínimo 8 caracteres, al menos 1 mayúscula, 1 número | — |
| RN-004 | El nivel de usuario se calcula en base a: experiencia acumulada (PRs, sesiones, conquistas, actividad) | Los niveles no decrecen |
| RN-005 | Usuario menor de 18 años requiere consentimiento parental (GDPR/ley local) | — |

---

## M02 — Gimnasios y GPS

### 1. Descripción
Catálogo de gimnasios, geolocalización contextual, check-in por GPS, heatmaps de actividad local. Sin tracking continuo tipo Strava.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-014 | El sistema debe mantener un catálogo de gimnasios con: nombre, dirección, latitud, longitud, cadena, ciudad, región | Alta | — |
| RF-015 | El sistema debe detectar gimnasios cercanos usando GPS del dispositivo | Alta | M02 |
| RF-016 | El sistema debe permitir check-in del usuario al llegar a un gimnasio | Alta | RF-014, RF-001 |
| RF-017 | El sistema debe permitir al usuario seleccionar su gimnasio principal | Alta | RF-014 |
| RF-018 | El sistema debe mostrar gimnasios activos (con usuarios haciendo check-in recientemente) | Media | RF-016 |
| RF-019 | El sistema debe mostrar actividad local: usuarios activos cercanos de manera limitada | Media | RF-016 |
| RF-020 | El sistema debe mostrar heatmaps simplificados: horarios punta, máquinas más disputadas, gimnasios más competitivos | Baja | RF-016 |
| RF-021 | Los mapas deben ser locales/regionales basados en gimnasios cercanos (radios 1km, 3km, 5km) | Media | RF-015 |
| RF-022 | El sistema debe tener una sección "Actividad del Gym" por gimnasio mostrando: últimas conquistas, PRs recientes, top levantamientos del día, usuarios activos recientes, máquinas más disputadas | Alta | RF-016 |

### 2.1 Búsqueda y selección de gimnasios

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-022A | El sistema debe buscar gimnasios usando la última ubicación válida del usuario como punto de partida y mostrar resultados para selección | Alta | RF-015, RF-017 |
| RF-022B | El sistema debe permitir abrir los resultados de búsqueda en Google Maps o un proveedor equivalente para que el usuario seleccione el gimnasio correcto | Alta | RF-014 |
| RF-022C | El sistema debe permitir al usuario confirmar un gimnasio desde los resultados y guardarlo como gimnasio principal o gimnasio visitado | Alta | RF-017, RF-016 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-006 | El check-in solo es válido si el usuario está dentro de un radio de 100m del gimnasio | — |
| RN-007 | El check-in expira después de 2 horas sin actividad registrada | — |
| RN-008 | No existe tracking continuo GPS segundo a segundo | — |
| RN-009 | Un usuario solo puede tener un gimnasio principal activo a la vez | — |
| RN-010 | La búsqueda de gimnasios debe priorizar la última ubicación válida del usuario; si no existe, usar la ubicación actual o permitir búsqueda manual | — |

---

## M03 — Biblioteca de Ejercicios

### 1. Descripción
Catálogo de ejercicios con metadatos (grupo muscular, tipo, categoría muscular) e indicador de elegibilidad competitiva.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-023 | El sistema debe mantener un catálogo de ejercicios con: nombre, grupo muscular, tipo de ejercicio, categoría muscular, imagen, estado competitivo | Alta | — |
| RF-024 | El sistema debe permitir filtrar ejercicios por grupo muscular, tipo y categoría | Alta | RF-023 |
| RF-025 | El sistema debe permitir buscar ejercicios por nombre | Alta | RF-023 |
| RF-026 | El sistema debe marcar cada ejercicio como competitivo o no competitivo (elegible para conquistas) | Alta | RF-023 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-010 | Solo ejercicios marcados como `competitive = true` participan en conquistas y rankings | — |
| RN-011 | Un ejercicio no puede eliminarse si tiene sesiones de entrenamiento asociadas | — |

---

## M04 — Rutinas y Registro de Entrenamiento

### 1. Descripción
Sistema completo de creación de rutinas semanales y registro de entrenamiento en vivo con métricas avanzadas (RPE, RIR, series, repeticiones, peso). Inspirado en Hevy.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-027 | El usuario debe poder crear rutinas semanales personalizadas | Alta | RF-023 |
| RF-028 | El usuario debe poder organizar rutinas por días de la semana | Alta | RF-027 |
| RF-029 | El usuario debe poder agregar ejercicios a cada día con orden personalizado | Alta | RF-027, RF-023 |
| RF-030 | El usuario debe poder guardar rutinas como plantillas reutilizables | Media | RF-027 |
| RF-031 | El usuario debe poder registrar entrenamiento en vivo: peso, repeticiones, series, RPE (1-10), RIR (0-5), notas | Alta | RF-027 |
| RF-032 | El usuario debe poder marcar un set como "competir" o "no competir" para elegibilidad de conquistas | Alta | RF-031 |
| RF-033 | El sistema debe calcular tonelaje automáticamente: peso × repeticiones × series | Alta | RF-031 |
| RF-034 | El sistema debe mostrar tonelaje por ejercicio, por sesión y semanal | Alta | RF-033 |
| RF-035 | El sistema debe mostrar comparación semanal: "Subiste 5 kg respecto a la semana pasada", "Tu tonelaje aumentó 12%", etc. | Media | RF-033 |
| RF-036 | El sistema debe permitir registrar escala pre-sesión: sueño (0-10), motivación (0-10), DOMS (0-10), energía (0-10) | Media | RF-031 |
| RF-037 | El sistema debe mostrar historial de entrenamientos completo | Alta | RF-031 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-012 | Un set con `competir = false` no se considera para conquistas ni rankings absolutos | — |
| RN-013 | RPE debe ser valor entre 1 y 10 | — |
| RN-014 | RIR debe ser valor entre 0 y 5 | — |
| RN-015 | Una sesión no puede tener más de 50 sets para prevenir abuso | — |
| RN-016 | El tonelaje semanal se resetea cada lunes a las 00:00 UTC | — |

---

## M05 — PRs, Progreso y Rankings

### 1. Descripción
Cálculo automático de marcas personales (PRs), evolución de rendimiento y rankings por gimnasio, ejercicio y categorías demográficas.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-038 | El sistema debe calcular y almacenar automáticamente PRs (1RM, máximas repeticiones con peso fijo) | Alta | RF-031 |
| RF-039 | El sistema debe mostrar evolución personal: historial semanal, comparación consigo mismo, historial de PRs | Alta | RF-038 |
| RF-040 | El sistema debe generar rankings internos (personales): evolución, tonelaje, mejoras de rendimiento | Alta | RF-038 |
| RF-041 | El sistema debe generar rankings externos por: gimnasio, comuna, región, ejercicio | Alta | RF-038 |
| RF-042 | El sistema debe segmentar rankings por categorías: edad (rangos de 2 años: 18-20, 20-22, 23-25... hasta 70+), sexo (Masculino/Femenino/Otros), peso corporal (por kg), IMC (Bajo/Normal/Elevado/Alto) | Alta | RF-041 |
| RF-043 | El sistema debe incluir rankings relativos: DOTS, Wilks, kg por kg corporal, % de mejora | Baja | RF-041 |
| RF-044 | Los rankings agregados deben actualizarse semanalmente (no tiempo real) para optimizar costos | Alta | RF-041 |
| RF-045 | El sistema debe mostrar historial de PRs y marcas personales en el perfil | Alta | RF-038 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-017 | Un PR se registra cuando el usuario supera su mejor marca anterior en un ejercicio específico | — |
| RN-018 | Rankings agregados se calculan cada domingo 23:59 UTC (no en tiempo real) | Rankings dentro del mismo gimnasio pueden tener actualización diaria |
| RN-019 | Categorías de IMC: Bajo (<18.5), Normal (18.5-24.9), Elevado (25-29.9), Alto (≥30) | — |
| RN-020 | 1RM estimado se calcula con fórmula de Epley: peso × (1 + reps/30) | — |

---

## M06 — Conquistas

### 1. Descripción
Núcleo competitivo de OlympX. Sistema de conquista semanal por gimnasio, ejercicio y categoría. Cada gimnasio tiene líderes por máquina/ejercicio. Temporadas semanales reiniciables.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-046 | El sistema debe asignar un "Rey"/"Reina" por ejercicio y gimnasio basado en el mejor rendimiento de la semana | Alta | RF-031, RF-014 |
| RF-047 | El sistema debe segmentar conquistas por categorías: edad, sexo, peso corporal, IMC | Alta | RF-042 |
| RF-048 | El sistema debe tener temporadas semanales que se reinician automáticamente cada lunes | Alta | RF-046 |
| RF-049 | Al finalizar la semana: recalcular campeones, generar nuevos rankings, actualizar banners, actualizar títulos | Alta | RF-048 |
| RF-050 | El sistema debe generar publicación automática en el feed cuando alguien supera un récord | Media | RF-046 |
| RF-051 | El sistema debe notificar al dueño anterior del récord cuando es superado | Media | RF-046 |
| RF-052 | El sistema debe generar banner compartible al lograr una conquista | Media | RF-046 |
| RF-053 | El sistema debe considerar para la conquista: peso levantado, repeticiones, 1RM, rendimiento relativo, DOTS/Wilks, validación social | Alta | RF-046 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-021 | La conquista NO funciona como "quien entrenó último gana" sino como "quien tuvo el mejor rendimiento de la semana dentro de su categoría" | — |
| RN-022 | Un usuario solo puede ser campeón de un ejercicio por gimnasio a la vez | Puede ser campeón en múltiples ejercicios distintos |
| RN-023 | Si un usuario se cambia de gimnasio, pierde sus conquistas del gimnasio anterior | El historial de conquistas pasadas se conserva en el perfil |
| RN-024 | La semana competitiva comienza y termina los días lunes 00:00 UTC | — |

---

## M07 — Feed Social

### 1. Descripción
Corazón social de OlympX. Feed de publicaciones con contenido temporal (24h), reacciones fitness, comentarios y seguimiento entre usuarios.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-054 | El sistema debe mostrar un feed social con publicaciones de usuarios seguidos y del gimnasio local | Alta | RF-001 |
| RF-055 | Cada publicación puede incluir: foto temporal, video temporal, PR, conquista, entrenamiento, progreso semanal, comparación personal | Alta | RF-031, RF-038, RF-046 |
| RF-056 | Las fotos/publicaciones deben tener duración de 24 horas (formato historia) | Alta | RF-055 |
| RF-057 | Los videos deben tener duración máxima de 45-60 segundos | Alta | RF-055 |
| RF-058 | Los videos deben subirse desde galería (sin grabación directa en MVP) | Media | RF-057 |
| RF-059 | El sistema debe comprimir videos automáticamente al subir | Alta | RF-057 |
| RF-060 | El sistema debe eliminar contenido automáticamente tras 24 horas | Alta | RF-056 |
| RF-061 | El sistema debe incluir reacciones fitness (no dislikes tradicionales): 🔥 "Bestial", 💪 "Buena ejecución", 📈 "Vas progresando", 👑 "Dominaste", ⚠️ "No apruebo", 😂 "Ni bloqueaste" | Alta | RF-054 |
| RF-062 | El sistema debe permitir comentar publicaciones | Alta | RF-054 |
| RF-063 | El sistema debe permitir seguir/dejar de seguir usuarios | Alta | RF-054 |
| RF-064 | El sistema debe mostrar perfiles de otros usuarios | Alta | RF-013 |
| RF-065 | El sistema debe permitir compartir logros y banners fuera de la app (Instagram, WhatsApp, historias, TikTok) | Media | RF-052 |
| RF-066 | El sistema debe permitir ver progresión de amigos | Media | RF-063 |
| RF-067 | El sistema debe tener validación social por reacciones + comentarios + reportes + revisión manual (sin IA en MVP) | Media | RF-061 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-025 | Contenido multimedia expira automáticamente a las 24 horas de su publicación | — |
| RN-026 | Videos no pueden exceder 60 segundos ni 50MB | — |
| RN-027 | No se permite grabación directa desde la app en MVP, solo subida desde galería | — |
| RN-028 | Un usuario puede reportar una publicación, y el reporte queda en cola de revisión manual | — |

---

## M08 — Notificaciones

### 1. Descripción
Notificaciones push asincrónicas para mantener engagement, retorno diario y competitividad.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-068 | El sistema debe notificar cuando a un usuario le quitan una máquina/conquista | Alta | RF-046 |
| RF-069 | El sistema debe notificar cuando intentan quitarle el récord a un usuario | Alta | RF-046 |
| RF-070 | El sistema debe notificar cuando el usuario sube de ranking | Alta | RF-041 |
| RF-071 | El sistema debe notificar cuando el usuario recibe nuevas reacciones | Media | RF-061 |
| RF-072 | El sistema debe notificar cuando el usuario gana una nueva categoría | Media | RF-046 |
| RF-073 | El sistema debe notificar cuando alguien comenta el PR del usuario | Media | RF-062 |
| RF-074 | El sistema debe notificar recordatorios de entrenamiento (configurable) | Baja | — |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-029 | Las notificaciones son asíncronas, no requieren realtime extremo | — |
| RN-030 | El usuario puede configurar qué tipos de notificaciones recibir | — |
| RN-031 | No se enviarán más de 10 notificaciones push por hora por usuario para evitar spam | — |

---

## M09 — Activity Summary

### 1. Descripción
Resúmenes automáticos compartibles tipo Strava para aumentar viralidad y engagement. Generados al finalizar sesión, semana, conquista o PR.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-075 | El sistema debe generar resumen automático al finalizar cada sesión de entrenamiento | Media | RF-031 |
| RF-076 | El sistema debe generar resumen semanal automático: tonelaje total, ejercicios realizados, PRs obtenidos, máquinas conquistadas, ranking alcanzado, streak, nivel actual | Media | RF-033, RF-038, RF-046 |
| RF-077 | El sistema debe generar resumen al lograr una conquista o PR | Media | RF-046, RF-038 |
| RF-078 | Los resúmenes deben poder guardarse en galería y compartirse en Instagram, WhatsApp, historias, TikTok | Media | RF-075 |
| RF-079 | Los resúmenes deben incluir diseño visual con métricas destacadas: ej. "42.350 kg levantados esta semana", "Top 3 de Smart Fit Apoquindo", "+12% de progreso semanal" | Media | RF-075 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-032 | Los resúmenes semanales se generan cada domingo 23:59 UTC | — |
| RN-033 | Los resúmenes de sesión se generan inmediatamente al finalizar el registro de entrenamiento | — |

---

## M10 — Rivalidades, Top del Día y Títulos

### 1. Descripción
Sistema de competencia social pasiva: rivalidades entre usuarios, top del día automatizado y títulos de prestigio.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-080 | El usuario debe poder marcar a otros usuarios como rivales | Baja | RF-063 |
| RF-081 | El sistema debe mostrar comparación con rivales: PRs, tonelaje semanal, conquistas, rankings, streaks, progreso semanal, categorías dominadas | Baja | RF-041, RF-046 |
| RF-082 | El sistema debe seleccionar automáticamente el Top del Día destacando: mejor levantamiento, mejor progreso, mayor tonelaje, conquista más importante, mejor score social | Baja | RF-031, RF-038, RF-046 |
| RF-083 | El sistema debe otorgar títulos automáticos (Titles) según: conquistas, rankings, actividad, progreso, streaks, dominio de ejercicios | Baja | RF-046, RF-041 |
| RF-084 | Los títulos deben mostrarse en el perfil, sobre el nickname, en rankings, en publicaciones y en banners compartibles | Baja | RF-083 |
| RF-085 | Los títulos pueden obtenerse semanal, mensual o históricamente | Baja | RF-083 |
| RF-086 | El sistema debe incluir títulos como: "Rey del Press Banca", "Reina de Piernas", "Destructor de PRs", "Dominador de Smart Fit", "Maestro del Hierro", "Rey del Progreso", "Guardián del Gym", "Top Tonelaje Semanal" | Baja | RF-083 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-034 | Un usuario puede tener máximo 5 rivales activos simultáneamente | — |
| RN-035 | Rivalidades no requieren aceptación del otro usuario (unidireccional) | — |
| RN-036 | Los títulos no decrecen ni se pierden una vez obtenidos, pero pueden ser reemplazados por uno de mayor jerarquía | — |
| RN-037 | Top del Día se recalcula cada 24 horas | — |

---

## M11 — Rangos de Fuerza Universales

### 1. Descripción
Clasificación de fuerza basada en evidencia para comparar el rendimiento del usuario por ejercicio usando 1RM estimado y estándares universales. El ranking no depende del gimnasio donde entrene el usuario, sino de tablas comparables por ejercicio y sexo.

### 2. Requerimientos Funcionales

| ID | Descripción | Prioridad | Dependencias |
|----|------------|-----------|--------------|
| RF-087 | El sistema debe calcular el rango de fuerza del usuario por ejercicio usando el 1RM estimado y tablas estándar universales basadas en evidencia | Alta | RF-038, RF-041 |
| RF-088 | El sistema debe segmentar los rangos de fuerza primariamente por sexo | Alta | RF-042 |
| RF-089 | El sistema debe mostrar para cada ejercicio el rango actual, el percentil dentro de su categoría y la diferencia hasta el siguiente rango | Alta | RF-087 |
| RF-090 | El sistema debe generar una tarjeta visual compartible y una plantilla PDF con el rango obtenido, percentil y progreso hacia el siguiente nivel | Media | RF-089 |
| RF-091 | El sistema debe limitar el MVP a ejercicios principales definidos por negocio: press banca, sentadilla, peso muerto, dominadas, press militar, curl de bíceps, fondos con lastre, curl isquiotibial, leg extension, hip thrust, jalón al pecho y remo barra libre; luego permitir expansión post-MVP con data propia de la comunidad | Alta | RF-087 |

### 3. Reglas de Negocio

| ID | Regla | Excepción |
|----|-------|-----------|
| RN-038 | El rango de fuerza se calcula por ejercicio + sexo + 1RM estimado; no depende del gimnasio ni de la región | — |
| RN-039 | Los umbrales iniciales de rangos deben ser configurables y curados con base en evidencia | — |
| RN-040 | En el MVP solo se habilitan los ejercicios principales aprobados por negocio; el resto queda para post-MVP | — |
| RN-041 | La visualización pública debe mostrar el rango actual, el percentil y la distancia al siguiente rango cuando exista clasificación | — |
| RN-042 | Los umbrales y categorías iniciales de fuerza se mantienen por ejercicio y sexo, sin depender del gimnasio | — |

---

## Requerimientos No Funcionales

| ID | Descripción | Métrica | Prioridad |
|----|------------|---------|-----------|
| RNF-001 | El sistema debe responder en menos de 2 segundos (p95) en conexión 4G para endpoints críticos (login, feed, registro de entrenamiento) | < 2s p95 | Crítica |
| RNF-002 | Las contraseñas deben almacenarse hasheadas con bcrypt (costo 12) | bcrypt cost 12 | Crítica |
| RNF-003 | Toda comunicación debe ser por HTTPS/TLS 1.3 | TLS 1.3 | Crítica |
| RNF-004 | El sistema debe tener 99.5% de uptime mensual | 99.5% | Alta |
| RNF-005 | El costo de infraestructura no debe superar $50 USD/mes en MVP | < $50/mes | Alta |
| RNF-006 | La API debe usar el envelope de respuesta ADR-005: `{ ok, data?, message?, statusCode }` | Consistente | Alta |
| RNF-007 | Los endpoints deben estar rate-limited: 3 req/s, 20 req/10s, 100 req/60s | Throttler | Alta |
| RNF-008 | Las consultas de rankings agregados deben cachearse con TTL mínimo de 1 hora | TTL ≥ 1h | Alta |
| RNF-009 | El sistema debe soportar al menos 1,000 usuarios concurrentes en MVP | 1,000 CCU | Media |
| RNF-010 | Los tokens JWT deben expirar en 24 horas con refresh token | 24h + refresh | Alta |
| RNF-011 | Los JWT deben incluir claims unificados ADR-005: `sub`, `name`, `roles[]`, `company_uuid` | ADR-005 | Alta |
| RNF-012 | El contenido multimedia debe comprimirse automáticamente y almacenarse con expiración de 24h | Auto-compress + TTL | Alta |
| RNF-013 | Las respuestas paginadas deben seguir formato ADR-005: `{ data: [], meta: { page, pageSize, total } }` | ADR-005 | Media |

---

## Matriz de Trazabilidad Módulos vs. Etapas (AnexoMVP)

| Etapa | Semanas | Módulos Cubiertos | RFs Cubiertos |
|-------|---------|-------------------|---------------|
| E1 — Discovery + Diseño UX/UI | 1-2 | Todos (definición) | — |
| E2 — Backend + Auth | 2-4 | M01 | RF-001 a RF-013 |
| E3 — Gimnasios + GPS + Ejercicios | 4-6 | M02, M03 | RF-014 a RF-026 |
| E4 — Rutinas y Entrenamiento | 6-8 | M04 | RF-027 a RF-037 |
| E5 — PRs + Rankings | 8-10 | M05, M11 | RF-038 a RF-045, RF-087 a RF-091 |
| E6 — Conquistas + Estadísticas + Notificaciones | 10-12 | M06, M08 | RF-046 a RF-053, RF-068 a RF-074 |
| E7 — QA + Estabilización | 12-14 | Todos | Todos |

> **Nota:** M07 (Feed Social), M09 (Activity Summary) y M10 (Rivalidades/Top/Títulos) quedan fuera de las 7 etapas del MVP. Se recomienda priorizar según disponibilidad de contingencia.

> **Nota adicional:** M11 (Rangos de Fuerza Universales) forma parte del alcance MVP dentro de E5, pero su catálogo inicial se limita a los ejercicios principales definidos por negocio.

---

## Glosario

| Término | Definición |
|---------|-----------|
| 1RM | One Rep Max — peso máximo levantado en una repetición |
| RPE | Rating of Perceived Exertion — escala 1-10 de esfuerzo percibido |
| RIR | Repetitions In Reserve — repeticiones dejadas en la reserva |
| DOMS | Delayed Onset Muscle Soreness — dolor muscular post-entreno |
| DOTS | Puntaje que normaliza levantamientos entre diferentes pesos corporales |
| Wilks | Coeficiente que permite comparar fuerza entre diferentes pesos corporales |
| PR | Personal Record — marca personal |
| Conquista | Título de campeón semanal por ejercicio/gimnasio/categoría |
| Tonelaje | Peso total levantado: peso × repeticiones × series |
| Activity Summary | Resumen automático compartible de rendimiento |
| Heatmap | Mapa de calor de actividad en gimnasio |

---

## Tabla de Prioridades

| Prioridad | Definición |
|-----------|------------|
| Crítica | Sin esto el sistema no es funcional. Bloqueante. |
| Alta | Feature principal del MVP. Diferencial competitivo. |
| Media | Mejora significativa de experiencia. Puede pausarse. |
| Baja | Nice-to-have. Pospuesto si el presupuesto no alcanza. |
