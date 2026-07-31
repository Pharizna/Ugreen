# Carpeta `docker/pihole-unbound`

Esta carpeta contiene el archivo `docker-compose.yaml` utilizado para desplegar Pi-hole y Unbound en el NAS UGREEN DXP2800 mediante la interfaz de proyectos de UGOS.

## Contenido

- **docker-compose.yaml**  
  Archivo con la configuración de Pi-hole y Unbound.  
  Incluye puertos, volúmenes, red interna y dependencias entre servicios.

## Uso en UGOS

El archivo `docker-compose.yaml` no se ejecuta mediante Docker Compose estándar.  
UGOS utiliza su propio sistema de gestión de contenedores:

1. Abrir la interfaz del NAS UGREEN.  
2. Ir a *Proyectos*.  
3. Crear un nuevo proyecto.  
4. Copiar y pegar el contenido del `docker-compose.yaml` en el editor.  
5. Guardar y desplegar.

## Nota

Este archivo se incluye únicamente como referencia técnica y para facilitar la reproducción del entorno utilizado durante la revisión del NAS.

