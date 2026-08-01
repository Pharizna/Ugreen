# Carpeta `colab` – Análisis CPU ↔ Temperatura del NAS UGREEN DXP2800 GT

Esta carpeta contiene todos los recursos necesarios para reproducir el análisis térmico realizado sobre el NAS **UGREEN DXP2800 GT**, incluyendo el notebook, los datos originales y las figuras generadas.

## Contenido

- **ugreen.ipynb**  
  Notebook de análisis CPU ↔ temperatura.  
  Incluye carga de datos, gráficas, correlaciones y evaluación del comportamiento térmico del modelo GT bajo diferentes condiciones.

- **history.csv**  
  Fichero de datos utilizado por el notebook.  
  Contiene el histórico de temperatura y carga del sistema del DXP2800 GT.

- **figura1.png**  
  Primera figura generada por el notebook (visualización principal del análisis).

- **figura2.png**  
  Segunda figura generada por el notebook (gráfica complementaria).

## Cómo reproducir el análisis

1. Descarga `ugreen.ipynb` y `history.csv` o <i>genera este fichero de datos directamente desde Home Assistant</i>.  
2. Abre el notebook en Jupyter, VS Code o Google Colab.  
3. Asegúrate de que `history.csv` está en la misma carpeta que el notebook.  
4. Ejecuta todas las celdas para regenerar las figuras.

## Nota

Este análisis forma parte de la revisión publicada en PCDEMANO.  
Aquí se incluyen únicamente los recursos técnicos necesarios para reproducir las gráficas y el estudio térmico del **UGREEN DXP2800 GT**.
