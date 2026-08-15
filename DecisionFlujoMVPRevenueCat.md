# OlympX MVP 2026 - Decision De Flujo Y Suscripciones

> Documento de continuidad de producto. Explica como debe evolucionar el flujo de entrenamiento, que queda en el MVP Core y como preparar monetizacion con RevenueCat sin chocar con el futuro.

## 1. Resumen Ejecutivo

OlympX va bien encaminado si prioriza el loop principal:

1. Autenticacion y perfil.
2. Gimnasio principal y contexto local.
3. Biblioteca de ejercicios.
4. Registro de sesiones y sets.
5. PRs, tonelaje e ისტორial.
6. Rangos de fuerza.

La capa social y de suscripcion premium debe construirse despues de validar este loop.

## 2. Decision De Producto

### Recomendacion principal

El flujo mas simple para usuarios no expertos es:

- Crear la sesion de entrenamiento.
- Registrar ejercicios y sets durante la sesion.
- Ver el resumen final al cerrar.

Esto evita formularios largos y hace que la app refleje el entrenamiento real.

### Lo que NO conviene hacer ahora

- No pedir al usuario que construya toda la sesion completa antes de empezar.
- No meter la capa social como protagonista del home.
- No mezclar monetizacion compleja con el flujo inicial de entrenamiento.

## 3. Como Continuar Sin Chocar Con El Futuro

### Regla de continuidad

Todo lo que se implemente ahora debe poder convivir con:

- Free
- Trial de 7 dias
- Paid

Y debe ser compatible con RevenueCat para el control de acceso premium.

### Implicaciones practicas

- Las pantallas de entrenamiento deben ser utiles aun en Free.
- El detalle de progreso debe existir antes del paywall.
- Las funciones premium deben agregarse como extensiones, no como base del flujo.

## 4. Riesgos Si Se Mezcla Todo Demasiado Pronto

| Riesgo | Impacto | Resultado |
|--------|---------|----------|
| Formularios largos en home | Alta friccion | Menor uso real |
| Monetizacion temprana sin valor | Baja conversion | Abandono de trial |
| Social antes del core | Scope creep | Producto mas caro y menos claro |
| Dependencia de logica de suscripcion en la UI | Difcil mantenimiento | Bugs de acceso y UX confusa |

## 5. Preparacion Para RevenueCat

RevenueCat sera la capa de monetizacion y entitlement para el plan Free/Trial/Paid.

### Decisiones recomendadas

- RevenueCat controla estado de suscripcion y acceso premium.
- El backend sigue siendo la fuente de verdad del dominio de entrenamiento.
- La UI consulta entitlements para desbloquear features premium.
- El acceso premium no debe romper el entrenamiento basico.

### Lo que conviene modelar desde ya

- `free`
- `trial`
- `paid_monthly`
- `paid_annual`
- `lifetime` si aparece mas adelante

### Lo que conviene evitar

- Logica de billing distribuida por toda la app.
- Estados de suscripcion hardcodeados en pantallas sueltas.
- Bloquear features core del entrenamiento con demasiada agresividad.

## 6. Impacto Tecnico Futuro

Para no chocar con RevenueCat, el producto debe mantener separadas estas capas:

| Capa | Responsabilidad |
|------|-----------------|
| UI | Presentar el flujo y el paywall |
| App state | Mantener sesion y preferencias locales |
| Backend | Guardar entrenos, PRs, historiales y progreso |
| RevenueCat | Entitlements, trial, paid, restauracion de compras |

## 7. Alcance Recomendado Ahora

### Entrenamiento

- Crear sesion en pantalla dedicada.
- Registrar sets, peso y repeticiones.
- Ver resumen de volumen y progreso.

### Premium futuro

- Rangos completos.
- Exportables.
- Comparaciones avanzadas.
- Capas sociales y de competencia extendidas.

## 8. Lo Que Falta Para Estar Solidos

- Más ejemplos musculares y de plantillas rápidas.
- Mejor jerarquia visual en entrenamiento.
- Resumen final de sesion mas claro.
- Definir el contrato de suscripcion con RevenueCat antes de cerrar la Fase 2.

## 9. Recomendacion Comercial

Presentar OlympX como:

> Una app de entrenamiento y progreso que primero resuelve el registro real de la sesion, y despues desbloquea comparacion, fuerza avanzada y monetizacion premium con RevenueCat.

## 10. Conclusión

La mejor ruta es seguir fortaleciendo el core de entrenamiento y dejar la monetizacion premium como una capa compatible con RevenueCat. Asi evitamos retrabajo y protegemos la experiencia base del usuario.
