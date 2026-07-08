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
