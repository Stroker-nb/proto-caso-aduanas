# Definicion de usuarios

Usuario
Persona que busca ingresar/salir del país.
Rango etario: 18-100 años.
Experiencia tecnológica variable.

Usuario Chileno
Clase hija de usuario. Ciudadano chileno que busca ingresar/salir del país.
Rango etario: 18-100 años.
Experiencia tecnológica variable.

Usuario Extranjero
Clase hija de usuario. Turista que busca ingresar/salir del país.
Rango etario: 18-100 años.
Experiencia tecnológica variable.

Funcionario
Trabajador que participa en el proceso de aduanas
Rango etario: 22-60 años.
Formación profesional completa.
Experiencia intermedia/alta.

Funcionario Aduanas
Clase hija de funcionario. Trabajador del SNA.
Rango etario: 22-60 años.
Formación profesional completa.
Experiencia intermedia/alta.

Funcionario SAG
Clase hija de funcionario.Trabajador del Servicio Agrícola y Ganadero.
Rango etario: 22-60 años.
Formación profesional completa.
Experiencia intermedia/alta.

Funcionario PDI
Clase hija de funcionario.Trabajador de la Policía de Investigaciones.
Rango etario: 22-60 años.
Formación profesional completa.
Experiencia intermedia/alta.

# CASOS DE USO 
CU1	
nombre actor:	usuario
descripcion actor:	Persona que quiere ingresar al pais
nombre caso de uso:	Acceso a plataforma
descripcion de caso de uso:	El usuario ingresa a la plataforma con su cuenta y es recibido por el menu principal que tiene toda la informacion necesaria para saber que documentos necesita el para ingresar a chile
Requerimientos aludidos	RF01, RF02

CU2	
Nombre:	usuario
Descripción: 	Persona que ya ha iniciado en la plataforma y necesita gestionar sus trámites de aduanas.
Nombre del caso de uso:	Gestión y registro de trámites de aduaneros.
Descripción del caso:	Tras iniciar sesión con éxito, el usuario accede a un menú principal que le permite visualizar y realizar los diversos trámites exigidos por adunas. Una vez que el usuario complete un trámite, el sistema se encarga de guardar automáticamente toda la información en la BD.
Requerimientos aludidos:	RF03, RF04

CU3
nombre actor:	Funcionario
descripcion actor:	Funcionario que trabaja en aduanas y necesita realizar tareas administrativas
nombre caso de uso:	Revision de base de datos
descripcion de caso de uso:	El usuario accede al sistema con una cuenta autorizada que le permite tener acceso a la base de datos donde le puede pedir un resumen para tener una vista general de todos los datos que hay
Requerimientos aludidos:	RFO5, RF06

CU4	
nombre actor: usuario
descripcion actor:	Persona que quiere ingresar al pais
nombre caso de uso:	Documentacion necesaria
descripcion de caso de uso:	El usuario entra a las distintas interfaces para poder realizar los distintos tramites que necesite para pasar, al terminar cada uno puede descargarlo. la base de datos guardara,asociara, y validara cada tramite a su cuenta, igualmente en el tema de validacion, se le mandara un notificacion sobre si el documento fue rechazado o validado por el sistema.
Requerimientos aludidos	RF07, RF08, RF09, RF10, RF11, RF12, RF13

CU5	
Nombre Actor:	usuario
Descripción Actor:	Persona que viaja con un menor de edad y necesita gestionar sus permisos legales.
Nombre caso de uso:	Gestión y cargar de documentación para menores.
Descripción de caso de uso:	El sistema permite al usuario subir los archivos y permisos legales del menor directamente a su cuenta. Esto facilitara tener toda la documentalización digitalizada y organizada para el momento de cruzar la frontera.
Requerimientos Aludidos:	RF14

CU6	
Nombre de actor:	Funcionario
Descripción Actor:	Personal encargado de la fiscalización que utiliza el sistema para validar la autenticidad de los documentos presentados.
Nombre caso de uso:	Generación y validación mediante códigos de seguridad.
Descripción de caso de uso:	El sistema asigna un código único a cada documento para que pueda ser escaneado. Al hacerlo, el sistema consulta la base de datos para confirmar de inmediato si el documento es válido y auténtico.
Requerimientos Aludidos:	RF15, RF16

CU7	
Nombre de actor:	usuario
Descripción Actor:	Persona que quier ingresar a aduanas
Nombre caso de uso:	Gestion de datos
Descripción de caso de uso:	El usuario entra a una interfaz donde puede ver y actualizar todos los datos de su cuenta y tambien ver el estado de sus documentos
Requerimientos Aludidos:	RF17 , RF18

CU8	
Nombre de actor:	Funcionario
Descripción Actor:	Funcionario que trabaja en aduanas
Nombre caso de uso:	Visualizacion de usuario
Descripción de caso de uso:	El funcionario puede ver dentro del sistema a un usuario especifico junto todos sus datos y documentacion.
Requerimientos Aludidos:	RF19