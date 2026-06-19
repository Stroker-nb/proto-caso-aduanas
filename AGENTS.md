# Instrucciones para los agentes de IA

## Fuentes de la verdad

Como agente de IA, los siguientes archivos o directorios son la fuente de la verdad para las implementaciones futuras:

- [README](README.md)
- [Instrucciones](AGENTS.md)
- [Documentos](docs)

## Técnicas de codificado

Como agente de IA, debes seguir estrictamente los siguientes lineamientos técnicos y de control de versiones para la construcción y prototipado del software:

- **Estrategia de Ramas (Git Branching):** Se debe crear una rama independiente por cada característica o componente específico (`feature/`) que se implemente en el prototipo navegable, mapeando los componentes principales definidos en la arquitectura. Ejemplos de nombres obligatorios para las ramas:
  - `feature/autenticacion-claveunica` para el desarrollo de los flujos de acceso inicial.
  - `feature/dashboard-turista` para el panel de control y estados del usuario.
  - `feature/formularios-tramites` para las interfaces de declaraciones juradas y carga de archivos.
  - `feature/panel-funcionarios` para las herramientas de búsqueda de la base de datos y fiscalización institucional.
- **Control de Versiones Semántico:** El desarrollo del código debe respetar y continuar el esquema de versionamiento semántico (X.Y.Z) registrado en el historial del sistema (ej. v1.0.0, v1.2.0, v2.0.0). Cualquier cambio incremental de lógica o interfaz debe ser documentado en la bitácora con su respectivo identificador de versión.
- **Arquitectura de Software Monolítica Simulada:** Aunque el entregable sea del lado del cliente, el código debe estructurarse emulando el estilo Monolítico por Capas adoptado en el diseño. Separa limpiamente la manipulación de datos internos de la lógica de validación de negocio (`ValidadorDocumentos`, `ValidadorTramites`) y de las funciones controladoras de las interfaces de usuario (HTML/CSS).
- **Mantenibilidad y Registro de Actividad:** Es obligatorio programar una función o script dedicado al registro de logs que almacene de forma estructurada en la memoria local cada acción simulada que realizan tanto los usuarios como los funcionarios aduaneros, dando cumplimiento directo al requerimiento de mantenibilidad RFN-05.
- **Validaciones Rigorosas Basadas en Heurísticas de Nielsen:** Con el fin de subsanar el cumplimiento parcial de la Heurística 9 (Ayudar a los usuarios a reconocer, diagnosticar y recuperarse de errores) detectado en los mockups previos, el agente de IA debe programar de forma explícita alertas visuales y mensajes claros ante fallos de autenticación, campos obligatorios vacíos o formatos incorrectos en los formularios.

## Contexto de desarrollo

El objetivo es implementar un prototipo web funcional, navegable e integrado para la modernización y automatización del **Proceso de Aduanas Terrestres en Chile**, enfocado en complejos fronterizos de alto flujo (como el Paso Los Libertadores). La solución debe simular la unificación operativa y el intercambio de información en tiempo real de tres instituciones críticas: el Servicio Nacional de Aduanas (SNA), el Servicio Agrícola y Ganadero (SAG) y la Policía de Investigaciones (PDI).

### Tecnologías Obligatorias
- **Frontend:** HTML5 semántico y CSS3 con diseño responsivo, estético y minimalista (Heurística 8), adoptando una paleta de colores institucional acorde a los portales gubernamentales chilenos.
- **Lógica e Interactividad:** JavaScript nativo (Vanilla JS) para manejar dinámicamente el intercambio de pantallas/vistas y las interacciones lógicas sin necesidad de dependencias externas.
- **Persistencia de Datos:** Uso exhaustivo de `localStorage` para emular el componente de la Base de Datos centralizada, persistiendo los datos de perfiles creados, las solicitudes guardadas y las acciones de control realizadas.

### Módulos y Vistas a Implementar

1. **Página de Inicio, Informativa y Autenticación (RF01, RF02, RF19):**
   - Menú principal de acceso público que detalla de forma clara toda la documentación y requisitos legales obligatorios para ingresar o salir del territorio chileno.
   - Un selector de idioma funcional que permita alternar instantáneamente la interfaz entre español e inglés.
   - Interfaz de inicio de sesión que divida explícitamente el acceso mediante "Clave Única" (para ciudadanos chilenos) y el acceso con "Cuenta Normal" (para turistas extranjeros).

2. **Panel Principal del Turista / Usuario Común (RF03, RF12, RF16, RF17):**
   - Dashboard interactivo donde el usuario visualiza de forma directa su información personal y el estado dinámico en tiempo real de todos sus trámites en curso (estados: *Pendiente*, *Aprobado*, *Rechazado*).
   - Formulario de Gestión de Perfil para crear, visualizar y modificar datos de identidad esenciales como RUT, número de Pasaporte, País de Origen, Nombres y Apellidos.
   - Botón habilitado para la simulación de descarga de todos los trámites asociados a su cuenta.

3. **Módulo Unificado de Formularios de Trámites y Carga Documental (RF07, RF08, RF09, RF10, RF13, RF14):**
   - **Formulario SAG/SNA:** Formulario interactivo para la Declaración Jurada obligatoria sobre el ingreso de alimentos o subproductos animales/vegetales.
   - **Formulario de Vehículos:** Formulario dedicado al permiso de "Salida y Admisión Temporal de Vehículos" según el Acuerdo Chileno-Argentino.
   - **Formulario de Mascotas:** Declaración jurada digital específica para el tránsito de animales de compañía.
   - **Apartado para Menores de Edad:** Zona interactiva que permite adjuntar de forma simulada la documentación necesaria para el viaje de menores (ej. autorizaciones notariales).
   - **Generador de Código QR:** Al enviar con éxito cualquier formulario, el sistema debe registrarlo en la base de datos simulada (`localStorage`) e inyectar dinámicamente un código QR en el documento digital generado para permitir su posterior validación.

4. **Panel de Control y Fiscalización para Funcionarios (RF05, RF06, RF15, RF18):**
   - Interfaz de acceso exclusivo restringida a personal fiscalizador, la cual debe permitir alternar u operar bajo tres perfiles institucionales diferenciados: Funcionario de Aduanas (SNA), Funcionario del SAG o Funcionario de la PDI.
   - Herramienta de consulta robusta vinculada al componente `ConsultaFuncionarios`, que provea barras de búsqueda avanzada por RUT o Pasaporte para localizar usuarios específicos.
   - Módulo Verificador de Seguridad: Input interactivo que simula el escaneo de un código QR, el cual busca el identificador del trámite en el `localStorage` y devuelve instantáneamente la información del documento y su validez.
   - Sistema de Gestión de Estado: Herramientas visuales para que los funcionarios revisen en profundidad los formularios del turista y sus documentos adjuntos, permitiéndoles presionar botones para cambiar el estado a *Aprobado* o *Rechazado*, lo que debe actualizar de inmediato el panel del usuario correspondiente.
   - Generación de Reportes: Un control operativo que compile de forma automática el estado cuantitativo actual de los trámites en el almacenamiento interno y despliegue un informe analítico simulando los formatos permitidos en PDF o Excel (RFN-09).