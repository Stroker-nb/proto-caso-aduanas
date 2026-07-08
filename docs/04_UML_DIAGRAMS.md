# Diagramas de Arquitectura - Proceso de Aduanas (Versión 2.0)

Este documento contiene la representación en código **Mermaid.js** de todos los diagramas de arquitectura UML descritos en el DAS v2.0 para el Sistema de Gestión Aduanera Terrestre.

---

## 1. VISTA DE ESCENARIO
### Diagrama General de Casos de Uso (CU-01 a CU-08)

```mermaid
graph LR
    %% Definición de Actores
    subgraph Actores
        U[Usuario]
        UC[Usuario Chileno]
        UE[Usuario Extranjero]
        F[Funcionario]
        FPDI[Funcionario PDI]
        FADU[Funcionario Aduanas]
        FSAG[Funcionario SAG]
    end

    %% Relaciones de Herencia de Actores
    UC --> U
    UE --> U
    FPDI --> F
    FADU --> F
    FSAG --> F

    %% Definición de Casos de Uso
    CU01([CU-01: Autenticar usuario])
    CU02([CU-02: Informarse sobre trámites])
    CU03([CU-03: Gestionar privacidad y perfil])
    CU04([CU-04: Realizar trámite])
    CU05([CU-05: Estados de trámite])
    CU06([CU-06: Escaneo de trámite])
    CU07([CU-07: Reportes de gestión])
    CU08([CU-08: Visualizar información de usuario específico])

    %% Asociaciones de Usuarios
    U --- CU01
    U --- CU02
    U --- CU03
    U --- CU04
    U --- CU05

    %% Asociaciones de Funcionarios
    F --- CU06
    F --- CU07
    F --- CU08

    %% Interacciones Cruzadas entre Actores y Casos de Uso
    U --- CU06
    U --- CU08

    %% Relaciones de Dependencia entre Casos de Uso
    CU05 -.->|include| CU04
    CU03 -.->|include| CU01
    CU02 -.->|include| CU01
