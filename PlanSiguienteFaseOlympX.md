# OlympX MVP 2026 - Plan Siguiente Fase

> Hoja de ruta para cerrar el MVP sin perder foco en entrenamiento, social y monetizacion ligera.

## 1. Objetivo De Esta Fase

Cerrar el loop principal de entrenamiento y dejar la experiencia lista para validacion real con usuarios.

El orden recomendado es:

1. Endurecer autenticacion y perfil.
2. Completar la experiencia de entrenamiento con detalles y sets.
3. Reducir friccion en home, busqueda y ranking.
4. Cubrir flujos criticos con tests.
5. Preparar monetizacion compatible con RevenueCat.

## 2. Principios De Ejecucion

- El home debe ser panel, no formulario.
- El flujo de entrenamiento debe vivir en pantallas dedicadas.
- El entrenamiento basico siempre debe funcionar en Free.
- La monetizacion premium debe agregarse como capa, no como barrera del core.
- Todo nuevo UX debe ser entendible por usuarios no expertos.

## 3. Prioridades

### P0 - Imprescindible

- Agregar tests basicos de mobile y API para flujos criticos.
- Mejorar la resiliencia offline y estados vacios en mobile.
- Mantener Home limpio y con CTA hacia el entrenamiento.

### P1 - Alto valor

- Mostrar PRs y progreso de forma mas visible.
- Conectar mejor el historial con el detalle.
- Agregar cache local para summary y listados.
- Definir limites Free/Paid sin afectar el core.

### P2 - Preparacion comercial

- Integracion conceptual con RevenueCat.
- Modelar entitlements para Free / Trial / Paid.
- Definir paywall futuro sin bloquear entrenamiento basico.

## 4. Roadmap Recomendado

### Bloque 1 - Flujo de Entrenamiento

Entregables:

- `TrainingSessionCreateScreen` pulida.
- Seleccion de plantilla rapida.
- Seleccion de zonas musculares mas clara.
- Campos guiados y mas amigables.

### Bloque 2 - Registro Durante La Sesion

Entregables:

- Registro de ejercicios por sesion.
- Sets con peso y repeticiones.
- Opciones avanzadas solo bajo demanda.
- Carga automatica del ultimo set como ayuda.

### Bloque 3 - Resumen Y Progreso

Entregables:

- Resumen de sets, volumen y promedio.
- Vista clara de progreso por ejercicio.
- Base para PRs y tonelaje.

### Bloque 4 - Monetizacion Preparada

Entregables:

- Definir plan Free / Trial / Paid.
- Preparar estados de suscripcion compatibles con RevenueCat.
- Separar UI de billing del dominio de entrenamiento.

## 5. Riesgos Si No Se Sigue Este Orden

| Riesgo | Consecuencia |
|-------|--------------|
| Mezclar social temprano | El producto se ve cargado y pierde foco |
| Meter billing antes del core | Friccion y peor conversion |
| Formularios largos en mobile | Abandono del flujo de entrenamiento |
| No separar entreno y suscripcion | Dificil evolucion futura con RevenueCat |

## 6. Dependencias Futuras Con RevenueCat

RevenueCat debe entrar cuando existan estos conceptos estables:

- plan Free
- trial de 7 dias
- plan Paid
- features premium definidas
- features core totalmente funcionales

### Regla de implementacion

RevenueCat controla acceso premium, pero no la logica de entrenamiento.

La app debe poder:

- crear entrenos en Free
- guardar progreso en Free
- mostrar limite premium de forma clara
- desbloquear premium sin romper sesiones existentes

## 7. Decision De Producto

La recomendacion es continuar con la ruta:

- entrenamiento primero
- progreso despues
- monetizacion luego
- social al final del core

## 8. Siguiente Paso Recomendado

1. Agregar tests smoke de auth, home y training.
2. Introducir cache local para reducir carga inicial.
3. Definir el paquete minimo de Free vs Paid.
