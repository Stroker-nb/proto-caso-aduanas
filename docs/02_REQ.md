
# Requerimiento funcionales

-RF01: El sistema debe permitir que el Usuario Chileno inicie sesión o cree su cuenta utilizando su Clave Única
-RF02: El sistema debe permitir que el Usuario Extranjero se registre y inicie sesión con un correo electrónico y contraseña creada en el portal
-RF03: El sistema debe permitir que los Funcionarios (Aduanas, SAG, PDI) accedan con sus credenciales institucionales a un panel de control privado
-RF04: El sistema debe permitir que cualquier Usuario elija ver todo el sitio en español o inglés
-RF05: El sistema debe mostrar una pantalla de inicio donde tenga acceso a todo lo que el sistema le ofrece.
-RF06: El sistema debe tener una sección donde se muestre información sobre el proceso de aduanas y toda la información sobre los trámites que se necesite
-RF07: El sistema debe permitir que el Usuario vea y edite sus datos personales en su perfil de cuenta
-RF08: El sistema debe permitir que el Usuario suba archivos (PDF o fotos) de su cédula de identidad o pasaporte
-RF09: El sistema debe permitir que el Usuario suba la autorización notarial para el paso de menores de edad
-RF10: El sistema debe permitir que el Usuario suba el documento del Juzgado de Familia si falta el permiso de un padre
-RF11: El sistema debe permitir que el Usuario suba los certificados de salud de mascotas si viaja con ellas
-RF12: El sistema debe validar que los archivos subidos tengan el formato correcto y avisar al Usuario si el archivo está dañado.
-RF13: El sistema debe validar automáticamente si los documentos del menor están en regla cruzando datos con el Registro Civil
-RF14: El sistema debe aprobar o rechazar de inmediato la solicitud de salida del menor basándose en la validez de los papeles subidos.
-RF15: El sistema debe verificar automáticamente si el vehículo tiene prohibiciones judiciales para salir del país
-RF16: El sistema debe aprobar automáticamente el permiso de vehículo por 180 días si es particular o 90 días si es diplomático
-RF17: El sistema debe rechazar automáticamente la Declaración Jurada si el Usuario marca que trae productos prohibidos por el SAG
-RF18: El sistema debe generar un comprobante con código QR para los usuarios que esté asociado a los trámites si estos fueron aprobados
-RF19: El sistema debe permitir que el Funcionario de la PDI escanee el QR de un trámite para ver si está aprobado
-RF20: El sistema debe permitir que el Usuario vea un historial de todos los trámites que ha realizado
-RF21: El sistema debe permitir que el Usuario elimine su cuenta y sus datos personales cuando ya no los necesite.
-RF22: El sistema debe asegurar que los datos del Usuario solo sean visibles para los Funcionarios autorizados en el momento del cruce
-RF23: El sistema debe generar informes automáticos de cuántos autos y personas pasaron por día.



   

# Requerimientos no funcionales

-RFN-01
Rendimiento
El 95% de las búsquedas de pasajeros deben responder en menos de 2 segundos.
-RFN-02
Seguridad
El sistema sólo dejará entrar a personas con cuenta habilitada (usuario y clave) y usará encriptación de datos.
-RFN-03
Fiabilidad
El sistema debe soportar picos de flujo de hasta un 180% (ej. temporada de verano) sin caerse o trabarse.
-RFN-04
Disponibilidad
El software debe estar funcionando el 99% del tiempo.
-RFN-05
Mantenibilidad
El sistema debe guardar los logs de todo lo que hacen los usuarios para facilitar la depuración de fallos.
-RFN-06
Portabilidad
El sistema debe abrirse correctamente en cualquier navegador moderno.
-RFN-07
Usabilidad
El sistema debe mostrar mensajes simples cuando el usuario o contraseña son incorrectos.
-RFN-08
Legal
El sistema debe asegurar que los datos sólo sean vistos por personal autorizado, cumpliendo la ley chilena.
-RFN-09
Reportes
El sistema debe generar informes únicamente en formato PDF o Excel.

