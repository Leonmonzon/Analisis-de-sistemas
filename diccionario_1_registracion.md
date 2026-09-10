# Diccionario de datos — Proceso Registración

## Entidad externa

| Entidad | Descripción |
|---|---|
| PROFESOR | Envía sus datos de registro y recibe el estado de su solicitud. |

## Procesos

| Código | Nombre | Descripción | Entradas | Salidas |
|---|---|---|---|---|
| 0 | Sistema | Proceso general que agrupa la interacción entre PROFESOR y el sistema | Datos | Respuestas |
| 1 | Registración | Registra la solicitud de un profesor en el sistema | Datos.registro | Estado.solicitud pendiente |
| 1.1 | Validar datos | Verifica que los datos de registro ingresados sean correctos y estén completos | Datos.registro | Datos validados |
| 1.2 | Registrar solicitud | Guarda la solicitud validada en el almacén de solicitudes | Datos validados | Solicitud registrada |
| 1.3 | Generar estado | Genera el estado de la solicitud para informar al profesor | Solicitud registrada | Estado.solicitud pendiente |

## Flujos de datos

| Nombre | Descripción | Origen | Destino | Composición |
|---|---|---|---|---|
| Datos.registro | Datos ingresados por el profesor para solicitar su registro | PROFESOR | 1.1 Validar datos | Nombre, apellido, DNI, email, contraseña |
| Datos validados | Datos de registro que superaron la validación | 1.1 Validar datos | 1.2 Registrar solicitud | = Datos.registro |
| Solicitud registrada | Confirmación interna de que la solicitud quedó guardada | 1.2 Registrar solicitud | 1.3 Generar estado | ID solicitud, fecha |
| Estado.solicitud pendiente | Confirmación al profesor de que su solicitud quedó pendiente de aprobación | 1.3 Generar estado | PROFESOR | Estado = "pendiente", fecha de solicitud |

## Almacenes de datos

| Código | Nombre | Descripción | Contenido |
|---|---|---|---|
| D1 | Solicitudes | Almacena las solicitudes de registro de los profesores | ID solicitud, datos del profesor, estado, fecha |

## Datos Primitivos

Nombre = varchar

Apellido = varchar

DNI = int

Email = varchar

Contraseña = varchar

ID solicitud = int

Fecha = date
