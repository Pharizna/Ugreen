# Arquitectura de red – UGREEN DXP2800 GT

Este documento describe la arquitectura de red utilizada en el NAS **UGREEN DXP2800 GT** durante la revisión técnica. Incluye la relación entre UGOS, Pi-hole, Unbound, la red interna de Docker y la red doméstica.

---

## 1. Visión general

La arquitectura de red del sistema se basa en tres capas:

1. **Red doméstica (LAN)**  
   Donde se encuentran los dispositivos del usuario: ordenadores, móviles, IoT, televisores, etc.

2. **UGOS (sistema operativo del NAS)**  
   Gestiona la conectividad del DXP2800 GT, los servicios internos y los contenedores.

3. **Contenedores Docker**  
   Ejecutan Pi-hole y Unbound en una red interna aislada.

El flujo general es:
Clientes LAN → Pi-hole → Unbound → Servidores raíz DNS

---

## 2. Red doméstica (LAN)

El NAS UGREEN DXP2800 GT se integra en la red doméstica mediante su interfaz Ethernet.  
En esta red se encuentran:

- ordenadores  
- móviles  
- dispositivos IoT  
- televisores  
- routers y switches  

Los clientes envían sus consultas DNS al NAS, donde Pi-hole actúa como servidor DNS principal.

---

## 3. UGOS y su papel en la arquitectura

UGOS es el sistema operativo del NAS y proporciona:

- gestión de red  
- firewall básico  
- sistema de proyectos (contenedores)  
- monitorización  
- servicios internos del NAS  

UGOS expone el contenedor de Pi-hole en la LAN, mientras que Unbound permanece aislado en una red interna.

---

## 4. Red interna de Docker (`dns_net`)

Pi-hole y Unbound se comunican mediante una red interna definida en el `docker-compose.yaml`:
dns_net:
driver: bridge

Características:

- Aislada de la LAN  
- Solo accesible entre contenedores  
- Evita fugas de tráfico DNS  
- Permite comunicación segura entre Pi-hole y Unbound  

---

## 5. Flujo de consultas DNS

### **1. Cliente LAN → Pi-hole**

Los dispositivos de la red doméstica envían sus consultas DNS al NAS:
192.168.X.X → puerto 53 → Pi-hole

Pi-hole recibe la consulta, aplica bloqueos y estadísticas.

### **2. Pi-hole → Unbound**

Si la consulta no está bloqueada ni en caché:
Pi-hole → dns_net → Unbound:53

Pi-hole utiliza:
FTLCONF_dns_upstreams: "unbound#53"

### **3. Unbound → Servidores raíz**

Unbound realiza resolución recursiva completa:
Unbound → root servers → authoritative servers → respuesta

### **4. Respuesta → Pi-hole → Cliente**

La respuesta vuelve a Pi-hole, que:

- registra estadísticas  
- aplica reglas  
- devuelve la respuesta al cliente  

---

## 6. Componentes principales

### **Pi-hole**
- Servidor DNS principal para la LAN  
- Bloqueo de publicidad, malware y telemetría  
- Estadísticas y panel web  
- Caché DNS local  

### **Unbound**
- Resolver recursivo  
- DNSSEC  
- Root hints  
- Caché independiente  
- No depende de proveedores externos  

### **UGOS**
- Orquestación de contenedores  
- Gestión de red  
- Interfaz de administración  

---

## 7. Diagrama de arquitectura
┌───────────────────────────────┐
│         Red doméstica         │
│  (PC, móviles, IoT, TV, etc.) │
└───────────────┬───────────────┘
│ DNS
▼
┌─────────────────┐
│     Pi-hole     │  ← expuesto en LAN
│  (contenedor)   │
└─────────┬───────┘
│ DNS interno
▼
┌─────────────────┐
│     Unbound     │  ← aislado en dns_net
│  (contenedor)   │
└─────────┬───────┘
│ resolución recursiva
▼
┌─────────────────┐
│  Root servers   │
└─────────────────┘

---

## 8. Ventajas de esta arquitectura

- **Privacidad total**: no se usan DNS externos.  
- **Aislamiento**: Unbound no está expuesto a la LAN.  
- **Seguridad**: DNSSEC habilitado.  
- **Rendimiento**: caché combinada Pi-hole + Unbound.  
- **Control**: Pi-hole centraliza estadísticas y bloqueos.  
- **Reproducibilidad**: configuración portable mediante Docker.

---

## 9. Relación con otros documentos del repositorio

Este archivo complementa:

- `docs/unbound_config.md`  
- `docs/pihole_databases.md`  
- `docs/hardware_notes.md`  
- `colab/ugreen.ipynb`  

---

## 10. Objetivo del documento

Proporcionar una referencia técnica clara sobre la arquitectura de red utilizada en el **UGREEN DXP2800 GT**, útil para reproducir la configuración, entender el flujo DNS y documentar el entorno utilizado en la revisión publicada en PCDEMANO.

