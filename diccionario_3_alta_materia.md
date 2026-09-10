# Diccionario de datos — Proceso Alta materia

## Entidad externa

| Entidad | Descripción |
|---|---|
| PROFESOR | Envía los datos de la nueva materia y recibe la confirmación de que quedó registrada y presente. |

## Procesos

| Código | Nombre | Descripción | Entradas | Salidas |
|---|---|---|---|---|
| 0 | Alta materia | Gestiona el alta de una nueva materia por parte del profesor | Datos.materia | Materia registrada y presente |
| 1.1 | Validar datos materia | Verifica que los datos de la materia sean correctos y no estén duplicados | Datos.materia | Datos validados |
| 1.2 | Registrar materia | Guarda la materia validada en el almacén de materias | Datos validados | Materia registrada |
| 1.3 | Publicar materia | Marca la materia como presente / disponible en el sistema | Datos validados | Materia presente |
| 1.1.1 | Verificar datos completos | Comprueba que todos los campos obligatorios de la materia estén presentes | Datos.materia | Datos completos |
| 1.1.2 | Verificar duplicado | Consulta el almacén de materias para descartar duplicados | Datos completos | Sin duplicado |
| 1.1.3 | Confirmar validez | Confirma que los datos de la materia son válidos en su conjunto | Sin duplicado | Datos validados |

## Flujos de datos

| Nombre | Descripción | Origen | Destino | Composición |
|---|---|---|---|---|
| Datos.materia | Datos de la nueva materia ingresados por el profesor | PROFESOR | 1.1.1 Verificar datos completos | Nombre, código, descripción, profesor a cargo |
| Datos completos | Señal de que los datos de la materia están completos | 1.1.1 Verificar datos completos | 1.1.2 Verificar duplicado | Resultado (sí/no) |
| Sin duplicado | Señal de que la materia no está registrada previamente | 1.1.2 Verificar duplicado | 1.1.3 Confirmar validez | Resultado (sí/no) |
| Datos validados | Datos de la materia que superaron la validación | 1.1 Validar datos materia | 1.2 Registrar materia, 1.3 Publicar materia | = Datos.materia |
| Materia registrada | Confirmación de que la materia quedó guardada | 1.2 Registrar materia | PROFESOR | ID materia, fecha de alta |
| Materia presente | Confirmación de que la materia quedó disponible/publicada | 1.3 Publicar materia | PROFESOR | Estado = "presente" |

## Almacenes de datos

| Código | Nombre | Descripción | Contenido |
|---|---|---|---|
| D3 | Materias | Almacena las materias registradas en el sistema | ID materia, nombre, código, profesor a cargo, estado |
