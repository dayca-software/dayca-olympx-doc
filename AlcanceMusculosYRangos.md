# OlympX MVP 2026 - Alcance de Musculos y Rangos de Fuerza

> Documento de alcance para revisar limites funcionales del catalogo muscular, el highlighter visual y los rangos de fuerza universales.

## 1. Objetivo

Definir con claridad que entra en el MVP para:
- Catalogo de musculos y relacion con ejercicios.
- Componente visual de highlighter corporal.
- Rangos de fuerza universales por ejercicio, sexo y 1RM estimado.

## 2. Problema Que Resuelve

El usuario necesita:
- Ver que musculos trabaja un ejercicio.
- Entender visualmente la activacion muscular con un componente reusable.
- Comparar su rendimiento con una base basada en evidencia.
- Ver su rango actual y el progreso hacia el siguiente nivel.

## 3. Alcance MVP

### 3.1 Catalogo muscular

Incluye:
- Catalogo normalizado de musculos o grupos musculares.
- Relacion entre ejercicio y musculo.
- Rol muscular por ejercicio: `primary`, `secondary`, `stabilizer`.
- Intensidad relativa por musculo.

### 3.2 Highlighter visual

Incluye:
- Componente reusable para pintar musculos trabajados.
- Vista frontal y posterior.
- Leyenda basica de colores.
- Estado solo lectura en MVP.

### 3.3 Rangos de fuerza universales

Incluye:
- Calculo de 1RM estimado.
- Clasificacion por ejercicio + sexo.
- Rangos: Bronze, Silver, Gold, Platinum, Diamond.
- Percentil aproximado dentro de la categoria.
- Distancia al siguiente rango.
- Tarjeta compartible y plantilla PDF simple.

## 4. Fuera De Alcance En MVP

- Highlighter interactivo editable por el usuario.
- Personalizacion avanzada de anatomia por entrenamientos particulares.
- Aprendizaje automatico de nuevos estandares desde data social.
- Rangos para ejercicios no incluidos en la lista inicial.
- Rankings territoriales por gimnasio para estos rangos.
- Version mobile offline del catalogo muscular.

## 5. Ejercicios Incluidos En MVP

- Press banca
- Sentadilla
- Peso muerto
- Dominadas
- Press militar
- Curl de biceps
- Fondos con lastre
- Curl isquiotibial
- Leg extension
- Hip thrust
- Jalon al pecho
- Remo barra libre

## 6. Dependencias Funcionales

- `M03` Biblioteca de Ejercicios.
- `M04` Rutinas y Registro de Entrenamiento.
- `M05` PRs, Progreso y Rankings.
- `M11` Rangos de Fuerza Universales.

## 7. Dependencias De Datos

- `Exercise` como entidad base.
- `Muscle` para normalizar grupos musculares.
- `ExerciseMuscleTarget` para relacion ejercicio-musculo.
- `ExerciseStrengthStandard` y `ExerciseStrengthStandardBand` para rangos.
- `TrainingSet` y `ExercisePR` para calcular 1RM y persistir progreso.

## 8. Regla De Producto

El alcance inicial prioriza ejercicios principales con evidencia suficiente. Los ejercicios mas simples o con menos data quedaran para post-MVP y podran nutrirse con data propia de la comunidad.

## 9. Criterio De Exito

El feature se considera listo cuando:
- El usuario puede ver los musculos principales de un ejercicio.
- El usuario puede ver su rango actual de fuerza por ejercicio.
- El sistema puede mostrar el progreso hacia el siguiente rango.
- El componente visual se puede reutilizar sin acoplar la UI al dominio.
