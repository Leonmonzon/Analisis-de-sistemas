# Diccionario de datos — Proceso Registrar Materia

## Entidad externa

| Entidad  | Descripción                                                                           |
| -------- | ------------------------------------------------------------------------------------- |
| PROFESOR | Envía los datos de la nueva materia y recibe la confirmación de que quedó registrada. |

## Procesos

| Código | Nombre            | Descripción                                           | Entradas      | Salidas            |
| ------ | ----------------- | ----------------------------------------------------- | ------------- | ------------------ |
| 1.3.1  | Registrar Materia | Registra los datos de una nueva materia en el sistema | Datos.materia | Materia.registrada |

## Flujos de datos

| Nombre                | Descripción                                                              | Origen                  | Destino                 | Composición                                            |
| --------------------- | ------------------------------------------------------------------------ | ----------------------- | ----------------------- | ------------------------------------------------------ |
| Datos.materia         | Datos ingresados por el profesor para registrar una nueva materia        | PROFESOR                | 1.3.1 Registrar Materia | Código materia, nombre, descripción, año, cuatrimestre |
| Materia.registrada    | Datos de la materia que fueron registrados correctamente                 | 1.3.1 Registrar Materia | D1 Materias             | = Datos.materia                                        |
| Confirmación.registro | Confirmación enviada al profesor indicando que la materia fue registrada | D1 Materias             | PROFESOR                | Código materia, nombre, estado, fecha de registro      |

## Almacenes de datos

| Código | Nombre   | Descripción                                                  | Contenido                                                                         |
| ------ | -------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------- |
| D1     | Materias | Almacena los datos de las materias registradas en el sistema | Código materia, nombre, descripción, año, cuatrimestre, estado, fecha de registro |

## Datos Primitivos

**Código materia** = varchar

**Nombre** = varchar

**Descripción** = varchar

**Año** = int

**Cuatrimestre** = int

**Estado** = varchar

**Fecha de registro** = date

---
