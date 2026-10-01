# Etapa 3 - Resumen Para Usuario No Técnico

## 1. Qué Se Desarrolló

La Etapa 3 permitió que OlympX comenzara a relacionar la experiencia de entrenamiento con el lugar donde la persona entrena y con los ejercicios que realiza.

Antes de esta etapa, la aplicación podía tener usuarios y una estructura inicial, pero todavía no contaba con un flujo completo para:

- Encontrar un gimnasio.
- Saber si ese gimnasio está disponible.
- Elegirlo como gimnasio principal.
- Confirmar que la persona se encuentra físicamente en el gimnasio.
- Consultar una biblioteca ordenada de ejercicios.

Con el desarrollo de esta etapa, esos flujos ya están disponibles en la aplicación.

## 2. Resultado General

La etapa se considera completada con el alcance aprobado.

El usuario ahora puede buscar gimnasios, revisar su información, guardar uno como principal, registrar una visita mediante la ubicación del teléfono y consultar ejercicios por nombre o grupo muscular.

El equipamiento de los gimnasios o de los ejercicios no se incluye en esta etapa. Se dejó definido como una mejora para una etapa posterior, sin impedir que el resto de la biblioteca esté disponible y funcionando.

## 3. Gimnasios

### 3.1 Buscar Un Gimnasio

La aplicación permite buscar gimnasios de dos maneras:

1. Usando la ubicación del teléfono para mostrar opciones cercanas.
2. Utilizando una búsqueda general cuando la persona no desea compartir su ubicación o el teléfono no logra obtenerla.

Esto evita que el usuario quede bloqueado si el GPS está apagado, si no concede el permiso o si se encuentra en un lugar donde la señal no es precisa.

### 3.2 Ver Información Del Gimnasio

Al seleccionar un gimnasio, la aplicación muestra información como:

- Nombre.
- Dirección.
- Ciudad.
- Región.
- Cadena o marca, cuando existe.
- Si el gimnasio está activo.
- Si el gimnasio fue verificado.
- Si tiene una ubicación disponible para las funciones de GPS.

La persona puede saber si ese gimnasio está disponible antes de intentar realizar una acción.

### 3.3 Elegir El Gimnasio Principal

El usuario puede marcar un gimnasio como su gimnasio principal.

Esto significa que OlympX lo reconocerá como el lugar habitual de entrenamiento de esa persona. El gimnasio principal queda guardado en el perfil y puede utilizarse como referencia para futuras funciones de la aplicación.

La selección se realiza desde el detalle del gimnasio y la aplicación informa cuando el cambio fue guardado correctamente.

### 3.4 Ver Actividad Del Gimnasio

El detalle del gimnasio incluye una visión de la actividad reciente de la comunidad, por ejemplo:

- Cantidad de visitas recientes registradas.
- Últimos usuarios que realizaron una visita pública.
- Publicaciones recientes relacionadas con ese gimnasio.

Esta información permite entender si el gimnasio tiene actividad dentro de la comunidad OlympX.

### 3.5 Abrir La Ubicación En Mapas

Cuando el gimnasio tiene una ubicación registrada, el usuario puede abrirla en la aplicación de mapas del teléfono.

En iPhone se utiliza Apple Maps y en Android se utiliza la aplicación de mapas disponible en el dispositivo.

Esto ayuda a que la persona pueda confirmar dónde está el gimnasio o planificar cómo llegar.

## 4. Check-in De Gimnasio

### 4.1 Qué Es El Check-in

El check-in es una confirmación de que el usuario se encuentra en un gimnasio determinado.

No significa que OlympX siga a la persona durante todo el día. La ubicación se utiliza solamente en el momento en que se busca un gimnasio cercano o se intenta confirmar una visita.

### 4.2 Cómo Funciona

Cuando el usuario presiona “Hacer check-in”:

1. La aplicación solicita permiso para consultar la ubicación.
2. El teléfono entrega su posición actual.
3. OlympX compara esa posición con la ubicación del gimnasio.
4. Si la persona está dentro del área permitida, se registra la visita.
5. El gimnasio queda asociado como principal.
6. La aplicación muestra la hora en que se registró el check-in.

### 4.3 Protección Del Check-in

El sistema verifica varias condiciones para evitar registros incorrectos:

- El gimnasio debe estar activo.
- El gimnasio debe estar verificado.
- El gimnasio debe tener una ubicación válida.
- El teléfono debe entregar una ubicación válida.
- La persona debe estar aproximadamente a menos de 100 metros.
- No se permite repetir inmediatamente el mismo check-in.

Si una de estas condiciones no se cumple, la aplicación muestra un mensaje y no registra una visita falsa.

### 4.4 Mensajes Para El Usuario

La aplicación contempla situaciones como:

- Permiso de ubicación rechazado.
- Ubicación no disponible.
- Persona demasiado lejos del gimnasio.
- Gimnasio inactivo.
- Gimnasio todavía no verificado.
- Gimnasio sin ubicación configurada.
- Check-in repetido recientemente.

El objetivo es que el usuario entienda qué ocurrió y pueda corregir la situación o continuar usando la búsqueda manual.

## 5. Biblioteca De Ejercicios

### 5.1 Para Qué Sirve

La biblioteca reúne los ejercicios que pueden utilizarse dentro de OlympX.

Su objetivo es que el usuario pueda encontrar fácilmente un ejercicio, entender a qué grupo muscular pertenece y revisar su información antes de utilizarlo en un entrenamiento.

### 5.2 Buscar Ejercicios

El usuario puede escribir el nombre de un ejercicio, por ejemplo:

- Press banca.
- Sentadilla.
- Peso muerto.
- Remo.
- Curl de bíceps.

La aplicación busca coincidencias y muestra los resultados disponibles.

### 5.3 Filtrar Por Grupo Muscular

La biblioteca permite ordenar la búsqueda por grupos como:

- Pecho.
- Espalda.
- Piernas.
- Hombros.
- Brazos.
- Glúteos.

Esto permite encontrar rápidamente ejercicios relacionados con el objetivo de la sesión.

### 5.4 Información De Cada Ejercicio

Cada ejercicio puede mostrar:

- Nombre.
- Grupo muscular.
- Tipo de ejercicio.
- Categoría muscular.
- Imagen cuando exista.
- Si es competitivo o general.

La información se presenta de forma simple dentro de la pantalla de detalle.

### 5.5 Ejercicios Competitivos

Algunos ejercicios pueden utilizarse para funciones competitivas futuras, como récords, conquistas o rankings.

La biblioteca identifica esa diferencia mediante una etiqueta. Así, la aplicación puede distinguir entre un ejercicio que participa en la competencia y uno que se utiliza solamente como referencia o entrenamiento general.

## 6. Administración Del Contenido

Además de lo que ve el usuario, se preparó el soporte para que el equipo administrador pueda mantener la información actualizada.

El administrador puede:

- Crear gimnasios.
- Editar gimnasios.
- Activar o desactivar gimnasios.
- Revisar su estado de verificación.
- Buscar gimnasios por texto.
- Filtrar gimnasios según su estado.
- Consultar el catálogo de ejercicios.
- Crear ejercicios nuevos indicando su información básica.
- Filtrar ejercicios por sus características.
- Definir si un ejercicio es competitivo.

Esto evita que la información dependa de cambios directos en la base de datos y permite mantener un catálogo controlado.

## 7. Qué Significa Para La Experiencia Del Usuario

La Etapa 3 mejora la experiencia de OlympX en cuatro aspectos principales:

1. La aplicación sabe qué gimnasios están disponibles.
2. El usuario puede identificar su lugar principal de entrenamiento.
3. El check-in se basa en una comprobación real de cercanía.
4. Los ejercicios están organizados para que sea más fácil comenzar a entrenar.

El resultado es una aplicación más contextual: no solo registra acciones, también entiende el gimnasio y los ejercicios asociados a la experiencia del usuario.

## 8. Lo Que No Se Incluye En Esta Etapa

Para mantener claro el alcance, esta etapa no incluye:

- Información de equipamiento de cada gimnasio.
- Información de equipamiento de cada ejercicio.
- Seguimiento permanente de la ubicación.
- Mapas internos de gimnasios.
- Heatmaps avanzados de horarios o máquinas.
- Personas cercanas en tiempo real.
- Solicitudes de gimnasios que todavía no estén en el catálogo.

El equipamiento queda planificado para una etapa posterior. Esto no impide utilizar la biblioteca de ejercicios ni realizar las acciones de gimnasios entregadas en esta fase.

## 9. Evidencia De La Entrega

La implementación fue acompañada por:

- Pruebas automatizadas del backend.
- Pruebas automatizadas de mobile.
- Validación de tipos y compilación.
- Verificación de búsqueda de gimnasios.
- Verificación del detalle de gimnasio.
- Verificación de selección de gimnasio principal.
- Verificación del check-in dentro del radio permitido.
- Verificación de la biblioteca y sus filtros.

La documentación técnica de respaldo identifica los módulos, pantallas y contratos utilizados para construir estos flujos.

## 10. Cierre De La Etapa

La Etapa 3 queda entregada porque los usuarios pueden:

- Buscar un gimnasio.
- Revisar su información.
- Guardarlo como gimnasio principal.
- Confirmar una visita mediante GPS.
- Recibir una respuesta clara cuando una condición no permite el check-in.
- Consultar la actividad reciente del gimnasio.
- Abrir la ubicación en mapas.
- Buscar ejercicios.
- Filtrar ejercicios.
- Revisar el detalle de un ejercicio.
- Distinguir ejercicios competitivos de ejercicios generales.

El siguiente trabajo relacionado será incorporar equipamiento y ampliar la información asociada a gimnasios y ejercicios, pero ese desarrollo corresponde a una etapa posterior y no modifica la entrega de la Etapa 3.

## 11. Glosario Simple

| Término               | Significado simple                                                                      |
| --------------------- | --------------------------------------------------------------------------------------- |
| GPS                   | Sistema del teléfono que permite conocer aproximadamente dónde se encuentra una persona |
| Check-in              | Registro de que el usuario está en un gimnasio                                          |
| Gimnasio principal    | Gimnasio habitual que el usuario decide guardar en su perfil                            |
| Catálogo              | Lista organizada de gimnasios o ejercicios disponibles                                  |
| Filtro                | Opción para reducir una lista y encontrar algo más rápido                               |
| Ejercicio competitivo | Ejercicio que puede participar en funciones de competencia de OlympX                    |
| API                   | Canal que permite que la aplicación mobile consulte y guarde información                |
| Estado verificado     | Confirmación administrativa de que el gimnasio puede utilizarse en la aplicación        |
