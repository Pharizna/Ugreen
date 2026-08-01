# UGOS – Notas técnicas y comportamiento en el UGREEN DXP2800 GT

Este documento recoge notas técnicas, observaciones y comportamientos relevantes del sistema operativo **UGOS** tal y como se ha utilizado en el NAS **UGREEN DXP2800 GT** durante la revisión.  
Su objetivo es servir como referencia técnica complementaria para entender cómo UGOS gestiona contenedores, red, almacenamiento y monitorización.

---

## 1. Sistema de proyectos (contenedores)

UGOS utiliza un sistema propio para gestionar contenedores, diferente de Docker Compose estándar.

### Características observadas
- Editor integrado para pegar configuraciones YAML.  
- Gestión automática de redes internas.  
- Logs accesibles desde la interfaz.  
- Reinicio automático de contenedores en caso de fallo.  
- Volúmenes persistentes gestionados por UGOS sin necesidad de configuración externa.

### Notas relevantes
- El sistema interpreta correctamente `docker-compose.yaml` siempre que no incluya funciones avanzadas de Compose.  
- Las redes internas (como `dns_net`) se crean automáticamente.  
- Los contenedores se reinician de forma fiable tras actualizaciones del NAS.

---

## 2. Monitorización del sistema

UGOS proporciona monitorización integrada de:

- temperatura de CPU  
- carga del sistema  
- uso de memoria  
- estado de discos  
- velocidad del ventilador  

### Observaciones
- Los sensores del modelo GT son precisos y estables.  
- La lectura de temperatura coincide con la reportada por el notebook del repositorio.  
- El ventilador responde correctamente a incrementos de carga.

---

## 3. Gestión de red

UGOS gestiona la red del NAS y expone servicios de forma controlada.

### Comportamiento observado
- Pi-hole se expone correctamente en la LAN.  
- Unbound permanece aislado en la red interna `dns_net`.  
- No se detectaron fugas de tráfico DNS.  
- Wake-on-LAN funciona de forma consistente desde Windows, iPhone y Home Assistant.

---

## 4. Almacenamiento y volúmenes

UGOS gestiona:

- discos SATA  
- RAID  
- volúmenes internos  
- almacenamiento del sistema operativo  

### Notas
- Los volúmenes de contenedores (`etc-pihole`, `etc-dnsmasq`, `unbound`) se mantienen tras reinicios.  
- No se observaron problemas de permisos en los contenedores utilizados.  
- El rendimiento de I/O fue estable durante toda la revisión.

---

## 5. Logs y diagnóstico

UGOS ofrece acceso a:

- logs de contenedores  
- eventos del sistema  
- estado de servicios internos  

### Observaciones
- Los logs de Pi-hole y Unbound se integran correctamente en la interfaz.  
- Los eventos del sistema ayudan a identificar reinicios o actualizaciones.  
- No se detectaron errores persistentes durante las pruebas.

---

## 6. Actualizaciones del sistema

UGOS recibe actualizaciones OTA.

### Notas
- Las actualizaciones no afectaron a los contenedores desplegados.  
- El sistema mantuvo la configuración de red y volúmenes sin cambios.  
- No se observaron regresiones en rendimiento o estabilidad.

---

## 7. Relación con otros documentos del repositorio

Este archivo complementa:

- `docs/network_architecture.md`  
- `docs/services_overview.md`  
- `docs/hardware_notes.md`  
- `docs/pihole_databases.md`  
- `docs/unbound_config.md`

---

## 8. Objetivo del documento

Proporcionar un espacio para documentar el comportamiento real de **UGOS** en el **UGREEN DXP2800 GT**, útil para reproducir la configuración, entender el entorno de pruebas y registrar observaciones técnicas que no encajan en otros documentos del repositorio.
