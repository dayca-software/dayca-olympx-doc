# OlympX MVP 2026 - Coach Requerimientos

> Documento maestro del modulo de coach y acompanamiento de OlympX.
> Enfocado en motivacion, adherencia y habitos, sin terapia clinica ni consejo medico.
> Version: 1.0 · Fecha: Junio 2026

## 1. Objetivo

Definir el sistema de acompanamiento que ayuda al usuario a entrenar con mas constancia, mejor adherencia y mejor percepcion de progreso.

## 2. Alcance

Incluye:

- Mensajes de animo y refuerzo positivo.
- Nudges contextuales por inactividad o baja consistencia.
- Check-in pre-sesion simple.
- Metas semanales de adherencia.
- Personalizacion basica del tono.

Fuera de alcance:

- Diagnostico psicologico.
- Terapia clinica.
- Consejos medicos.
- Intervencion de crisis automatizada.

## 3. Prioridad

| Prioridad | Motivo                                                      |
| --------- | ----------------------------------------------------------- |
| Media     | Aumenta retencion y adherencia, pero no bloquea el MVP Core |

## 4. Requerimientos Funcionales

| ID      | Descripcion                                                              | Prioridad |
| ------- | ------------------------------------------------------------------------ | --------- |
| CRF-001 | Mostrar mensajes de animo antes, durante o despues del entrenamiento     | Media     |
| CRF-002 | Permitir registrar estado pre-sesion: animo, energia, estres, motivacion | Media     |
| CRF-003 | Generar sugerencias simples segun el estado del usuario                  | Media     |
| CRF-004 | Detectar inactividad o caida de consistencia y enviar nudges             | Media     |
| CRF-005 | Permitir definir metas semanales de adherencia                           | Media     |
| CRF-006 | Mostrar streaks, consistencia y cumplimiento de metas                    | Media     |
| CRF-007 | Permitir configurar el tono del coach: directo, motivador o neutral      | Baja      |
| CRF-008 | Permitir desactivar el coach por completo                                | Alta      |

## 5. Reglas de Negocio

| ID      | Regla                                                                   | Excepcion |
| ------- | ----------------------------------------------------------------------- | --------- |
| CRN-001 | El coach no puede emitir diagnosticos ni interpretaciones clinicas      | Ninguna   |
| CRN-002 | Las sugerencias del coach son orientativas, no obligatorias             | Ninguna   |
| CRN-003 | El usuario puede desactivar el coach en cualquier momento               | Ninguna   |
| CRN-004 | El coach debe usar datos de producto minimos y relevantes               | Ninguna   |
| CRN-005 | El sistema no debe generar spam ni repetir mensajes identicos en exceso | Ninguna   |

## 6. Requerimientos No Funcionales

| ID       | Descripcion                                               | Mettrica          |
| -------- | --------------------------------------------------------- | ----------------- |
| CRNF-001 | El coach debe respetar privacidad y minimizacion de datos | Data minimization |
| CRNF-002 | Los mensajes deben aparecer sin friccion perceptible      | < 2s p95          |
| CRNF-003 | La desactivacion no debe borrar historial                 | 100%              |

## 7. Criterios De Aceptacion

| ID      | Criterio                                              | Validacion            |
| ------- | ----------------------------------------------------- | --------------------- |
| CCA-001 | El usuario ve mensajes de animo y sugerencias simples | Mensaje visible       |
| CCA-002 | El usuario puede registrar su estado pre-sesion       | Datos persistidos     |
| CCA-003 | El usuario puede desactivar el coach                  | Preferencia guardada  |
| CCA-004 | El sistema no emite contenido clinico o medico        | Revision de contenido |

## 8. Casos Borde

| ID      | Escenario                          | Comportamiento esperado    |
| ------- | ---------------------------------- | -------------------------- |
| CCB-001 | Usuario desactiva el coach         | Deja de enviar mensajes    |
| CCB-002 | Falta contexto suficiente          | Mostrar sugerencia neutral |
| CCB-003 | Mensaje reportado como inapropiado | Se oculta y queda registro |
| CCB-004 | Inactividad prolongada             | Nudging suave, no agresivo |

## 9. Trazabilidad

| Necesidad del cliente | Resultado esperado                 |
| --------------------- | ---------------------------------- |
| Apoyo y motivacion    | Refuerzo positivo y nudges         |
| Mejora de adherencia  | Metas y consistencia visibles      |
| Control del tono      | Acompanamiento configurable        |
| Seguridad de producto | Sin diagnostico ni consejo clinico |

## 10. Tipos De Notificaciones Del Coach

| ID      | Tipo                        | Cuándo se dispara                       | Objetivo              |
| ------- | --------------------------- | --------------------------------------- | --------------------- |
| CNT-001 | Refuerzo positivo           | Al cerrar una sesión o registrar un PR  | Reforzar conducta     |
| CNT-002 | Nudge de inactividad        | Tras varios días sin entrenar           | Recuperar adherencia  |
| CNT-003 | Check-in pre-sesión         | Antes de iniciar entrenamiento          | Contextualizar estado |
| CNT-004 | Meta semanal                | Al inicio de semana o al fijar una meta | Dar foco              |
| CNT-005 | Streak alert                | Al acercarse a romper una racha         | Evitar abandono       |
| CNT-006 | Recuperación suave          | Luego de una caída de consistencia      | Volver sin culpa      |
| CNT-007 | Celebración de consistencia | Al cumplir una meta semanal o mensual   | Mantener motivación   |

## 11. Mensajes Base

| Situación              | Mensaje base                                                     |
| ---------------------- | ---------------------------------------------------------------- |
| PR nuevo               | "Nuevo PR. Hoy ganaste una batalla."                             |
| Sesion completada      | "Buen trabajo. La constancia suma mas que la perfeccion."        |
| 3 dias sin entrenar    | "Hace unos dias no entrenas. Volver suave tambien cuenta."       |
| Energia baja           | "Hoy toca una sesion inteligente, no heroica."                   |
| Meta cumplida          | "Objetivo cumplido. Vas construyendo ritmo."                     |
| Racha en riesgo        | "Tu racha sigue viva. Un paso mas y la mantienes."               |
| Cumplimiento semanal   | "Semana cerrada. Tu progreso sigue en marcha."                   |
| Perfil nuevo sin datos | "Empieza con una sesion simple y dejemos que el progreso hable." |

## 12. Personalidad Y Tono

| Estilo    | Descripcion                   | Uso recomendado                         |
| --------- | ----------------------------- | --------------------------------------- |
| Directo   | Corto, claro, sin adornos     | Usuarios que quieren foco               |
| Motivador | Enfasis en progreso y orgullo | Usuarios que responden a refuerzo       |
| Neutral   | Tono sobrio, cero presion     | Usuarios que no quieren carga emocional |

### Reglas De Voz

- Hablar en segunda persona.
- Evitar culpa, vergüenza o lenguaje manipulador.
- Priorizar claridad y accion simple.
- No sobrecargar con mensajes repetidos.
- Ajustar el tono segun la preferencia del usuario.

## 13. Disparadores

| ID     | Disparador        | Condicion                                              | Accion                        |
| ------ | ----------------- | ------------------------------------------------------ | ----------------------------- |
| CT-001 | Fin de sesion     | El usuario guarda una rutina o cierra un entrenamiento | Enviar refuerzo positivo      |
| CT-002 | PR nuevo          | Se registra una nueva marca personal                   | Enviar celebracion            |
| CT-003 | Estado pre-sesion | El usuario completa animo, energia o motivacion        | Sugerir tipo de sesion        |
| CT-004 | Inactividad corta | 3 dias sin entrenar                                    | Enviar nudge suave            |
| CT-005 | Inactividad media | 7 dias sin entrenar                                    | Enviar recordatorio mas claro |
| CT-006 | Racha en riesgo   | Falta 1 sesion para romper streak                      | Enviar alerta de continuidad  |
| CT-007 | Meta cumplida     | El usuario completa su meta semanal                    | Enviar celebracion            |
| CT-008 | Meta incumplida   | Cierra la semana sin cumplir meta                      | Enviar recuperacion suave     |

## 14. Frecuencia Y Control De Spam

| Regla                              | Limite                                   |
| ---------------------------------- | ---------------------------------------- |
| Nudges por dia                     | Maximo 1 por dia                         |
| Mensajes motivacionales por semana | Maximo 3 por semana                      |
| Alertas de racha                   | Solo una por evento                      |
| Mensajes nocturnos                 | No enviar entre 22:00 y 08:00 hora local |
| Repeticion de contenido            | No repetir el mismo mensaje en 14 dias   |

### Regla De Entrega

- Si existe una notificacion de producto de mayor prioridad, el coach no la reemplaza.
- El coach se apoya en el sistema de notificaciones existente, pero mantiene su propia logica de decision.

## 15. Preferencias Del Usuario

| Preferencia         | Valores                          | Efecto                                |
| ------------------- | -------------------------------- | ------------------------------------- |
| Coach activo        | Si / No                          | Habilita o deshabilita todo el modulo |
| Tono                | Directo / Motivador / Neutral    | Ajusta el estilo de los mensajes      |
| Nudges              | Bajas / Medias / Fuertes         | Ajusta intensidad de recordatorios    |
| Horario de mensajes | Libre / Solo dia / Personalizado | Limita cuando puede notificar         |
| Metas semanales     | Activadas / Desactivadas         | Habilita seguimiento de objetivos     |

### Regla De Privacidad

- Las preferencias del coach siempre son editables por el usuario.
- Si el usuario desactiva el coach, solo quedan activos los eventos funcionales de producto que no dependan de este modulo.
