
# Requerimiento funcionales

RF01
El sistema debe mostrar una página de inicio con opciones de login mediante Clave Única (para chilenos) o cuenta normal (para cualquier persona).
RF02
El sistema debe mostrar un menú principal con toda la información sobre los documentos requeridos para ingresar al país.
RF03
El sistema debe mostrar un menú después de loguearse que permita realizar los diversos trámites aduaneros.
RF04
El sistema debe guardar la información de los trámites realizados en una base de datos.
RF05
El sistema debe permitir que los funcionarios autorizados accedan a la base de datos de trámites.
RF06
El sistema debe poder generar un reporte del estado actual de la base de datos.
RF07
El sistema debe mostrar una interfaz para que los usuarios realicen su declaración jurada de ingreso de alimentos/productos.
RF08
El sistema debe mostrar una interfaz para el permiso "Salida y Admisión Temporal de Vehículos Acuerdo Chileno Argentino".
RF09
El sistema debe mostrar una interfaz para declaración jurada de mascotas.
RF10
El sistema debe guardar los trámites en una base de datos y asociarlos a la cuenta del usuario.
RF11
El sistema debe validar el documento y enviar una notificación al usuario sobre si fue validado o rechazado.
RF12
El sistema debe permitir al usuario descargar todos los trámites relacionados con él.
RF13
El sistema debe dar la opción de subir los documentos necesarios para el paso de un menor de edad.
RF14
El sistema debe poner en cada documento un código QR para ser escaneado.
RF15
El sistema debe poder escanear los códigos QR de los documentos para validarlos en la base de datos.
RF16
El sistema debe permitir a los usuarios crear, visualizar y actualizar su información personal en su perfil.
RF17
El sistema debe mostrar al turista en su panel principal el estado actual de sus solicitudes.
RF18
El sistema permite a los funcionarios de Aduanas/SAG/PDI ver los datos y documentos de un usuario específico.
RF19
El sistema permitirá a usuarios y funcionarios seleccionar idioma (español o inglés).


   

# Requerimientos no funcionales

Código
Requerimiento
Descripción
RFN-01
Rendimiento
El 95% de las búsquedas de pasajeros deben responder en menos de 2 segundos.
RFN-02
Seguridad
El sistema sólo dejará entrar a personas con cuenta habilitada (usuario y clave) y usará encriptación de datos.
RFN-03
Fiabilidad
El sistema debe soportar picos de flujo de hasta un 180% (ej. temporada de verano) sin caerse o trabarse.
RFN-04
Disponibilidad
El software debe estar funcionando el 99% del tiempo.
RFN-05
Mantenibilidad
El sistema debe guardar los logs de todo lo que hacen los usuarios para facilitar la depuración de fallos.
RFN-06
Portabilidad
El sistema debe abrirse correctamente en cualquier navegador moderno.
RFN-07
Usabilidad
El sistema debe mostrar mensajes simples cuando el usuario o contraseña son incorrectos.
RFN-08
Legal
El sistema debe asegurar que los datos sólo sean vistos por personal autorizado, cumpliendo la ley chilena.
RFN-09
Reportes
El sistema debe generar informes únicamente en formato PDF o Excel.

