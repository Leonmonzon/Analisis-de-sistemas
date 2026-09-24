# Diccionario de datos — Proceso Inicio de sesión

## Entidad externa

| Entidad | Descripción |
|---|---|
| PROFESOR | Envía sus credenciales para acceder al sistema y recibe la confirmación de sesión y cuenta iniciadas. |

## Procesos

| Código | Nombre | Descripción | Entradas | Salidas |
|---|---|---|---|---|
| 0 | Inicio de sesión | Gestiona el acceso del profesor al sistema | Datos.inicio.sesion | Sesión y cuenta iniciada |
| 1.1 | Validar credenciales | Verifica usuario y contraseña del profesor | Datos.inicio.sesion | Credenciales válidas, Credenciales inválidas |
| 1.2 | Iniciar sesión | Abre la sesión activa del profesor en el sistema | Credenciales válidas | Sesión iniciada |
| 1.3 | Activar cuenta | Marca la cuenta del profesor como activa / en línea | Credenciales válidas | Cuenta iniciada |
| 1.1.1 | Verificar usuario | Comprueba que el usuario ingresado exista en el sistema | Datos.inicio.sesion | Usuario verificado, Usuario inexistente |
| 1.1.2 | Verificar contraseña | Contrasta la contraseña ingresada contra el almacén de credenciales | Usuario verificado, Datos de credenciales | Contraseña correcta, Contraseña incorrecta |
| 1.1.3 | Confirmar validez | Confirma que usuario y contraseña son válidos en su conjunto | Contraseña correcta | Credenciales válidas |

## Flujos de datos

| Nombre | Descripción | Origen | Destino | Composición |
|---|---|---|---|---|
| Datos.inicio.sesion | Usuario y contraseña ingresados por el profesor para acceder | PROFESOR | 1.1.1 Verificar usuario | Usuario, Contraseña |
| Usuario verificado | Señal de que el usuario ingresado existe en el sistema | 1.1.1 Verificar usuario | 1.1.2 Verificar contraseña | Usuario, Resultado (sí/no) |
| Datos de credenciales | Lectura de datos o hash de contraseña desde el almacén para contrastar | D2 Credenciales | 1.1.2 Verificar contraseña | ID profesor, Contraseña (hash) |
| Contraseña correcta | Señal de que la contraseña ingresada coincide | 1.1.2 Verificar contraseña | 1.1.3 Confirmar validez | Resultado (sí/no) |
| Credenciales válidas | Confirmación de que usuario y contraseña son correctos | 1.1.3 Confirmar validez | 1.2 Iniciar sesión, 1.3 Activar cuenta | Usuario, Resultado = "válido" |
| Credenciales inválidas | Mensaje de error retornado al profesor por fallo de autenticación | 1.1 Validar credenciales | PROFESOR | Mensaje_Error = "Usuario o contraseña incorrectos" |
| Sesión iniciada | Confirmación de apertura de sesión activa | 1.2 Iniciar sesión | PROFESOR | ID sesión, Fecha/hora |
| Cuenta iniciada | Confirmación de activación de la cuenta en línea | 1.3 Activar cuenta | PROFESOR | Estado = "activo" |
| Sesión y cuenta iniciada | Respuesta agregada del Nivel 0 que confirma el acceso exitoso | 0 Inicio de sesión | PROFESOR | ID sesión, Estado = "activo" |

## Almacenes de datos

| Código | Nombre | Descripción | Contenido |
|---|---|---|---|
| D2 | Credenciales | Almacena usuario y contraseña de los profesores para validar el inicio de sesión | ID profesor, Usuario, Contraseña (hash) |

## Datos Primitivos

| Nombre de Dato | Tipo de Dato |
|---|---|
| Usuario | Varchar |
| Contraseña | Varchar |
| Resultado | Bool |
| ID profesor | Int |
| ID sesión | Int |
| Fecha/hora | Datetime |
| Estado | Varchar |
| Activo | Bool |
