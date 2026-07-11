# OlympX MVP 2026 - Admin Requerimientos

> Documento maestro de requerimientos del panel interno de administracion de OlympX.
> Enfocado en operacion, moderacion, soporte y control del sistema.
> Version: 1.0 · Fecha: Junio 2026

## 1. Objetivo

Definir el panel admin que el equipo interno necesita para operar OlympX sin depender del frontend publico ni de procesos manuales dispersos.

## 2. Alcance

El panel admin cubre:

- Acceso seguro para roles internos.
- Visibilidad operativa del sistema.
- Gestion de usuarios, gimnasios y catalogos base.
- Moderacion de reportes y contenido.
- Control de estados y acciones de soporte.

Fuera de alcance inicial:

- Billing avanzado.
- BI completo.
- Automatizacion de moderacion con IA.
- Flujos publicos de cliente final.

## 3. Priorizacion MoSCoW

| Prioridad   | Alcance                                                                                                   | Motivo                                  |
| ----------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| Must have   | Auth admin, dashboard operativo, gestion de usuarios, moderacion de reportes, gestion basica de gimnasios | Sin esto no hay control interno minimo  |
| Should have | Gestion de ejercicios, rangos de fuerza, estados de contenido                                             | Reduce friccion operativa               |
| Could have  | KPIs de negocio, exportes CSV, auditoria avanzada                                                         | Valor adicional para soporte y analisis |
| Won't have  | BI externo, automatizacion con IA, permisos granulares complejos                                          | No necesario para el MVP administrativo |

## 4. Matriz Valor Vs Esfuerzo

| Iniciativa                       | Valor    | Esfuerzo | Prioridad |
| -------------------------------- | -------- | -------- | --------- |
| Login admin y proteccion de ruta | Alto     | Bajo     | Muy alta  |
| Dashboard operativo              | Alto     | Medio    | Muy alta  |
| Gestion de usuarios              | Alto     | Medio    | Muy alta  |
| Moderacion de reportes           | Muy alto | Medio    | Muy alta  |
| Gestion basica de gimnasios      | Alto     | Medio    | Alta      |
| Gestion de ejercicios            | Medio    | Medio    | Media     |
| Gestion de rangos                | Medio    | Medio    | Media     |
| Exportes y auditoria             | Medio    | Alto     | Baja      |

## 5. Requerimientos Funcionales

### M01 - Autenticacion y Acceso

| ID      | Descripcion                                                                         | Prioridad | Dependencias |
| ------- | ----------------------------------------------------------------------------------- | --------- | ------------ |
| ARF-001 | El sistema debe permitir iniciar sesion solo a usuarios con rol admin o super_admin | Critica   | -            |
| ARF-002 | El sistema debe proteger todas las rutas admin con autenticacion persistida         | Critica   | ARF-001      |
| ARF-003 | El sistema debe permitir cerrar sesion y limpiar credenciales locales               | Alta      | ARF-001      |

### M02 - Dashboard Operativo

| ID      | Descripcion                                                                                                     | Prioridad | Dependencias |
| ------- | --------------------------------------------------------------------------------------------------------------- | --------- | ------------ |
| ARF-004 | El sistema debe mostrar indicadores base: usuarios, gimnasios, sesiones, reportes pendientes y usuarios activos | Alta      | ARF-001      |
| ARF-005 | El sistema debe mostrar alertas operativas de bajo inventario de moderacion, errores o incidencias abiertas     | Media     | ARF-004      |
| ARF-006 | El sistema debe mostrar estado de salud resumido de la plataforma                                               | Media     | ARF-004      |

### M03 - Gestion de Usuarios

| ID      | Descripcion                                                                                | Prioridad | Dependencias |
| ------- | ------------------------------------------------------------------------------------------ | --------- | ------------ |
| ARF-007 | El sistema debe permitir buscar usuarios por nickname, email o id                          | Alta      | ARF-001      |
| ARF-008 | El sistema debe mostrar el detalle de usuario con perfil, gimnasio, PRs y actividad basica | Alta      | ARF-007      |
| ARF-009 | El sistema debe permitir desactivar o suspender una cuenta de usuario                      | Alta      | ARF-008      |
| ARF-010 | El sistema debe permitir reactivar una cuenta suspendida                                   | Media     | ARF-009      |
| ARF-011 | El sistema debe registrar la razon de cada accion administrativa sobre un usuario          | Alta      | ARF-009      |

### M04 - Gestion de Gimnasios

| ID      | Descripcion                                                                                      | Prioridad | Dependencias |
| ------- | ------------------------------------------------------------------------------------------------ | --------- | ------------ |
| ARF-012 | El sistema debe permitir crear, editar y desactivar gimnasios                                    | Alta      | ARF-001      |
| ARF-013 | El sistema debe permitir gestionar nombre, direccion, latitud, longitud, cadena, ciudad y region | Alta      | ARF-012      |
| ARF-014 | El sistema debe permitir marcar un gimnasio como verificado o pendiente de revision              | Media     | ARF-012      |

### M05 - Moderacion y Reportes

| ID      | Descripcion                                                         | Prioridad | Dependencias |
| ------- | ------------------------------------------------------------------- | --------- | ------------ |
| ARF-015 | El sistema debe mostrar reportes pendientes de usuarios o contenido | Critica   | ARF-001      |
| ARF-016 | El sistema debe permitir aprobar, rechazar o cerrar reportes        | Critica   | ARF-015      |
| ARF-017 | El sistema debe permitir registrar observaciones de moderacion      | Alta      | ARF-016      |
| ARF-018 | El sistema debe permitir ver historial de acciones de moderacion    | Alta      | ARF-016      |

### M06 - Catalogos Base

| ID      | Descripcion                                                                  | Prioridad | Dependencias |
| ------- | ---------------------------------------------------------------------------- | --------- | ------------ |
| ARF-019 | El sistema debe permitir revisar catalogo de ejercicios                      | Alta      | ARF-001      |
| ARF-020 | El sistema debe permitir activar o desactivar ejercicios competitivos        | Media     | ARF-019      |
| ARF-021 | El sistema debe permitir revisar rangos de fuerza y su estado de publicacion | Media     | ARF-019      |

### M07 - Gestion Comercial

| ID      | Descripcion                                                                                                                   | Prioridad | Dependencias     |
| ------- | ----------------------------------------------------------------------------------------------------------------------------- | --------- | ---------------- |
| ARF-022 | El sistema debe permitir crear, editar y desactivar planes comerciales                                                        | Critica   | ARF-001          |
| ARF-023 | El sistema debe permitir configurar precio mensual, precio anual y moneda por plan                                            | Critica   | ARF-022          |
| ARF-024 | El sistema debe permitir definir limites por plan: sesiones, gimnasios, ejercicios, exportes, comparticion y features premium | Alta      | ARF-022          |
| ARF-025 | El sistema debe permitir activar o desactivar trials                                                                          | Alta      | ARF-022          |
| ARF-026 | El sistema debe permitir configurar duracion de trial y si requiere tarjeta                                                   | Alta      | ARF-025          |
| ARF-027 | El sistema debe permitir gestionar cupones y codigos promocionales                                                            | Media     | ARF-022          |
| ARF-028 | El sistema debe permitir ver suscripciones activas, canceladas y vencidas                                                     | Critica   | ARF-022          |
| ARF-029 | El sistema debe permitir forzar cancelacion, reactivacion o extension manual de una suscripcion                               | Alta      | ARF-028          |
| ARF-030 | El sistema debe mostrar KPIs comerciales basicos: MRR, churn, conversion a paid, trial-to-paid, ARPU                          | Alta      | ARF-028          |
| ARF-031 | El sistema debe permitir registrar cambios historicos de precio y plan para auditoria                                         | Alta      | ARF-022          |
| ARF-032 | El sistema debe permitir configurar un cupo maximo de nuevas altas Free                                                       | Critica   | ARF-022          |
| ARF-033 | El sistema debe redirigir nuevas altas al trial de 7 dias cuando el cupo Free este agotado                                    | Critica   | ARF-032, ARF-026 |

## 6. Reglas de Negocio

| ID      | Regla                                                                                                       | Excepcion                                           |
| ------- | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| ARN-001 | Solo roles internos pueden acceder al admin                                                                 | Ninguna                                             |
| ARN-002 | Toda accion de suspension, reactivacion o moderacion debe quedar auditada                                   | Ninguna                                             |
| ARN-003 | Un gimnasio desactivado no se elimina fisicamente si tiene historial asociado                               | Se mantiene para trazabilidad                       |
| ARN-004 | Los reportes no deben resolverse automaticamente en el MVP                                                  | Revision manual obligatoria                         |
| ARN-005 | Los cambios sobre catalogos base deben ser reversibles                                                      | Reversion por auditoria                             |
| ARN-006 | Los cambios de precio y plan deben quedar con version historica                                             | Ninguna                                             |
| ARN-007 | Un trial activo solo puede existir una vez por cuenta y por tarjeta                                         | Reintento permitido solo si el trial no se consumio |
| ARN-008 | Una suscripcion cancelada mantiene acceso hasta la fecha de corte                                           | Ninguna                                             |
| ARN-009 | El plan Free debe respetar limites maximos definidos por configuracion comercial                            | Ninguna                                             |
| ARN-010 | Cualquier cambio en limites Free debe aplicarse sin romper datos historicos                                 | Requiere versionado                                 |
| ARN-011 | El cupo de nuevas altas Free solo afecta registros nuevos, no usuarios existentes                           | Ninguna                                             |
| ARN-012 | Si el cupo Free se agota, el flujo comercial debe ofrecer trial de 7 dias como unica alternativa de entrada | Ninguna                                             |

## 7. Requerimientos No Funcionales

| ID       | Descripcion                                                                             | Mettrica         |
| -------- | --------------------------------------------------------------------------------------- | ---------------- |
| ARNf-001 | El panel debe cargar en menos de 2 segundos en 4G para dashboards simples               | < 2s p95         |
| ARNf-002 | El acceso admin debe requerir token valido y rol autorizado                             | 100%             |
| ARNf-003 | La UI debe ser responsiva para desktop y tablet                                         | Layout adaptable |
| ARNf-004 | El sistema debe guardar audit log de acciones criticas                                  | 100%             |
| ARNf-005 | El panel debe mantener consistencia con el envelope de API ADR-005                      | 100%             |
| ARNf-006 | El modulo comercial debe mostrar precios y estados correctamente en menos de 2 segundos | < 2s p95         |

## 8. Criterios De Aceptacion

| ID      | Criterio                                                                | Validacion                       |
| ------- | ----------------------------------------------------------------------- | -------------------------------- |
| ACA-001 | Un usuario sin rol admin no puede acceder al panel                      | Redireccion o bloqueo            |
| ACA-002 | Un admin puede ver el dashboard operativo                               | KPIs visibles                    |
| ACA-003 | Un admin puede suspender y reactivar un usuario                         | Estado persistido                |
| ACA-004 | Un admin puede resolver reportes manualmente                            | Accion registrada                |
| ACA-005 | Un admin puede crear o editar gimnasios                                 | Datos guardados                  |
| ACA-006 | Toda accion critica genera registro auditable                           | Log disponible                   |
| ACA-007 | Un admin puede crear, editar y desactivar planes                        | Plan persistido                  |
| ACA-008 | Un admin puede configurar precios, trials y cupones                     | Configuracion visible            |
| ACA-009 | Un admin puede ver suscripciones y sus estados                          | Listado disponible               |
| ACA-010 | Un admin puede consultar KPIs comerciales basicos                       | MRR, churn y conversion visibles |
| ACA-011 | Un admin puede modificar los limites del plan Free                      | Valores persistidos              |
| ACA-012 | Un admin puede ver claramente que features quedan bloqueadas en Free    | Matriz de limites visible        |
| ACA-013 | Un admin puede configurar el cupo maximo de nuevas altas Free           | Cupo persistido                  |
| ACA-014 | Al agotarse el cupo Free, el registro nuevo solo ofrece trial de 7 dias | Flujo bloqueado para Free        |

## 9. Casos Borde

| ID      | Escenario                                                          | Comportamiento esperado                                           |
| ------- | ------------------------------------------------------------------ | ----------------------------------------------------------------- |
| ACB-001 | Token expirado                                                     | Cerrar sesion y pedir login                                       |
| ACB-002 | Usuario sin permisos                                               | Denegar acceso                                                    |
| ACB-003 | Reporte ya resuelto                                                | Informar estado y evitar doble accion                             |
| ACB-004 | Gimnasio duplicado                                                 | Bloquear guardado                                                 |
| ACB-005 | Error al guardar una accion administrativa                         | Mostrar error y no cambiar estado                                 |
| ACB-006 | Se intenta cambiar el precio de un plan con suscripciones activas  | Guardar nueva version sin romper historico                        |
| ACB-007 | Se desactiva un plan con suscriptores activos                      | Mantener acceso hasta vencimiento                                 |
| ACB-008 | Coupon expirado o invalido                                         | Rechazar aplicacion                                               |
| ACB-009 | Trial ya consumido                                                 | Bloquear nuevo trial                                              |
| ACB-010 | Se reduce el limite Free por debajo del uso historico del usuario  | Mantener historial y aplicar nuevo limite solo hacia adelante     |
| ACB-011 | Se intenta habilitar una feature premium en Free sin configuracion | Bloquear y mostrar advertencia                                    |
| ACB-012 | Se agota el cupo Free mientras un usuario esta registrandose       | Ofrecer solo trial de 7 dias con tarjeta                          |
| ACB-013 | El trial no esta habilitado por configuracion comercial            | Bloquear alta Free si el cupo se agotó y mostrar mensaje de venta |

## 10. Trazabilidad

| Necesidad interna            | Modulo | Resultado esperado                              |
| ---------------------------- | ------ | ----------------------------------------------- |
| Control de acceso            | M01    | Solo staff autorizado entra                     |
| Visibilidad operativa        | M02    | KPIs y alertas claras                           |
| Soporte a usuarios           | M03    | Suspender y reactivar cuentas                   |
| Gestion territorial          | M04    | Mantener gimnasios activos                      |
| Moderacion manual            | M05    | Resolver reportes y abusos                      |
| Mantenimiento de catalogos   | M06    | Controlar ejercicios y rangos                   |
| Monetizacion y suscripciones | M07    | Gestionar planes, precios, trials y KPIs        |
| Limites del plan Free        | M07    | Restringir el acceso Free sin tocar historial   |
| Cupo de nuevas altas Free    | M07    | Bloquear altas Free cuando se alcance el maximo |
