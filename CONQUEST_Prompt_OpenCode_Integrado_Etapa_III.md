# CONQUEST — PROMPT MAESTRO PARA OPENCODE
## Integración controlada del Entregable Etapa III + Feedback Fase III

> **Uso:** ejecutar dentro del repositorio real de CONQUEST. Adjuntar como referencias `CONQUEST_Entregable_Etapa_III_VF_Corregido.docx` y `Feedback Fase III Conquest.docx`, o proporcionar sus imágenes/capturas relevantes. **No confundir maquetas o propuestas con el estado del código.**

## Rol y objetivo

Actúa como desarrollador senior especializado en React Native, arquitectura de aplicaciones y evolución segura de software. Debes **inspeccionar primero el código existente** e incorporar de manera incremental, funcional y verificable las observaciones visuales y de experiencia de usuario que aparecen en DOS documentos del cliente:

1. **`CONQUEST_Entregable_Etapa_III_VF_Corregido.docx`**, que incluye capturas actuales, imágenes comparativas de rediseño y textos de especificaciones para desarrollador.
2. **`Feedback Fase III Conquest.docx`**, que detalla observaciones posteriores sobre las mismas pantallas.

**Meta:** aprovechar componentes, rutas, servicios, estilos, datos, assets e interacciones ya desarrollados. No crear una aplicación distinta ni rehacer pantallas por completo. No deshacer funcionalidades demostradas en Etapa III. Minimizar líneas y archivos modificados, manteniendo calidad visual y funcional.

## Reglas innegociables

- **Primero diagnóstico, luego código:** identificar el framework, estructura mobile, design tokens, componentes y estado de cada funcionalidad en el repositorio. Nada de inventar rutas de archivos ni asumir que una pantalla sigue igual que en una captura antigua.
- **Documentos son referencias de producto/diseño, NO especificación de refactorización:** las imágenes de “Actual” / “Propuesta” expresan apariencia y jerarquía, no autorizan cambios de lógica, API ni arquitectura. Si parte del rediseño ya existe, no repetirlo.
- **En caso de conflicto:** (a) preservar comportamiento y reglas del código existente; (b) respetar solicitud funcional concreta del feedback posterior; (c) aplicar lineamientos premium del entregable donde sean compatibles; (d) escalar ambigüedades sin improvisar.
- Mantener las funcionalidades, rutas, controles, validaciones, estados vacíos, permisos y cálculo estadístico presentes.
- **Sin cambios de backend, API, contratos, base de datos, migraciones, autenticación, planes/trial/pagos, GPS/check-in, rankings, PR, 1RM, persistencia de ejercicios ni reglas de negocio.** Si algo estrictamente exige uno de ellos, documentarlo y pedir aprobación antes de realizarlo.
- No instalar dependencias pesadas, no agregar nuevos endpoints, no refactorizar globalmente, no incorporar mocks como datos reales y no cambiar el tema de toda la app de una vez.
- Reutilizar la biblioteca de iconos, componentes y assets existentes. Las imágenes de renders y ejemplos del documento son **referencias de apariencia**; no asumir que sus archivos están disponibles ni que tienen licencia para publicación comercial.
- Para imágenes/fuentes/SVG externos comprobar licencia de uso comercial y atribución. Si faltan, dejar fallback y necesidad documentada.
- Respetar safe areas, navegación inferior, scroll, accesibilidad (áreas de toque de aproximadamente 44×44 puntos), pequeños dispositivos, estado oscuro, iOS/Android y legibilidad.

## Identidad visual de referencia — aplicarla sin reestructurar el tema

En el Entregable Etapa III se propone una línea **premium minimalista / deportiva**:

| Token de referencia | Valor |
|---|---|
| Fondo negro | `#05090D` |
| Tarjeta grafito | `#0D1720` |
| Superficie azul profunda | `#101E32` |
| Azul eléctrico, navegación/selección | `#259BEB` |
| Turquesa, acción principal | `#4ADBE5` |
| Texto principal | `#F7F9FC` |
| Texto secundario | `#A7B4C4` |
| Borde tenue | `#254258` |
| Tipografía de referencia | `Inter` |
| Iconografía de referencia | `Lucide` |
| Radio tarjetas | aprox. `18–20px` |
| Radio botones | aprox. `12–14px` |
| Márgenes laterales y separación | aprox. `16px` |

**Aplicación conservadora:** buscar los tokens y fuentes ya existentes; reutilizar equivalentes. Si una pantalla ya adoptó un diseño premium consistente, conservarlo. No forzar toda la paleta como reemplazo global ni introducir `Inter` o `Lucide` como nuevas dependencias solo porque aparecen en la maqueta. Evitar fondos morados/azules muy extensos, tarjetas anidadas, gradientes intensos y decoración excesiva. Usar contraste, separación y una acción principal clara por pantalla.

---

## MATRIZ DE TRABAJO POR PANTALLA

### 1) INICIO / HOME

**Referencias:** Entregable, páginas 6–14 (capturas “Actual”, comparativa “Propuesta” y sistema de diseño); Feedback, página 1.

**Lo que muestra la propuesta de rediseño del Entregable:** cabecera limpia, saludo, selector de semana, métricas compactas, accesos rápidos, tarjeta de próximo entrenamiento con imagen discreta, navegación inferior más clara. El documento pide **mantener** calendario, progreso, estadísticas, cuenta Free, accesos, próximo entrenamiento y navegación.

**Observaciones posteriores específicas:**

1. Colocar el indicador real del plan (`Cuenta Free`, trial o plan contratado) y la acción existente **«Ver planes» agrupados cerca del saludo**, antes de la sección “Esta semana”, sin mezclarlos con el bloque de entrenamiento. **No hardcodear** nombre de plan ni saltarse validación/flujo de suscripción.
2. En la tarjeta de próximo entrenamiento (ejemplo visual: “Push competitivo”), incorporar una imagen oscura/de bajo contraste alusiva al ejercicio, persona entrenando o barra con discos, **solo si existe asset apropiado y licenciado**. Preservar texto legible con overlay y fallback sin imagen.
3. Aplicar la limpieza de jerarquía de la maqueta *solo donde sea necesaria*: tarjetas estadísticas contenidas, acciones bien separadas, próximo entrenamiento visible y CTA correcto. **No reconstruir** cabecera, navegación y calendario si ya funcionan y son coherentes.

**Aceptación:** plan/CTA arriba; estadísticas y entreno legibles; ni navegación ni comportamiento de planes cambian; sin pérdida de datos.

### 2) INICIAR ENTRENO / SELECCIÓN DE FOCO E INTENSIDAD

**Referencias:** Entregable, páginas 15–22 (comparativa con propuesta premium y texto de especificación); Feedback, página 1.

**Diseño del Entregable (adaptación mínima):** sustituir grandes superficies moradas por fondo oscuro y tarjetas independientes **solo si siguen existiendo**; resumen últimas sesiones discreto; las opciones de plantilla `Push`, `Pull`, `Legs`, `Upper`, `Lower`, `Full`, `Glutes`, `Chest+`, `Back+`, `Core` pueden mostrarse en cuadrícula compacta de tres columnas **si no altera el flujo actual ni requiere reescritura**; conservar nombre editable de sesión, duración personalizada, intensidad y CTA “Empezar ahora” visible/ancho suficiente.

**Feedback específico:**

1. **Imagen del ejercicio al pulsar su tarjeta.** Auditar qué son los recuadros reales: si son *plantillas/focos* (Push, Pull, etc.), **no representarlos falsamente como un ejercicio concreto**. Si se trata de ejercicios identificados con un `imageUri`/asset en catálogo, abrir el detalle/preview ya existente o un modal ligero reutilizable, sin sustituir la selección funcional. Si no hay relación fiable imagen-ejercicio, dejar constancia y preservar el funcionamiento actual.
2. **Intensidad, `%1RM` y repeticiones sugeridas:** mostrar información orientativa relacionada con la intensidad seleccionada **solo si existe mapeo confirmado** en código o por el cliente. El cliente cita `Media 60–80% RM` como **ejemplo**, no como tabla aprobada. No inventar rangos Suave/Alta ni número de repeticiones, ni alterar estimación de 1RM. Si existen porcentajes personalizables, utilizar los datos reales válidos y evitar contradicciones de categoría; si faltan, registrar pendiente de confirmación.
3. Acomodar el botón “Empezar ahora” para no solapar nuevas etiquetas; mantener su `onPress`, estados, validaciones y navegación.

**Aceptación:** mismo inicio de sesión, duración e intensidad; cero porcentajes inventados; preview cuando haya asset válido; CTA accesible.

### 3) HISTORIAL DE ENTRENOS / PROGRESO / RÉCORDS

**Referencias:** Entregable, sección de rediseño de Historial en páginas aproximadas 23–31 (texto sobre tabs, gráficos, récords, siluetas anatómicas e imágenes comparativas); Feedback, página 2.

**Propuesta del Entregable:** organizar en `Resumen / Sesiones / Rutinas`, indicadores `Volumen total / Repeticiones totales / Mejor 1RM estimado`, gráfica semanal separada, foco predominante, récords en tarjetas limpias y vista previa con “Ver todos”. El propio texto solicita **mantener cálculos existentes**, navegación y evitar que el botón flotante tape contenido.

**Integración prudente:**

1. **Prioridad inmediata:** reducir saturación en los récords. Cada ítem muestra por defecto nombre de ejercicio (y señal accesible de expandir), y revela al tocarlo el **mismo detalle existente**: peso, series/repeticiones, fecha, rango/clasificación elite, 1RM estimado, estado y barra de progreso *cuando ya existan*. Usar acordeón local/reutilizable. No perder datos ni acciones.
2. **Motivación contextual:** donde el cálculo existente muestre aumento positivo real de volumen frente a periodo comparable (p. ej. +360 kg en captura), mostrar “¡Felicidades!” o “¡Sigue así!”. No motivar falsamente si no hay datos, son incomparables o el cambio es cero/negativo.
3. **Tarjetas de resumen y gráfico:** si los datos y estructuras YA existen, aplicar disposición premium y separar visualmente gráfico/estadísticas; conservar periodos, filtros, lógica y unidades. No inventar indicadores, series, comparaciones ni endpoints.
4. **Pestañas Resumen / Sesiones / Rutinas:** si ya están implementadas, pulirlas según imagen; si no están, **NO crear un nuevo sistema de tabs como parte del ajuste menor** sin informar que amplía alcance y pedir autorización. Preferir agrupación/colapso local manteniendo rutas existentes.
5. **Foco muscular predominante, nuevos gráficos, iconos anatómicos y «Ver todos»:** solo integrar si existen datos y navegación suficientes; no crear estadísticas derivadas no auditadas ni herramientas gráficas nuevas en este encargo. Registrar como mejora ampliada pendiente.

**Aceptación:** récords compactos pero completos al desplegar; cálculos iguales; mensaje motivacional correcto; nada queda tapado por FAB/tab bar.

### 4) COMUNIDAD / GIMNASIOS DISPONIBLES / GIMNASIO PRINCIPAL / DETALLE

**Referencias:** Entregable, sección “03 · Red de gimnasios” y sus maquetas (aproximadamente página 34 en adelante); Feedback, página 3.

**Propuesta del Entregable:** comunidad como feed limpio (avatar, nombre, fecha, contenido, interacciones), gimnasios disponibles como filas compactas con nombre/localización, búsqueda por nombre/comuna, separación de entrenamientos recientes; detalle con check-in principal turquesa, abrir mapas secundario, estados vacíos legibles.

**Feedback posterior concreto:**

1. En las tarjetas de sección del gimnasio principal, mantener contraste visual **azul-negro**: exterior/superficie azul profundo e interior de tarjetas grafito/negro, respetando reglas premium (evitar fondo azul saturado en toda la pantalla). **Añadir una corona discreta** junto al título “Tu gimnasio principal”, sin reemplazar indicadores funcionales como la estrella.
2. Conservar selección de gimnasio principal, ubicación, botón “Abrir en mapas”, check-in y flujo GPS (sin cambios funcionales).
3. Si el feed, buscador, disposición de filas, estados vacíos o jerarquía de botones **ya existen**, ajustar espaciados y estilos locales para asemejarlos a las capturas. **Si implementar buscador por comuna, nueva lista, nuevo feed o datos de interacción exige endpoints, filtros o reglas nuevas, no hacerlo automáticamente**: reportar su alcance como mejora ampliada.

**Aceptación:** contraste uniforme y corona; funciones de gimnasio/check-in intactas; acción principal clara; no se pierde la información del centro.

### 5) DETALLE DE ENTRENO / MÚSCULOS A TRABAJAR

**Referencias:** Feedback, página 3; Entregable, notas de iconografía anatómica/SVG en la propuesta de Historial.

1. Revisar si existe silueta anatómica frontal/posterior o iconos SVG asociados a los grupos musculares. Cuando el usuario selecciona un grupo como “cuádriceps”, resaltar **la zona correcta** en azul/verde de acento mediante estado visual local, **solo con correspondencias verificadas**. Preferir un recurso vectorial reutilizable y consistente; no inventar anatomía ni descargar gráficos sin verificar licencia de uso comercial.
2. Si faltan recursos o mapa válido, no instalar nuevas librerías ni implementar un sistema anatómico desde cero. Dejar especificación y dependencia pendiente, conservando etiquetas e información actual.
3. Ocultar el **bloque inferior verdaderamente duplicado** “músculos a trabajar” (si repite exactamente etiquetas ya visibles arriba). No eliminar datos, componentes compartidos, atributos de ejercicio ni contenido único.

**Aceptación:** ningún músculo se representa erróneamente; información duplicada se oculta solo en esta vista; el resto del detalle sigue siendo funcional.

---

## Priorización y control de alcance

### Prioridad A — implementar automáticamente SI no está resuelto y el diff es localizado
- Agrupar plan/Ver planes arriba en Home.
- Mejoras ligeras de espaciados, contraste y orden de tarjetas según estilo ya existente.
- Mensaje motivacional únicamente ante incremento positivo real.
- Acordeón de récords que conserve íntegro el detalle.
- Corona decorativa en gimnasio principal y contraste exterior/interior localizado.
- Quitar bloque de músculos verdaderamente duplicado sin borrar datos.
- Previsualizar imagen de ejercicio cuando ya existan asociación y recursos válidos.
- Ajustar CTA «Empezar ahora» sin modificar lógica.

### Prioridad B — implementar solo si ya hay componentes, datos y assets listos
- Foto del próximo entrenamiento con derechos comerciales comprobados.
- Adaptación mínima a cuadrícula, tarjetas segmentadas y composición de las maquetas premium.
- Indicadores de porcentaje 1RM y repeticiones con parámetros aprobados.
- Mapa muscular con SVG y mapeo anatómico ya disponible.
- Pulir tabs/estadísticas/foco del historial si la funcionalidad real ya lo soporta.
- Limpieza de feed, buscador y gimnasio cuando estén resueltos en código.

### Prioridad C — detener y pedir aprobación por posible ampliación
- Crear desde cero pestañas/rutas de Historial, indicadores nuevos o cálculos de volumen predominante.
- Incorporar una nueva galería de ejercicios, banco completo de imágenes o editor de assets.
- Crear ilustraciones anatómicas interactivas de cero.
- Incorporar buscador con lógica o fuentes de datos nuevas.
- Modificar backend, API, esquema o contratos.

## Orden de ejecución obligatorio

**PASO 1 — AUDITORÍA SIN MODIFICAR CÓDIGO.** Entregar una tabla:

| ID | Pantalla | Solicitud y documento/página | ¿Ya está en código? | Archivo/componente real | Riesgo | Acción mínima | Prioridad |
|---|---|---|---|---|---|---|---|

Revisar componentes compartidos, tema, librerías, imágenes, rutas, servicios, caches y tests. Distinguir *captura actual*, *imagen conceptual* y *funcionalidad implementada*. Identificar cambios que ya estén resueltos para excluirlos del trabajo.

**PASO 2 — PLAN DE MODIFICACIONES PEQUEÑAS.** Agrupar commits o cambios por pantalla y justificar cada archivo. Verificar que no se rompan otras pantallas por estilos compartidos. **Antes de implementar cualquier punto C, detener y pedir autorización.** No detener los puntos A/B independientes por requisitos pendientes de C.

**PASO 3 — IMPLEMENTAR SOLO CAMBIOS APROBADOS POR LAS REGLAS.** Preservar estado real, fetch, caché, navegación, validación, traducciones existentes y roles. Nunca simular endpoints o inventar datos de usuario.

**PASO 4 — VALIDAR.** Ejecutar los scripts ya definidos en el repo: lint, typecheck, test, build cuando aplique. Comprobar al menos: home en cuenta free/trial/paga; plan CTA; iniciar entreno con distintas plantillas/intensidades y duración personalizada; historial vacío, registros extensos, variación semanal positiva/cero/negativa; expansión de récords; gimnasio principal, mapas y check-in; grupos musculares con/sin recurso visual; iOS/Android o simulación disponible; tamaños pequeños, scroll y safe area. Si no es posible ejecutar alguna prueba, indicarlo.

**PASO 5 — ENTREGABLE DE DESARROLLO.** Responder en español con: diagnóstico previo, modificaciones exactas y archivos, funcionalidades preservadas, pruebas con resultado real, observaciones no implementadas y causa, dependencias o confirmaciones solicitadas al cliente, riesgos residuales y sugerencia de capturas antes/después.

## Criterios finales de éxito

1. La nueva presentación se reconoce como una evolución **premium dark** de las imágenes de referencia del Entregable, pero NO implica sustituir toda la aplicación.
2. Se incorporan las observaciones del Feedback sin cambiar las reglas existentes del sistema.
3. El cambio está limitado a los componentes necesarios, evitando nuevos endpoints o modelos.
4. No hay pérdidas de campos/datos ni alteración de estadísticas, GPS, pagos, trial, membresías, rankings y registro de entrenamiento.
5. Cualquier dependencia de tabla 1RM, SVG, imágenes comerciales o alcance mayor se reporta **antes** de implementar algo especulativo.

**COMIENZA AHORA CON EL PASO 1: audita el repositorio, presenta la tabla de trazabilidad y el plan mínimo; después ejecuta únicamente cambios de prioridad A y los B comprobablemente seguros.**
