# Especificación de Software Basada en Casos de Uso y Suite de Pruebas (TDD)

Este documento sirve como la especificación técnica de entrada para la generación automática del sistema "Proceso de Aduanas". La IA de desarrollo debe implementar tanto las clases de negocio como la suite de pruebas unitarias y de integración descritas a continuación, garantizando que todos los criterios de aceptación pasen con éxito (Definición de "Done").

---

## 1. Modelo de Dominio y Restricciones de Usuario

La IA debe implementar de manera estricta la siguiente jerarquía de objetos y tipos de datos:

### Entidades de Usuario
* **Usuario (Clase Base):** * Atributos: `nombre` (String), `apellido` (String), `edad` (Integer, restricción: 18 a 100 años), `sesion_activa` (Boolean), `documentos_adjuntos` (List).
* **Usuario Chileno (Hijo de Usuario):**
    * Atributos adicionales: `rut` (String, formato chileno válido).
* **Usuario Extranjero (Hijo de Usuario):**
    * Atributos adicionales: `pasaporte` (String).

### Entidades de Funcionario (Personal de Fiscalización)
* **Funcionario (Clase Base):**
    * Atributos: `nombre` (String), `apellido` (String), `edad` (Integer, restricción: 22 a 60 años), `institucion` (String).
* **Funcionario Aduanas (SNA), Funcionario SAG, Funcionario PDI:**
    * Clases hijas que heredan de Funcionario y mapean la propiedad `institucion` según su rol fiscalizador.

---

## 2. Suite de Pruebas de Criterios de Aceptación (Una por Caso de Uso)

El sistema generado se considerará **Terminado (Done)** únicamente si pasa con éxito la ejecución del siguiente código de pruebas implementado en `test_aduanas.py`.

```python
import pytest
from datetime import datetime
from typing import List, Dict, Any, Optional

# ==============================================================================
# INFRAESTRUCTURA DE SIMULACIÓN REQUERIDA (Mock/Stubs del Sistema)
# ==============================================================================

class BaseDeDatosSimulada:
    def __init__(self):
        self.usuarios = {}
        self.tramites = []
        self.logs_auditoria = []

    def guardar_tramite(self, tramite: Dict[str, Any]):
        self.tramites.append(tramite)
        self.logs_auditoria.append(f"Trámite {tramite['id']} guardado automáticamente.")

    def obtener_resumen_general(self) -> Dict[str, int]:
        return {
            "total_tramites": len(self.tramites),
            "total_usuarios_registrados": len(self.usuarios)
        }

class SistemaAduanas:
    def __init__(self):
        self.bd = BaseDeDatosSimulada()
        self.notificaciones_enviadas = []

    def login(self, usuario: Any) -> str:
        usuario.sesion_activa = True
        return "Menú Principal: Para ingresar a Chile necesita Declaración SAG y Documento de Identidad."

    def registrar_tramite(self, usuario: Any, tipo_tramite: str, datos: Dict[str, Any]) -> Dict[str, Any]:
        id_tramite = f"TRAM-{len(self.bd.tramites) + 1}"
        tramite = {
            "id": id_tramite,
            "usuario_nombre": usuario.nombre,
            "tipo": tipo_tramite,
            "datos": datos,
            "estado": "Pendiente",
            "codigo_seguridad": f"QR-{id_tramite}",
            "fecha": datetime.now()
        }
        self.bd.guardar_tramite(tramite)
        return tramite

    def actualizar_y_notificar_estado(self, id_tramite: str, nuevo_estado: str):
        for t in self.bd.tramites:
            if t["id"] == id_tramite:
                t["estado"] = nuevo_estado
                self.notificaciones_enviadas.append({
                    "usuario": t["usuario_nombre"],
                    "mensaje": f"Su documento {id_tramite} ha sido {nuevo_estado} por el sistema."
                })

    def escanear_codigo(self, codigo_qr: str) -> Optional[Dict[str, Any]]:
        for t in self.bd.tramites:
            if t["codigo_seguridad"] == codigo_qr:
                return {"valido": True, "documento": t}
        return {"valido": False, "documento": None}


# ==============================================================================
# EJECUCIÓN DE PRUEBAS DE CASOS DE USO
# ==============================================================================

# --- PRUEBA CU1: Acceso a plataforma (RF01, RF02) ---
def test_cu1_acceso_a_plataforma():
    """
    CU1 - Actor: Usuario (Chileno/Extranjero)
    Escenario: Login exitoso en plataforma y despliegue de requisitos informativos.
    """
    # GIVEN: Un usuario chileno registrado dentro del rango de edad permitido
    # (Clase UsuarioChileno simulada o real con sus restricciones)
    from de_algun_lado import UsuarioChileno # La IA debe proveer la clase real
    usuario_chileno = UsuarioChileno(nombre="Juan", apellido="Pérez", edad=35, rut="12.345.678-9")
    sistema = SistemaAduanas()

    # WHEN: El usuario inicia sesión en el sistema
    vista_menu_principal = sistema.login(usuario_chileno)

    # THEN: La sesión pasa a estado activo
    assert usuario_chileno.sesion_activa is True
    # Y: El menú expone los requerimientos informativos obligatorios para ingresar al país
    assert "Menú Principal" in vista_menu_principal
    assert "necesita Declaración SAG" in vista_menu_principal


# --- PRUEBA CU2: Gestión y registro de trámites de aduaneros (RF03, RF04) ---
def test_cu2_gestion_y_registro_tramites():
    """
    CU2 - Actor: Usuario
    Escenario: Almacenamiento automático y persistente de trámites completados en la BD.
    """
    # GIVEN: Un usuario extranjero autenticado que requiere gestionar sus trámites
    from de_algun_lado import UsuarioExtranjero
    usuario_extranjero = UsuarioExtranjero(nombre="John", apellido="Doe", edad=28, pasaporte="A1234567")
    sistema = SistemaAduanas()
    sistema.login(usuario_extranjero)

    # WHEN: Envía un trámite completado exigido por la aduana
    datos_declaracion = {"trae_productos_organicos": False, "monto_efectivo": 2000}
    tramite_creado = sistema.registrar_tramite(usuario_extranjero, "Declaración de Aduana", datos_declaracion)

    # THEN: El trámite se procesa con un identificador único correlativo
    assert tramite_creado["id"] == "TRAM-1"
    # Y: La información se almacena automáticamente en el repositorio persistente sin intervención manual
    assert len(sistema.bd.tramites) == 1
    assert "guardado automáticamente" in sistema.bd.logs_auditoria[0]


# --- PRUEBA CU3: Revision de base de datos (RF05, RF06) ---
def test_cu3_revision_base_de_datos():
    """
    CU3 - Actor: Funcionario
    Escenario: Consulta administrativa y consolidación de un resumen general del estado aduanero.
    """
    # GIVEN: Un Funcionario del Servicio Agrícola y Ganadero (SAG) con credenciales vigentes
    from de_algun_lado import Funcionario
    funcionario_sag = Funcionario(nombre="Ana", apellido="Gómez", edad=42, institucion="SAG")
    sistema = SistemaAduanas()
    
    # Inyección de registros de prueba en la BD
    sistema.bd.usuarios["juan123"] = {"nombre": "Juan"}
    sistema.bd.tramites.append({"id": "TRAM-99", "estado": "Pendiente"})

    # WHEN: El funcionario autorizado solicita el resumen analítico de control aduanero
    resumen_datos = sistema.bd.obtener_resumen_general()

    # THEN: Se valida la identidad institucional y se provee la vista general de la data
    assert funcionario_sag.institucion == "SAG"
    assert resumen_datos["total_tramites"] == 1
    assert resumen_datos["total_usuarios_registrados"] == 1


# --- PRUEBA CU4: Documentación necesaria (RF07 al RF13) ---
def test_cu4_documentacion_necesaria_y_notificacion():
    """
    CU4 - Actor: Usuario
    Escenario: Asociación de formularios completados y despacho automatizado de notificaciones de estado.
    """
    # GIVEN: Un trámite asociado directamente a la cuenta de un viajero
    from de_algun_lado import Usuario
    usuario = Usuario(nombre="Carlos", apellido="Ruiz", edad=45)
    sistema = SistemaAduanas()
    tramite = sistema.registrar_tramite(usuario, "Permiso Vehicular", {"patente": "AB-CD-12"})

    # WHEN: El sistema o un fiscalizador procesa la validación emitiendo un veredicto (Aprobado/Rechazado)
    id_documento = tramite["id"]
    sistema.actualizar_y_notificar_estado(id_documento, nuevo_estado="Rechazado")

    # THEN: El estado cambia de forma íntegra en el backend
    assert sistema.bd.tramites[0]["estado"] == "Rechazado"
    # Y: Se despacha una alerta inmediata informando al usuario sobre la resolución del documento
    assert len(sistema.notificaciones_enviadas) == 1
    assert sistema.notificaciones_enviadas[0]["usuario"] == "Carlos"
    assert "ha sido Rechazado" in sistema.notificaciones_enviadas[0]["mensaje"]


# --- PRUEBA CU5: Gestión y cargar de documentación para menores (RF14) ---
def test_cu5_gestion_y_carga_documentacion_menores():
    """
    CU5 - Actor: Usuario
    Escenario: Carga y resguardo digitalizado de autorizaciones legales de menores de edad.
    """
    # GIVEN: Un usuario adulto que actúa como tutor o viaja con un menor de edad
    from de_algun_lado import Usuario
    usuario_padre = Usuario(nombre="Roberto", apellido="Lara", edad=39)
    
    # WHEN: Carga los archivos adjuntos y documentos del menor directamente dentro del alcance de su cuenta
    documento_menor = {
        "tipo": "Autorización Notarial de Viaje",
        "menor_nombre": "Diego Lara",
        "archivo_binario_simulado": b"PDF_PERMISO_NOTARIAL"
    }
    usuario_padre.documentos_adjuntos.append(documento_menor)

    # THEN: Los documentos quedan indexados y organizados para agilizar la posterior inspección fronteriza
    assert len(usuario_padre.documentos_adjuntos) == 1
    assert usuario_padre.documentos_adjuntos[0]["menor_nombre"] == "Diego Lara"
    assert usuario_padre.documentos_adjuntos[0]["tipo"] == "Autorización Notarial de Viaje"


# --- PRUEBA CU6: Generación y validación mediante códigos de seguridad (RF15, RF16) ---
def test_cu6_generacion_y_validacion_codigos_seguridad():
    """
    CU6 - Actor: Funcionario
    Escenario: Validación instantánea de documentos en frontera mediante el escaneo de códigos criptográficos únicos.
    """
    # GIVEN: Un funcionario de la Policía de Investigaciones (PDI) operando en el paso fronterizo
    from de_algun_lado import Funcionario
    funcionario_pdi = Funcionario(nombre="Subcomisario", apellido="Muñoz", edad=30, institucion="PDI")
    sistema = SistemaAduanas()
    
    # Un usuario generó una solicitud previa que el sistema firmó con un código de seguridad único
    from de_algun_lado import Usuario
    usuario = Usuario(nombre="María", apellido="Silva", edad=22)
    tramite_previo = sistema.registrar_tramite(usuario, "Declaración de Mascotas", {"tipo_animal": "Perro"})
    codigo_qr_presentado = tramite_previo["codigo_seguridad"]

    # WHEN: El fiscalizador escanea el identificador único del documento presentado
    resultado_escaneo = sistema.escanear_codigo(codigo_qr_presentado)

    # THEN: El sistema interroga a la base de datos y ratifica de forma síncrona y en tiempo real la validez del mismo
    assert funcionario_pdi.institucion == "PDI"
    assert resultado_escaneo["valido"] is True
    assert resultado_escaneo["documento"]["usuario_nombre"] == "María"


# --- PRUEBA CU7: Gestion de datos (RF17, RF18) ---
def test_cu7_gestion_de_datos_usuario():
    """
    CU7 - Actor: Usuario
    Escenario: Interfaz de autoservicio para modificar perfiles personales e inspeccionar estados de tramitación.
    """
    # GIVEN: Un usuario con una solicitud en curso registrada
    from de_algun_lado import Usuario
    usuario = Usuario(nombre="Luis", apellido="Tapia", edad=50)
    sistema = SistemaAduanas()
    tramite = sistema.registrar_tramite(usuario, "Declaración SAG", {"trae_frutas": False})

    # WHEN: El usuario actualiza su información personal mediante la interfaz de gestión y consulta el estado de su trámite
    usuario.apellido = "Tapia Concha"
    estado_documento = tramite["estado"]

    # THEN: El modelo de datos muta reflejando el cambio de perfil actualizado
    assert usuario.apellido == "Tapia Concha"
    # Y: El sistema retorna con fidelidad el estado actual ("Pendiente") asignado al archivo
    assert estado_documento == "Pendiente"


# --- PRUEBA CU8: Visualización de usuario (RF19) ---
def test_cu8_visualizacion_de_usuario_por_funcionario():
    """
    CU8 - Actor: Funcionario
    Escenario: Inspección pormenorizada de la ficha de un ciudadano y sus anexos desde la consola del fiscalizador.
    """
    # GIVEN: Un funcionario de la aduana (SNA) y un usuario cargado con documentos en el padrón del sistema
    from de_algun_lado import Funcionario, UsuarioChileno
    funcionario_aduana = Funcionario(nombre="Marcos", apellido="Reyes", edad=48, institucion="Aduanas")
    usuario_viajero = UsuarioChileno(nombre="Esteban", apellido="Quito", edad=29, rut="18.123.456-7")
    usuario_viajero.documentos_adjuntos.append({"tipo": "DNI Frente", "archivo": "rut_frente.jpg"})
    
    sistema = SistemaAduanas()
    sistema.bd.usuarios[usuario_viajero.rut] = usuario_viajero

    # WHEN: El funcionario invoca la búsqueda específica de un ciudadano usando su credencial única
    usuario_consultado = sistema.bd.usuarios.get("18.123.456-7")

    # THEN: El sistema despliega todos sus datos demográficos y la documentación adjunta asociada
    assert funcionario_aduana.institucion == "Aduanas"
    assert usuario_consultado is not None
    assert usuario_consultado.nombre == "Esteban"
    assert len(usuario_consultado.documentos_adjuntos) == 1
    assert usuario_consultado.documentos_adjuntos[0]["tipo"] == "DNI Frente"