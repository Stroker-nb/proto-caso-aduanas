# Diagramas de Arquitectura - Sistema Procesos de Aduanas

Este archivo contiene los diagramas UML mapeados del Documento de Arquitectura de Software (DAS) e implementados mediante **Mermaid.js**.

---

## 1. Vista de Escenario: Diagrama de Casos de Uso Específicos

Representa las interacciones de los distintos actores (Turistas, Chilenos, Funcionarios SAG/PDI/Aduanas) con el sistema informático.

```mermaid
graph LR
    %% Actores Principales
    Usuario((Usuario))
    Chileno((Usuario Chileno))
    Extranjero((Usuario Extranjero))
    Funcionario((Funcionario))
    FuncionarioAduanas((Funcionario Aduanas))
    FuncionarioSAG((Funcionario SAG))
    FuncionarioPDI((Funcionario PDI))

    %% Herencia de Actores
    Usuario <|-- Chileno
    Usuario <|-- Extranjero
    Funcionario <|-- FuncionarioAduanas
    Funcionario <|-- FuncionarioSAG
    Funcionario <|-- FuncionarioPDI

    %% Casos de Uso
    CU001(CU-001: Acceso a plataforma)
    CU002(CU-002: Gestión y registro de trámites aduaneros)
    CU003(CU-003: Revisión de base de datos)
    CU004(CU-004: Documentación necesaria)
    CU005(CU-005: Gestión y carga de documentación para menores)
    CU006(CU-006: Generación y validación mediante códigos de seguridad)
    CU007(CU-007: Gestión de datos / Visualización o actualización)
    CU008(CU-008: Visualización de usuario)

    %% Relaciones Actor -> Caso de Uso
    Usuario --> CU001
    Usuario --> CU002
    Usuario --> CU004
    Usuario --> CU005
    Usuario --> CU007

    Funcionario --> CU003
    Funcionario --> CU006
    Funcionario --> CU008

classDiagram
    %% Clases e interconexiones de Herencia
    Usuario <|-- Turista
    Usuario <|-- Chileno
    Funcionario <|-- FuncionarioPDI
    Funcionario <|-- FuncionarioSAG
    Funcionario <|-- FuncionarioAduanas
    DocumentoIdentidad <|-- DNITurista
    DocumentoIdentidad <|-- DNIChileno
    DocumentoIdentidad <|-- Pasaporte

    class Usuario {
        +String paisDeOrigen
        +String nombres
        +String apellidos
        +subirDocumento()
        +realizarTramite()
    }

    class Turista {
        +String idOPasaporte
        +String nroDeDocumento
    }

    class Chileno {
        +String rut
        +String nroDeDocumento
    }

    class Funcionario {
        +String rut
        +String nombres
        +String apellidos
        +int nivelDeAcceso
        +buscarUsuario()
        +buscarDocumento()
    }

    class FuncionarioPDI {
        +String rangoPDI
    }

    class FuncionarioSAG {
        +String rangoSAG
    }

    class FuncionarioAduanas {
        +String rangoAduanas
    }

    class Tramite {
        +String idTramite
        +String estado
        +Date fechaDeEmision
        +Date fechaDeVencimiento
        +String tipo
        +String documentoNecesario
        +validarTramite()
    }

    class Documento {
        +String tipoDeDocumento
        +String estado
        +validarDocumento()
    }

    class DocumentoIdentidad {
        +String nroDeDocumento
        +Date fechaEmision
        +Date fechaDeVencimiento
        +validarDocumentoDeIdentidad()
    }

    class DNITurista {
        +String id
    }

    class DNIChileno {
        +String rut
    }

    class Pasaporte {
        +String nroDePasaporte
    }

    %% Relaciones de Asociación
    Usuario "1" --> "*" Tramite : realiza
    Usuario "1" --> "*" Documento : sube
    Usuario "1" --> "1" DocumentoIdentidad : posee
    Funcionario "*" --> "*" Tramite : valida
    Funcionario "*" --> "*" Documento : revisa
    Tramite "*" --> "*" Documento : requiere

architecture-beta
    group sistemaAduanas(logos:aws) [Sistema aduanas]

    %% Componentes principales
    service DB(database) [BaseDeDatos] in sistemaAduanas
    service GU(subcomponents) [GestionUsuarios] in sistemaAduanas
    service GT(subcomponents) [GestionTramites] in sistemaAduanas
    service VT(subcomponents) [ValidadorTramite] in sistemaAduanas
    service GD(subcomponents) [GestionDocumento] in sistemaAduanas
    service VD(subcomponents) [ValidadorDocumento] in sistemaAduanas
    service GF(subcomponents) [GestionFuncionarios] in sistemaAduanas
    service CF(subcomponents) [ConsultaFuncionarios] in sistemaAduanas

    %% Relaciones y flujos
    GU:R -> GD
    GU:B -> GT
    GT:B -> VT
    GD:B -> VD
    GF:B -> VD
    GF:B -> VT
    GF:R -> CF
    
    %% Conexiones finales a Base de datos
    GU:B -> DB
    VT:B -> DB
    VD:B -> DB
    CF:B -> DB
    GF:B -> DB

graph TB
    subgraph Sistema_Aduanas [Sistema aduanas]
        GU[GestionUsuarios]
        GD[GestionDocumento]
        GT[GestionTramites]
        GF[GestionFuncionarios]
        VD[ValidadorDocumento]
        VT[ValidadorTramite]
        CF[ConsultaFuncionarios]
        BD[(BaseDeDatos)]
    end

    GU --> GT
    GU --> GD
    GD --> VD
    GT --> VT
    GF --> VD
    GF --> VT
    GF --> CF

    %% Persistencia
    GU -.-> BD
    VT -.-> BD
    VD -.-> BD
    CF -.-> BD
    GF -.-> BD

sequenceDiagram
    autonumber
    actor U as Usuario / Turista
    participant S as Servidor Aplicación
    participant DB as Base de Datos
    actor F as Funcionario (PDI/SAG/SNA)

    %% Registro e inicio de sesión
    U->>S: Registrarse / Iniciar Sesión (ClaveÚnica/Cuenta)
    S->>DB: Validar y guardar credenciales
    DB-->>S: Confirmación de cuenta exitosa
    S-->>U: Menú principal habilitado

    %% Flujo de carga y tramitación
    U->>S: Cargar documentos / Realizar Trámite
    S->>S: Procesar y Validar Formato (Generar Código QR)
    S->>DB: Almacenar Trámite y Documentos en estado 'Pendiente'
    DB-->>S: Trámite registrado

    %% Acción del Funcionario
    F->>S: Consultar información de un Usuario/Trámite
    S->>DB: Buscar datos persistidos e historial de logs
    DB-->>S: Retornar datos del Usuario e historial
    S-->>F: Visualización de datos y documentos en pantalla
    F->>S: Validar y cambiar estado del trámite (Aprobar/Rechazar)
    S->>DB: Actualizar estado de Trámite en BD
    S-->>U: Notificación de validación de documento (QR activo)
    F->>S: Solicitar generación de reportes (PDF / Excel)
    S->>DB: Consultar estado actual para reporte
    DB-->>S: Envío de datos consolidados
    S-->>F: Entrega de Reporte Final

graph TD
    subgraph Dispositivos_Cliente [Complejos Fronterizos / Cliente Externo]
        C1[Cliente Web: Navegador Moderno Turistas]
        C2[Cliente Web: Dispositivo Funcionario SNA/SAG/PDI]
    end

    subgraph Servidor_Gubernamental [Infraestructura de Servidores]
        subgraph Capa_Logica [Servidor de Aplicaciones]
            App[Lógica del Sistema: Validaciones, Gestión de Trámites y Documentos]
        end
        subgraph Capa_Datos [Servidor de Datos]
            BD[(Base de Datos Relacional + Logs de Auditoría)]
        end
    end

    C1 -- HTTPS / Protocolos Web --> App
    C2 -- HTTPS / Lector de Código QR --> App
    App -- Conexión Persistente / SQL --> BD