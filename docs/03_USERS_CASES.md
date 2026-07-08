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
-CU-01 nombre actor: Usuario (Chileno o Extranjero)
 descripcion actor: Persona que busca ingresar o salir del país y requiere identificarse en el sistema
. nombre caso de uso: Autenticar usuario
 descripcion de caso de uso: El usuario ingresa a la plataforma utilizando su Clave Única (si es chileno) o su correo y contraseña (si es extranjero) para acceder a sus trámites personalizados
. Requerimientos aludidos: RF01, RF02, RF03
-CU-02 nombre actor: Usuario
 descripcion actor: Viajero que necesita conocer las reglas y documentos obligatorios antes de su viaje
. nombre caso de uso: Informarse sobre trámites
 descripcion de caso de uso: El sistema ofrece una pantalla de inicio pública con guías claras sobre los requisitos para menores, vehículos y el SAG, permitiendo cambiar el idioma a inglés si es necesario
. Requerimientos aludidos: RF04, RF05, RF06
-CU-03 nombre actor: Usuario
 descripcion actor: Persona que desea administrar la información de su cuenta y su derecho a la privacidad
. nombre caso de uso: Gestionar privacidad y perfil
 descripcion de caso de uso: Interfaz donde el usuario puede visualizar y actualizar sus datos personales de contacto, o bien solicitar la eliminación definitiva de su cuenta y registros del sistema
. Requerimientos aludidos: RF07, RF21
-CU-04 nombre actor: Usuario
 descripcion actor: Viajero que realiza la carga digital de sus documentos para la frontera
. nombre caso de uso: Realizar trámite
 descripcion de caso de uso: El usuario sube archivos (fotos/PDF) de identidad y permisos legales. El sistema valida los formatos, cruza datos automáticamente con otras instituciones y aprueba o rechaza la solicitud de inmediato, generando un código QR si el resultado es positivo
. Requerimientos aludidos: RF08, RF09, RF10, RF11, RF12, RF13, RF14, RF15, RF16, RF17, RF18
-CU-05 nombre actor: Usuario
 descripcion actor: Viajero que desea consultar el progreso y resultado de sus gestiones digitales
. nombre caso de uso: Estados de trámite
 descripcion de caso de uso: Panel donde el usuario visualiza el historial de todos sus trámites realizados (RF20) y puede acceder en cualquier momento al código QR de los trámites aprobados para su exhibición en frontera
. Requerimientos aludidos: RF18, RF20
-CU-06 nombre actor: Funcionario (Aduanas, SAG o PDI)
 descripcion actor: Personal encargado de la fiscalización que valida el paso de los viajeros
. nombre caso de uso: Escaneo de trámite
 descripcion de caso de uso: El funcionario utiliza un dispositivo para leer el código QR del usuario; el sistema confirma de inmediato si los trámites fueron aprobados y permite revisar la documentación digital asociada para agilizar el cruce
. Requerimientos aludidos: RF19
-CU-07 nombre actor: Funcionario (Jefes de Servicio)
 descripcion actor: Personal administrativo que requiere analizar el flujo de personas y vehículos para la toma de decisiones
. nombre caso de uso: Reportes de gestión
 descripcion de caso de uso: El sistema procesa de forma inteligente la información de la base de datos para generar informes estadísticos automáticos, permitiendo su descarga únicamente en formatos PDF o Excel
. Requerimientos aludidos: RF23, RF24
-CU-08 nombre actor: Funcionario
 descripcion actor: Personal de control que requiere realizar una fiscalización dirigida a un viajero en particular
. nombre caso de uso: Visualizar información de un usuario específico
 descripcion de caso de uso: Permite al funcionario buscar a cualquier viajero por su identificador único (RUT o Pasaporte) para auditar su perfil, historial completo de trámites y documentos cargados por seguridad
. Requerimientos aludidos: RF22
