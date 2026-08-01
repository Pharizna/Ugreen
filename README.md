# UGREEN DXP2800 GT – Recursos técnicos

Este repositorio contiene los recursos técnicos utilizados durante la revisión del NAS **UGREEN DXP2800 GT** publicada en PCDEMANO.  
Incluye la configuración real de Pi-hole + Unbound en UGOS, datos y notebooks de análisis térmico, documentación auxiliar y material reproducible.

## Contenido del repositorio

### **docker/**
Configuración de contenedores utilizada en el NAS UGREEN DXP2800 GT.

- **pihole-unbound/**  
  Contiene el archivo `docker-compose.yaml` empleado en la interfaz de proyectos de UGOS para desplegar Pi-hole y Unbound.  
  Incluye puertos, volúmenes, redes y parámetros FTL.

### **colab/**
Material del análisis térmico del DXP2800 GT.

- **ugreen.ipynb**  
  Notebook con el análisis CPU ↔ temperatura.  
- **history.csv**  
  Datos originales utilizados en el notebook.  
- **figura1.png / figura2.png**  
  Figuras generadas automáticamente por el notebook.

### **docs/**
Documentación técnica complementaria.

- **pihole_databases.md**  
  Bases de datos internas de Pi-hole, listas utilizadas y configuración DNS con Unbound.  
- Otros documentos técnicos relacionados con metodología térmica, hardware y configuración del sistema.

## Objetivo del repositorio

Centralizar todos los recursos técnicos utilizados durante la revisión del **UGREEN DXP2800 GT**, permitiendo:

- reproducir el análisis térmico,  
- consultar la configuración real de Pi-hole + Unbound,  
- acceder a documentación técnica adicional,  
- facilitar la transparencia y replicabilidad del proceso de pruebas.

## Nota

Este repositorio contiene únicamente material técnico.  
La revisión completa, conclusiones y análisis se publican en PCDEMANO.

## Licencia

MIT

