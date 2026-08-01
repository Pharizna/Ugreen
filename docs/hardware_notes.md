# Hardware del UGREEN DXP2800 GT – Notas técnicas

Este documento recoge las notas de hardware más relevantes del NAS **UGREEN DXP2800 GT**, incluyendo CPU, memoria, almacenamiento, ventilación, sensores térmicos y consideraciones prácticas observadas durante las pruebas.

---

## 1. CPU y arquitectura

El UGREEN DXP2800 GT utiliza un procesador x86 de bajo consumo orientado a NAS doméstico y semiprofesional.  
Características observadas:

- Arquitectura x86_64  
- Soporte completo para virtualización ligera (Docker, contenedores UGOS)  
- Capacidad suficiente para ejecutar servicios simultáneos sin saturación  
- Comportamiento térmico estable incluso bajo carga sostenida

Durante las pruebas térmicas, el procesador mostró una relación lineal entre carga y temperatura, documentada en el notebook del repositorio.

---

## 2. Memoria RAM

El modelo GT incorpora memoria RAM ampliada respecto a versiones anteriores:

- RAM suficiente para ejecutar Pi-hole, Unbound, contenedores adicionales y servicios UGOS sin swapping  
- Latencias estables bajo carga  
- No se observaron cuellos de botella relacionados con memoria

---

## 3. Almacenamiento interno y bahías

El DXP2800 GT incluye:

- Bahías para discos SATA  
- Soporte para configuraciones RAID mediante UGOS  
- Almacenamiento interno para el sistema operativo  
- Rendimiento adecuado para uso doméstico y semiprofesional

Durante las pruebas no se detectaron problemas de I/O ni saturación del bus SATA.

---

## 4. Ventilación y disipación térmica

El sistema de ventilación del GT es notablemente mejor que el de modelos anteriores:

- Ventilador principal con control automático  
- Flujo de aire suficiente para mantener CPU y discos en rangos seguros  
- Ruido moderado incluso bajo carga  
- Disipador interno bien dimensionado para el TDP del procesador

Las gráficas del notebook muestran que el ventilador responde correctamente a incrementos de temperatura.

---

## 5. Sensores térmicos

El NAS expone sensores térmicos accesibles desde UGOS:

- Sensor de CPU  
- Sensor de placa base  
- Sensor de discos (dependiendo del modelo)  

Estos datos se utilizaron para generar el archivo `history.csv` incluido en el repositorio.

---

## 6. Conectividad

El DXP2800 GT incluye:

- Puertos USB para expansión  
- Conectividad de red estable  
- Soporte para Wake-on-LAN (probado y documentado en el repositorio)  
- Compatibilidad con dispositivos externos como coordinadores Zigbee LAN

---

## 7. Consideraciones prácticas observadas

Durante las pruebas se observaron:

- Excelente estabilidad térmica incluso con contenedores múltiples  
- Rendimiento consistente en Pi-hole + Unbound  
- Comportamiento predecible del ventilador  
- Ausencia de throttling térmico  
- Buen aislamiento del ruido y vibraciones

---

## 8. Relación con otros documentos del repositorio

Este archivo complementa:

- `colab/ugreen.ipynb` (análisis térmico)  
- `docs/pihole_databases.md` (servicios DNS)  
- `docs/unbound_config.md` (resolver recursivo)  

---

## 9. Objetivo del documento

Proporcionar una referencia técnica clara sobre el hardware del **UGREEN DXP2800 GT**, útil para reproducir pruebas, entender el comportamiento térmico y documentar el entorno utilizado en la revisión publicada en PCDEMANO.
