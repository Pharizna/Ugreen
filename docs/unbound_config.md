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

