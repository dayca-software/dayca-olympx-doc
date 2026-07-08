OlympX MVP 2026 — Documento Global y Detallado
Documento maestro de especificación funcional del MVP de OlympX. Incluye visión general, flujo completo del usuario, sistema social, módulo de conquista, rankings, GPS contextual, heatmaps, perfiles, rutinas, calculadores inteligentes y estructura de gamificación.
Se eliminó lo que tiene que ver con running, y validaciones de IA, agregándose ideas tipo HEVY y aminorando problemas pensando en servidor, pero a la vez también integrando elementos que lo hagan de una app paga, una experiencia elite (aunque básica, pero distintiva)
5. Flujo Completo del Usuario

5.1 Apertura de la aplicación

La aplicación iniciará con una Splash Screen animada de 2–3 segundos.
Elementos:
- Logo OlympX.
- Animación ligera.
- Slogan:
“Conquista. Entrena. Comparte.”
- Carga inicial de sesión y sincronización de datos.

Objetivo:
Generar identidad visual competitiva y moderna.

--------------------------------------------------

5.2 Pantalla de Bienvenida

Opciones:
- Crear cuenta.
- Iniciar sesión.
- Explorar versión limitada.

La exploración limitada permitirá:
- Ver algunos rankings.
- Explorar gimnasios.
- Ver ejemplos de conquistas.
- Ver interfaz social básica.

No permitirá:
- Competir.
- Registrar entrenamientos.
- Conquistar máquinas.
- Publicar contenido.

--------------------------------------------------

5.3 Registro

Opciones:
- Registro por email.
- Login con Google.
- Login con Apple.

Campos:
- Nombre.
- Email.
- Contraseña.
- Confirmación de contraseña.

Checkbox obligatorio:
- Aceptar términos y privacidad.

--------------------------------------------------

5.4 Completar Perfil

Campos:
- Foto/avatar.
- Nickname obligatorio.
- Edad.
- Sexo.
- Peso corporal.
- Altura.
- Región.
- Comuna.
- Gimnasio principal.
- Nivel fitness:
  - Principiante.
  - Intermedio.
  - Avanzado.

Objetivo:
Personalizar rankings, categorías y feed.

--------------------------------------------------

5.5 Permisos

La app solicitará:
- GPS.
- Cámara.
- Notificaciones.

GPS:
Se utilizará para:
- Detectar gimnasios cercanos.
- Activar check-in.
- Mostrar actividad local.
- Heatmaps locales.

La aplicación NO realizará tracking continuo estilo Strava.

6. Sistema GPS y Mapas

OlympX utilizará GPS contextual y geolocalización local.

No existirá tracking continuo segundo a segundo.

--------------------------------------------------

Funciones GPS del MVP

- Detectar gimnasios cercanos.
- Permitir check-in.
- Mostrar gimnasios activos.
- Mostrar actividad local.
- Mostrar heatmaps locales.
- Mostrar usuarios activos cercanos de manera limitada.

--------------------------------------------------

Radio de búsqueda sugerido

- 1 km.
- 3 km.
- 5 km.

Esto permitirá:
- Reducir carga servidor.
- Limitar consultas.
- Mantener contexto social local.

--------------------------------------------------

Opciones a cotizar

OPCIÓN A:
GPS solo para:
- Check-in.
- Gimnasios cercanos.

OPCIÓN B:
GPS para:
- Check-in.
- Gimnasios cercanos.
- Usuarios activos localmente.
- Actividad competitiva local.

--------------------------------------------------

Mapas MVP

Los mapas serán:
- Locales.
- Regionales.
- Basados en gimnasios cercanos.

No existirá:
- Mapa nacional territorial complejo.
- Tracking global continuo.
- Rutas tipo Strava.

7. Feed Social

El feed será el corazón social de OlympX.

Objetivo:
Transformar el entrenamiento en una experiencia social competitiva.

--------------------------------------------------

Cada publicación puede incluir:

- Foto temporal.
- Video temporal.
- PR.
- Conquista.
- Entrenamiento.
- Progreso semanal.
- Comparación personal.

--------------------------------------------------

Duración del contenido

- Historias/fotos: 24 horas.
- Videos: 45–60 segundos.

--------------------------------------------------

Características de videos

- Subida desde galería.
- Compresión automática.
- Expiración automática.
- Sin grabación directa dentro de la app en MVP.

--------------------------------------------------

Reacciones Fitness

Las publicaciones NO utilizarán dislikes tradicionales.

Reacciones:
🔥 “Bestial”
💪 “Buena ejecución”
📈 “Vas progresando”
👑 “Dominaste”
⚠️ “No apruebo”
😂 “Ni bloqueaste”

--------------------------------------------------

Funciones sociales

- Seguir usuarios.
- Ver perfiles.
- Reaccionar.
- Comentar.
- Compartir logros.
- Compartir banners.
- Ver progresión de amigos.
- Ver conquistas recientes.

8. Sistema de Conquista

El sistema de conquista será el núcleo competitivo de OlympX.

Cada gimnasio tendrá líderes por ejercicio o máquina.

--------------------------------------------------

Ejemplo

Press banca — Smart Fit La Florida

Rey actual:
Usuario X

Marca:
140 kg x 1 repetición.

--------------------------------------------------

Tipos de conquista

- 1RM.
- Máximas repeticiones con peso fijo.

--------------------------------------------------

Categorías obligatorias

- Edad.
- Sexo.
- Peso corporal.
- IMC.

--------------------------------------------------

Rankings Absolutos

Literalmente:
quien levanta más peso gana la categoría general.

--------------------------------------------------

Rankings por categorías

Edad:
- Rangos de 2 años:
18–20
20–22
23–25
...
hasta 70+.

Peso corporal:
- Categorías por kg.

IMC:
- Bajo IMC.
- IMC Normal.
- IMC Elevado.
- IMC Alto.

Sexo:
- Masculino.
- Femenino.
- Otros.

--------------------------------------------------

Rankings relativos

Incluyen:
- DOTS.
- Wilks.
- Kg por kg corporal.
- % de mejora.

--------------------------------------------------

Eventos competitivos

Cuando alguien supera un récord:
- Se actualiza el ranking.
- Se genera publicación automática.
- Se notifica al dueño anterior.
- Se genera banner compartible.

9. Rankings

Rankings Internos

- Evolución personal.
- Historial semanal.
- Comparación consigo mismo.
- Historial de PRs.
- Tonelaje.
- Mejoras de rendimiento.

--------------------------------------------------

Rankings Externos

- Por gimnasio.
- Por comuna.
- Por región.
- Por ejercicio.
- Por categoría.
- Por edad.
- Por IMC.
- Por peso corporal.

--------------------------------------------------

Optimización servidor

Los rankings agregados:
- podrán actualizarse semanalmente.
- no requerirán cálculos en tiempo real constantes.

Esto ayudará a:
- reducir costos.
- reducir consultas.
- optimizar backend.

10. Heatmaps

Los heatmaps serán simplificados y agregados.

No serán mapas en tiempo real complejos.

--------------------------------------------------

Mostrarán:

- Horarios punta.
- Máquinas más disputadas.
- Intentos fallidos.
- Gimnasios más competitivos.
- Conquistas semanales.
- Actividad local.

--------------------------------------------------

Objetivo

Crear sensación de:
- comunidad.
- competencia.
- actividad.
- territorialidad.

Sin requerir infraestructura extrema.

11. Videos o Fotos y Validación

Los videos o Fotos serán parte de la red social competitiva.

--------------------------------------------------

Esto dependerá del coste del servidor 
Características

- Duración máxima:
45–60 segundos.

- Subida desde galería.
- Compresión automática.
- Expiración automática.

--------------------------------------------------

Validación social MVP

- Reacciones.
- Comentarios.
- Reportes.
- Revisión manual.

--------------------------------------------------

Reacciones válidas

🔥 “Bestial”
💪 “Buena ejecución”
📈 “Vas progresando”
👑 “Dominaste”
⚠️ “No apruebo”
😂 “Ni bloqueaste”

--------------------------------------------------

Importante

No habrá IA de validación en MVP.

12. Notificaciones

Las notificaciones serán asincrónicas.

No se requiere realtime extremo.

--------------------------------------------------

Ejemplos

- Te quitaron la máquina.
- Intentaron quitarte el récord.
- Sigues siendo el dueño.
- Subiste de ranking.
- Recibiste nuevas reacciones.
- Ganaste una nueva categoría.
- Alguien comentó tu PR.

--------------------------------------------------

Objetivo

Mantener:
- engagement.
- retorno diario.
- competitividad.

13. Perfil del Usuario

Cada perfil incluirá:

- Avatar.
- Nickname.
- Gimnasio principal.
- Categoría.
- Estadísticas.
- Historial.
- PRs.
- Conquistas.
- Seguidores.
- Ranking.
- Nivel.
- Badges.

--------------------------------------------------

Sistema de niveles

- Madera.
- Hierro.
- Bronce.
- Plata.
- Oro.
- Platino.
- Diamante.
- Rubí.
- Maestro.

--------------------------------------------------

Información visible

- Tonelaje semanal.
- Historial de PRs.
- Evolución.
- Conquistas.
- Ranking local.
- Ranking regional.
- Badges desbloqueados.

14. Módulo de Rutinas y Registro de Entrenamiento

OlympX integrará un sistema completo de rutinas y registro de entrenamiento tipo HEVY.

--------------------------------------------------

Biblioteca de ejercicios

Cada ejercicio incluirá:
- Nombre.
- Imagen.
- Grupo muscular.
- Tipo de ejercicio.
- Categoría muscular.
- Estado competitivo.

--------------------------------------------------

Creación de rutinas

El usuario podrá:
- Crear rutinas semanales.
- Organizar días.
- Agregar ejercicios.
- Guardar plantillas.

--------------------------------------------------

Registro de entrenamiento

Por ejercicio:
- Peso.
- Repeticiones.
- Series.
- RPE.
- RIR.
- Notas.
- PR.
- Competir o no competir.

--------------------------------------------------

Escala previa a la sesión

- Sueño: 0–10.
- Motivación: 0–10.
- DOMS: 0–10.
- Energía: 0–10.

--------------------------------------------------

Tonelaje

Fórmula:
Peso × repeticiones × series.

La app mostrará:
- Tonelaje por ejercicio.
- Tonelaje semanal.
- Comparación semanal.
- Historial.

--------------------------------------------------

Comparación semanal

Ejemplos:
- “Subiste 5 kg respecto a la semana pasada.”
- “Tu tonelaje aumentó 12%.”
- “Mantuviste el rendimiento.”

--------------------------------------------------

Calculadores inteligentes

Basados en:
- RPE.
- RIR.
- Repeticiones.
- Peso.
- Sueño.
- DOMS.
- Motivación.

Recomendaciones:
- Mantener peso.
- Subir peso.
- Bajar peso.
- Reducir volumen.

Funcionarán mediante reglas condicionales simples tipo Excel.

15. Módulo de Rutinas y Registro de Entrenamiento

Algunas características relacionadas con la gamificación y atención de la app

🔥 Conquista Vigente Semanal

Objetivo

El sistema de “Conquista Vigente” busca generar competencia constante y justa dentro de cada gimnasio sin depender del horario en que entrene el usuario.

La conquista NO funcionará como:
- “quien entrenó último gana”.

Funcionará como:
- “quien tuvo el mejor rendimiento de la semana dentro de su categoría”.

--------------------------------------------------

Funcionamiento general

Cada semana existirán campeones vigentes por:
- gimnasio
- ejercicio
- categoría

Ejemplo:

Smart Fit La Florida — Press banca

👑 Campeón absoluto semanal
Ignacio — 160 kg x 1

👑 Campeona categoría 70–75 kg
Sofía — 95 kg x 5

👑 Campeón IMC Normal
Matías — 120 kg x 2

--------------------------------------------------

Duración de temporadas

La conquista será:
- semanal
- reiniciable automáticamente

Al finalizar la semana:
- se recalculan campeones
- se generan nuevos rankings
- se actualizan banners
- se actualizan títulos

--------------------------------------------------

Variables consideradas

- peso levantado
- repeticiones
- 1RM
- rendimiento relativo
- DOTS/Wilks
- categoría
- validación social

--------------------------------------------------

Beneficios

- competencia justa
- evita ventaja horaria
- genera retorno semanal
- aumenta participación
- evita monopolios permanentes

🔥 Activity Summary Automático

Objetivo

Generar resúmenes automáticos compartibles tipo Strava para:
- aumentar viralidad
- incentivar progreso
- aumentar orgullo competitivo
- generar marketing orgánico

--------------------------------------------------

Funcionamiento general

La app generará automáticamente imágenes/resúmenes al finalizar:
- sesión
- semana
- conquista
- PR
- temporada

--------------------------------------------------

Información posible

Resumen semanal:
- tonelaje total
- ejercicios realizados
- PRs obtenidos
- máquinas conquistadas
- ranking alcanzado
- streak
- nivel actual
- tiempo entrenado

--------------------------------------------------

Ejemplos

🔥 “42.350 kg levantados esta semana”
👑 “Top 3 de Smart Fit Apoquindo”
📈 “+12% de progreso semanal”
🏆 “Nuevo PR en Sentadilla”

--------------------------------------------------

Compartir

Los resúmenes podrán:
- guardarse en galería
- compartirse en Instagram
- compartirse en historias
- compartirse en WhatsApp
- compartirse en TikTok

--------------------------------------------------

Objetivo psicológico

- orgullo
- reconocimiento
- validación social
- competencia
- FOMO

🔥 Actividad del Gimnasio

Objetivo

Hacer que cada gimnasio se sienta:
- vivo
- competitivo
- activo
- social

--------------------------------------------------

Funcionamiento general

Cada gimnasio tendrá una sección llamada:
“Actividad del Gym”

Mostrará eventos recientes del gimnasio.

--------------------------------------------------

Información mostrada

- últimas conquistas
- PRs recientes
- top levantamientos del día
- usuarios activos recientes
- máquinas más disputadas
- streaks recientes
- top publicaciones del gym
- top progreso semanal

--------------------------------------------------

Ejemplos

🔥 “Ignacio conquistó Press Banca”
👑 “Nueva reina de Sentadilla”
📈 “Valentina aumentó 18% su tonelaje”
🏆 “Top PR del día”

--------------------------------------------------

Actualización

No requiere realtime extremo.

Puede actualizar:
- cada ciertos minutos
- cada apertura de app
- mediante refresh manual

--------------------------------------------------

Beneficios

- sensación de comunidad
- engagement local
- identidad de gimnasio
- retorno constante

 🔥 Favoritos / Rivalidades

Objetivo

Permitir competencia social pasiva entre usuarios sin necesidad de chat complejo.

--------------------------------------------------

Funcionamiento general

El usuario podrá:
- marcar rivales
- seguir progreso
- comparar estadísticas
- comparar conquistas
- comparar tonelaje
- comparar PRs

--------------------------------------------------

Importante

NO requiere:
- mensajería
- realtime complejo
- guerras en vivo

--------------------------------------------------

Información comparada

Rivalidades:
- PRs
- tonelaje semanal
- conquistas
- rankings
- streaks
- progreso semanal
- categorías dominadas

--------------------------------------------------

Ejemplo

Sofía vs Ignacio

Press banca:
- Sofía → 95 x 5
- Ignacio → 100 x 3

Tonelaje semanal:
- Sofía → 42.000 kg
- Ignacio → 39.000 kg

Conquistas:
- Sofía → 4
- Ignacio → 3

--------------------------------------------------

Beneficios

- comparación social
- engagement
- motivación
- competitividad
- retorno diario

🔥 Top del Día + Titles

TOP DEL DÍA

Objetivo

Destacar diariamente a usuarios relevantes dentro del ecosistema OlympX.

--------------------------------------------------

Funcionamiento general

La app seleccionará automáticamente:
- mejores levantamientos
- mejores progresos
- top tonelaje
- top publicaciones
- top conquistas

--------------------------------------------------

Tipos de Top

💪 Top levantamiento del día
Mayor PR o levantamiento destacado.

📈 Top progreso del día
Mayor mejora respecto a sí mismo.

🔥 Top tonelaje del día
Mayor volumen total.

👑 Top conquista del día
Conquista más importante o competitiva.

🌟 Top social del gym
Publicación con mejor score social.

--------------------------------------------------

Variables utilizadas

- tonelaje
- PR
- reacciones
- score social
- progresión
- conquistas
- categorías

--------------------------------------------------

TITLES (TÍTULOS)

Objetivo

Generar:
- identidad
- ego competitivo
- prestigio
- reconocimiento social

--------------------------------------------------

Funcionamiento general

La app otorgará títulos automáticos según:
- conquistas
- rankings
- actividad
- progreso
- streaks
- dominio de ejercicios

--------------------------------------------------

Ejemplos de Titles

👑 Rey del Press Banca
🏆 Reina de Piernas
🔥 Destructor de PRs
⚔️ Dominador de Smart Fit
💪 Maestro del Hierro
📈 Rey del Progreso
🛡️ Guardián del Gym
⚡ Top Tonelaje Semanal

--------------------------------------------------

Obtención

Los títulos pueden obtenerse:
- semanalmente
- mensualmente
- históricamente

--------------------------------------------------

Visualización

Los Titles aparecerán:
- en el perfil
- sobre el nickname
- en rankings
- en publicaciones
- en banners compartibles

--------------------------------------------------

Beneficios psicológicos

- status
- identidad
- tribalismo
- orgullo
- motivación
- diferenciación entre usuarios