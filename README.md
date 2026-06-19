# Análisis y Predicción de Ventas en una Tienda de Retail

## Objetivo
Realizar un análisis exploratorio de datos (EDA) completo, preprocesamiento y benchmarking de técnicas de machine learning para predecir ventas en una tienda de retail. Además, generar un análisis de métricas y crear una presentación one-page para explicar los resultados. 

## Descripción
Este proyecto documenta la "Paradoja del Machine Learning", evaluando cómo la inclusión o exclusión de la variable `Price per Unit` determina la viabilidad de los modelos predictivos. Se demuestra que ante una identidad matemática determinista ($Total = Cantidad \times Precio$), los modelos alcanzan perfección técnica sin necesidad de aprendizaje real, mientras que en ausencia de la variable causal, el rendimiento colapsa a niveles cercanos al azar.

## Estructura del Repositorio
Siguiendo los estándares de la versión **v1.0.0**:

*   **`/data`**: Contiene `dataset.csv` con los datos transaccionales originales.
*   **`/notebooks`**:
    *   `analisis_prediccion_ventas.ipynb`: Carga, exploración inicial, tratamiento de nulos/outliers y mapas de calor de correlación. Transformación de columnas  y creación de Pipelines para automatización. Entrenamiento de 6 modelos (Regresión Logística, KNN, Árbol de Decisión, Random Forest, XGBoost y LGBM), optimización con GridSearchCV e infome con conclusiones.
*   **`/reports`**: 
    *   `classification_report.txt`: Resumen de métricas de rendimiento por modelo.
    *   `confusion_matrix_con_PricePerUnit.png`: Visualización de errores CON la variable 'Price per Unit'.
    *   `confusion_matrix_sin_PricePerUnit.png`: Visualización de errores SIN utilizar la variable 'Price per Unit'.    
    *   `roc_curve.png`: Curva ROC y cálculo de AUC para evaluar la capacidad de distinción entre clases.
*   **`/presentation`**: 
    *   `onepage_presentation.pptx`: Presentación ejecutiva que resume objetivos, metodología, hallazgos clave y recomendaciones.
*   **`README.md`**: Documentación general del proyecto.
*   **`requirements.txt`**: Instalación de librerías.

## Principales Hallazgos
*   **Escenario Determinista (Con Precio):** Modelos como **XGBoost y Decision Tree lograron un Accuracy de 1.0000**. Esto confirma que los algoritmos simplemente codificaron una regla de negocio matemática.
*   **Colapso Predictivo (Sin Precio):** El rendimiento máximo fue de **50.5% de Accuracy** con Random Forest. La optimización con GridSearchCV solo logró mejoras marginales del 3-5%, lo que se define como una "optimización de ruido".
*   **Importancia de Variables:** Existe un consenso técnico en que **`num__Quantity`** es la única variable con poder predictivo legítimo entre todos los modelos evaluados.

## Instrucciones para Ejecutar
Para reproducir los resultados de este proyecto:

1.  **Clonar el repositorio y crear un entorno virtual:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # En Windows: venv\Scripts\activate
    ```
2.  **Instalar dependencias:**
    ```bash
    pip install --upgrade pip
    pip install -r requirements.txt
    ```
3.  **Ejecutar los Notebooks:**
    Siga el orden lógico: `EDA.ipynb` -> `Preprocessing.ipynb` -> `Benchmarking.ipynb`.

## Recomendaciones Finales para el negocio
*   **No utilizar Machine Learning** si se dispone de la variable de precio; se recomienda implementar directamente la regla de negocio: $Sales Category = cut(Quantity \times Price)$.
*   Si no se dispone de precio, el modelo no es apto para automatización debido a su bajo rendimiento (53% accuracy optimizado).  

## Autor
Álvaro Ortega Hamel

## Licencia
Este proyecto se distribuye bajo la **Licencia MIT**.