# Diccionario de datos — Proceso Inicio de sesión

## Entidad externa

| Entidad | Descripción |
|---|---|
| PROFESOR | Envía sus credenciales para acceder al sistema y recibe la confirmación de sesión y cuenta iniciadas. |

## Procesos

| Código | Nombre | Descripción | Entradas | Salidas |
|---|---|---|---|---|
| 0 | Inicio de sesión | Gestiona el acceso del profesor al sistema | Datos.inicio.sesion | Sesión y cuenta iniciada |
| 1.1 | Validar credenciales | Verifica usuario y contraseña del profesor | Datos.inicio.sesion | Credenciales válidas |
| 1.2 | Iniciar sesión | Abre la sesión activa del profesor en el sistema | Credenciales válidas | Sesión iniciada |
| 1.3 | Activar cuenta | Marca la cuenta del profesor como activa / en línea | Credenciales válidas | Cuenta iniciada |
| 1.1.1 | Verificar usuario | Comprueba que el usuario ingresado exista en el sistema | Datos.inicio.sesion | Usuario verificado |
| 1.1.2 | Verificar contraseña | Contrasta la contraseña ingresada contra el almacén de credenciales | Usuario verificado | Contraseña correcta |
| 1.1.3 | Confirmar validez | Confirma que usuario y contraseña son válidos en su conjunto | Contraseña correcta | Credenciales válidas |

## Flujos de datos

| Nombre | Descripción | Origen | Destino | Composición |
|---|---|---|---|---|
| Datos.inicio.sesion | Usuario y contraseña ingresados por el profesor para acceder | PROFESOR | 1.1.1 Verificar usuario | Usuario, contraseña |
| Usuario verificado | Señal de que el usuario ingresado existe | 1.1.1 Verificar usuario | 1.1.2 Verificar contraseña | Usuario, resultado (sí/no) |
| Contraseña correcta | Señal de que la contraseña ingresada coincide | 1.1.2 Verificar contraseña | 1.1.3 Confirmar validez | Resultado (sí/no) |
| Credenciales válidas | Confirmación de que usuario y contraseña son correctos | 1.1 Validar credenciales | 1.2 Iniciar sesión, 1.3 Activar cuenta | Usuario, resultado = "válido" |
| Sesión iniciada | Confirmación de apertura de sesión | 1.2 Iniciar sesión | PROFESOR | ID sesión, fecha/hora |
| Cuenta iniciada | Confirmación de activación de la cuenta | 1.3 Activar cuenta | PROFESOR | Estado = "activo" |

## Almacenes de datos

| Código | Nombre | Descripción | Contenido |
|---|---|---|---|
| D2 | Credenciales | Almacena usuario y contraseña de los profesores para validar el inicio de sesión | ID profesor, usuario, contraseña (hash) |
