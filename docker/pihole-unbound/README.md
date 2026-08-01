# Carpeta `docker/pihole-unbound` – Configuración para UGREEN DXP2800 GT

Esta carpeta contiene el archivo `docker-compose.yaml` utilizado para desplegar Pi-hole y Unbound en el NAS **UGREEN DXP2800 GT** mediante la interfaz de proyectos de UGOS.

## Contenido

- **docker-compose.yaml**  
  Archivo con la configuración completa de Pi-hole + Unbound adaptada al modelo GT.  
  Incluye:
  - puertos expuestos  
  - volúmenes persistentes  
  - red interna para comunicación segura  
  - parámetros FTL  
  - upstream DNS apuntando a Unbound  

## Uso en UGOS (DXP2800 GT)

El archivo `docker-compose.yaml` no se ejecuta mediante Docker Compose estándar.  
UGOS utiliza su propio sistema de gestión de contenedores:

1. Abrir la interfaz del NAS UGREEN DXP2800 GT.  
2. Ir a **Proyectos**.  
3. Crear un nuevo proyecto.  
4. Copiar y pegar el contenido del `docker-compose.yaml` en el editor.  
5. Guardar y desplegar.

## Volúmenes persistentes

El modelo GT mantiene los datos de Pi-hole en:

./etc-pihole:/etc/pihole
./etc-dnsmasq:/etc/dnsmasq.d


Esto garantiza que:

- las bases de datos (`gravity.db`, `pihole-FTL.db`)  
- las listas (`adlists.list`, `regex.list`)  
- la configuración (`setupVars.conf`)  

permanezcan intactas tras reinicios o actualizaciones del contenedor.

## Nota

Este archivo se incluye únicamente como referencia técnica y para facilitar la reproducción del entorno utilizado durante la revisión del **UGREEN DXP2800 GT**.

