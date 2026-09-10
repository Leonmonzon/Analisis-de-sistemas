
# Diccionario de datos — Sistema

## Entidad externa

| Entidad  | Descripción                                                                                                                          |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| PROFESOR | Envía datos para registrarse, iniciar sesión, registrar materias y dar de alta materias. Recibe las confirmaciones correspondientes. |

## Procesos

| Código | Nombre                   | Descripción                                               | Entradas             | Salidas                                       |
| ------ | ------------------------ | --------------------------------------------------------- | -------------------- | --------------------------------------------- |
| 1.1.1  | Registrar Profesor       | Registra los datos del profesor en el sistema             | DATOS_PROFESOR       | PROFESOR_REGISTRADO                           |
| 1.2.1  | Validar Inicio de Sesión | Verifica las credenciales ingresadas por el profesor      | DATOS_INICIO_SESION  | CREDENCIALES_VALIDAS / CREDENCIALES_INVALIDAS |
| 1.2.2  | Crear Sesión             | Crea una sesión para el profesor con credenciales válidas | CREDENCIALES_VALIDAS | SESION_INICIADA                               |
| 1.3.1  | Registrar Materia        | Registra una nueva materia en el sistema                  | DATOS_MATERIA        | MATERIA_REGISTRADA                            |
| 1.3.2  | Dar de Alta Materia      | Da de alta una materia previamente registrada             | DATOS_ALTA_MATERIA   | ALTA_MATERIA_REGISTRADA                       |

## Flujos de datos

| Nombre                   | Descripción                      | Origen                         | Destino                        | Composición                                   |
| ------------------------ | -------------------------------- | ------------------------------ | ------------------------------ | --------------------------------------------- |
| DATOS_PROFESOR           | Datos ingresados por el profesor | PROFESOR                       | 1.1.1 Registrar Profesor       | Nombre, apellido, DNI, email, contraseña      |
| PROFESOR_REGISTRADO      | Confirmación del registro        | 1.1.1 Registrar Profesor       | D1 Profesores                  | ID profesor, datos profesor                   |
| CONFIRMACION_REGISTRO    | Confirmación del registro        | D1 Profesores                  | PROFESOR                       | Estado, fecha                                 |
| DATOS_INICIO_SESION      | Datos para iniciar sesión        | PROFESOR                       | 1.2.1 Validar Inicio de Sesión | Usuario, contraseña                           |
| CREDENCIALES_VALIDAS     | Credenciales correctas           | 1.2.1 Validar Inicio de Sesión | 1.2.2 Crear Sesión             | Usuario, resultado                            |
| CREDENCIALES_INVALIDAS   | Credenciales incorrectas         | 1.2.1 Validar Inicio de Sesión | PROFESOR                       | Resultado                                     |
| SESION_INICIADA          | Confirmación de sesión           | 1.2.2 Crear Sesión             | D1 Cuentas                     | ID sesión, usuario, fecha/hora                |
| DATOS_MATERIA            | Datos de la materia              | PROFESOR                       | 1.3.1 Registrar Materia        | Nombre, código, descripción, profesor a cargo |
| MATERIA_REGISTRADA       | Confirmación de registro         | 1.3.1 Registrar Materia        | D1 Materias                    | ID materia, nombre, código                    |
| CONFIRMACION_REGISTRO    | Confirmación del registro        | D1 Materias                    | PROFESOR                       | Estado, fecha                                 |
| DATOS_ALTA_MATERIA       | Datos para dar de alta           | PROFESOR                       | 1.3.2 Dar de Alta Materia      | ID materia, código                            |
| ALTA_MATERIA_REGISTRADA  | Confirmación del alta            | 1.3.2 Dar de Alta Materia      | D1 Materias                    | ID materia, estado                            |
| CONFIRMACION_ALTA_VALIDA | Confirmación del alta            | D1 Materias                    | PROFESOR                       | Estado, fecha                                 |

# Datos primitivos

* **Nombre** = `varchar`
* **Apellido** = `varchar`
* **DNI** = `int`
* **Email** = `varchar`
* **Contraseña** = `varchar`
* **ID profesor** = `int`
* **Estado** = `varchar`
* **Fecha** = `date`
* **Usuario** = `varchar`
* **Resultado** = `bool`
* **ID sesión** = `int`
* **Fecha/hora** = `date`
* **ID materia** = `int`
* **Código** = `varchar`
* **Descripción** = `varchar`
* **Profesor a cargo** = `int`

### Almacenes de datos

**D1 Profesores**

* ID profesor = `int`
* Nombre = `varchar`
* Apellido = `varchar`
* DNI = `int`
* Email = `varchar`
* Contraseña = `varchar`

**D2 Cuentas**

* ID sesión = `int`
* ID profesor = `int`
* Usuario = `varchar`
* Estado = `varchar`
* Fecha/hora = `date`

**D3 Materias**

* ID materia = `int`
* Nombre = `varchar`
* Código = `varchar`
* Descripción = `varchar`
* Profesor a cargo = `int`
* Estado = `varchar`
