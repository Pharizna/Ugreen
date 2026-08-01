# Unbound – Configuración técnica y funcionamiento en el UGREEN DXP2800 GT

Este documento describe la configuración técnica de **Unbound** utilizada en el NAS UGREEN DXP2800 GT como servidor DNS recursivo local.  
Incluye arquitectura, parámetros clave, archivos relevantes y notas de funcionamiento dentro del entorno UGOS + Pi-hole.

---

## 1. ¿Qué es Unbound?

Unbound es un **resolver DNS recursivo** diseñado para ser:

- rápido  
- ligero  
- seguro  
- validado con DNSSEC  
- independiente de proveedores externos  

En esta configuración, Unbound actúa como **upstream DNS de Pi-hole**, permitiendo resolver dominios directamente contra los servidores raíz sin depender de Google, Cloudflare, Quad9 u otros servicios.

---

## 2. Arquitectura en el DXP2800 GT

La arquitectura utilizada en el NAS es:

Pi-hole → Unbound → Servidores raíz DNS


Ambos servicios se ejecutan en contenedores Docker dentro de UGOS, comunicándose mediante una red interna:
dns_net

Esto garantiza:

- aislamiento  
- seguridad  
- tráfico DNS no expuesto al exterior  
- resolución local optimizada  

---

## 3. Archivo de configuración de Unbound

El archivo principal es:
/opt/unbound/unbound.conf

En el contenedor se monta mediante:
./unbound:/opt/unbound


A continuación se documentan los parámetros más relevantes.

---

## 4. Parámetros clave de `unbound.conf`

### **server:**
Configuración principal del servidor Unbound.

server:
verbosity: 1
interface: 0.0.0.0
port: 53
do-ip4: yes
do-ip6: no
do-udp: yes
do-tcp: yes

### **Seguridad y privacidad**
hide-identity: yes
hide-version: yes
harden-glue: yes
harden-dnssec-stripped: yes
harden-referral-path: yes

### **DNSSEC**
auto-trust-anchor-file: "/var/lib/unbound/root.key"

### **Optimización**
prefetch: yes
prefetch-key: yes
minimal-responses: yes
num-threads: 2

### **Cache**
cache-min-ttl: 3600
cache-max-ttl: 86400


### **Root hints**
El archivo `root.hints` se incluye en:
/opt/unbound/root.hints

y se referencia así:
root-hints: "/opt/unbound/root.hints"


---

## 5. Integración con Pi-hole

Pi-hole se configura para usar Unbound como DNS upstream mediante:

FTLCONF_dns_upstreams: "unbound#53"

Esto implica:

- Pi-hole recibe consultas DNS de los clientes  
- Las reenvía a Unbound dentro de `dns_net`  
- Unbound realiza resolución recursiva completa  
- Pi-hole registra estadísticas y bloqueos  
- No se utilizan DNS externos  

---

## 6. Volúmenes persistentes

El volumen de Unbound se define como:
./unbound:/opt/unbound

Esto permite:

- mantener `unbound.conf`  
- conservar `root.hints`  
- almacenar la clave DNSSEC (`root.key`)  
- persistir cualquier ajuste adicional  

---

## 7. Archivos relevantes

### **unbound.conf**
Configuración principal del servidor.

### **root.hints**
Lista de servidores raíz DNS.

### **root.key**
Clave DNSSEC generada automáticamente.

### **logfile (opcional)**
Si se habilita:
logfile: "/opt/unbound/unbound.log"

---

## 8. Notas de funcionamiento en el DXP2800 GT

- El modelo GT tiene potencia suficiente para ejecutar Unbound sin impacto en rendimiento.  
- La resolución recursiva suele tardar entre 20–40 ms en la primera consulta.  
- Las consultas posteriores se sirven desde caché en 1–3 ms.  
- DNSSEC funciona correctamente en UGOS sin configuraciones adicionales.  
- La red interna `dns_net` evita fugas de tráfico DNS.

---

## 9. Objetivo del documento

Este archivo sirve como referencia técnica para entender y reproducir la configuración de Unbound utilizada en el NAS **UGREEN DXP2800 GT** durante la revisión publicada en PCDEMANO.











