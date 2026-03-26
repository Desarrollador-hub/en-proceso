# Despliegue de Infraestructura FTTH Metropolitana con Segmentación L3 y Servicios WAN

## 1. Introducción
Este proyecto representa la implementación de una arquitectura de red de fibra óptica de última milla (FTTH) mediante el simulador Cisco Packet Tracer. Se ha diseñado una topología jerárquica que emula el flujo de tráfico desde un proveedor de servicios (ISP) hasta el terminal del suscriptor, aplicando conceptos avanzados de enrutamiento, traducción de direcciones y servicios de red de capa de aplicación.

## 2. Diagrama de Topología Lógica
La red se divide en tres segmentos críticos:
1. **Core (Borde):** Gestión de salida a Internet y seguridad (NAT/PAT).
2. **Distribución (OLT):** Agregación de tráfico y administración de VLANs mediante un Switch Multicapa 3650.
3. **Acceso (Planta Externa):** Distribución pasiva mediante Splitter óptico (Caja NAP) hacia ONTs de clientes.

## 3. Configuración Técnica de Capas

### Capa de Red (Layer 3)
* **Protocolo de Enrutamiento:** Implementación de rutas estáticas y rutas por defecto (Gateway of Last Resort) para garantizar la convergencia WAN.
* **NAT con Sobrecarga (PAT):** Configuración de traducción de direcciones para permitir la salida concurrente de múltiples usuarios privados (`192.168.10.0/24`) a través de una interfaz pública única (`200.48.1.1`).
* **Inter-VLAN Routing:** Configuración de SVI (Switch Virtual Interface) en la unidad OLT para el aislamiento de tráfico del suscriptor.

### Servicios de Red
* **DHCP Server:** Aprovisionamiento automatizado de direccionamiento IP, máscara y DNS para los terminales de usuario.
* **DNS & HTTP:** Implementación de resolución de nombres de dominio y servidor de contenidos para validación de conectividad extremo a extremo.

## 4. Tabla de Direccionamiento IP

| Dispositivo | Interfaz | Dirección IP | Máscara | Función |
| :--- | :--- | :--- | :--- | :--- |
| **Router_Core** | Gig8/0 | 200.48.1.1 | /30 | Enlace WAN (Internet) |
| **Router_Core** | Gig9/0 | 10.0.0.1 | /30 | Enlace Troncal (OLT) |
| **Switch_OLT** | Gig1/1/1 | 10.0.0.2 | /30 | Puerta de Enlace a Core |
| **Switch_OLT** | VLAN 10 | 192.168.10.1 | /24 | Gateway Clientes FTTH |
| **Server_Web** | Gig0 | 200.48.1.2 | /30 | ISP / DNS Server |

## 5. Validaciones de Ingeniería
Se han realizado pruebas de conectividad satisfactorias (ICMP Echo Request) desde los terminales de usuario hacia el servidor externo, validando la integridad de la tabla NAT y la resolución de nombres DNS.

---
**Autor:** Hurtado - 2026
**Especialidad:** Ingeniería Electrónica - Telecomunicaciones
