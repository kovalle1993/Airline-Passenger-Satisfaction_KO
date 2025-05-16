# Airline Passenger Satisfaction - Clustering Analysis

## 1. Introducción del problema

Este proyecto tiene como objetivo identificar perfiles de pasajeros aéreos mediante técnicas de agrupamiento no supervisado, a partir de una base de datos de satisfacción del cliente. La finalidad es explorar patrones comunes entre los usuarios que permitan comprender mejor sus comportamientos, necesidades y experiencias de viaje.

## 2. Metodología y técnicas aplicadas

### 2.1 Análisis estadístico

Se utilizó el conjunto de datos de prueba ("test") de la base "Airline Passenger Satisfaction", el cual contiene 25.976 registros. Debido a restricciones de procesamiento en Google Colab, se trabajó con una muestra reducida de 12.322 observaciones. El análisis exploratorio incluyó boxplots e histogramas con curvas de densidad para las 12 variables numéricas. Se detectaron outliers en tres variables: "Flight Distance", "Departure Delay in Minutes" y "Arrival Delay in Minutes". A continuación, se presentan las estadísticas descriptivas de las variables seleccionadas:

| Variable                   | count   | mean   | std   | min | 25% | 50% | 75%   | max   |
|----------------------------|---------|--------|-------|-----|-----|-----|--------|--------|
| Age                        | 12322.0 | 39.50  | 15.29 | 7.0 | 27.0| 40.0| 51.00  | 85.0   |
| Flight Distance            | 12322.0 | 1089.82| 891.69| 31.0| 391.0|780.0|1603.75| 3568.0 |
| Departure Delay in Minutes| 12322.0 | 0.097  | 0.38  | 0.0 | 0.0 | 0.0 | 0.0    | 2.0    |
| Arrival Delay in Minutes  | 12322.0 | 0.0    | 0.0   | 0.0 | 0.0 | 0.0 | 0.0    | 0.0    |

### 2.2 Visualización de correlaciones y distribución

Se emplearon gráficos de distribución y correlación para entender la relación entre las variables y su comportamiento. Estas visualizaciones permitieron justificar la selección de variables para el análisis de clustering y facilitaron la detección de datos atípicos que podrían distorsionar los modelos.

### 2.3 Eliminación de columnas irrelevantes o transformación de variables

Se descartaron variables categóricas o redundantes, y se seleccionaron únicamente variables numéricas con relación directa al comportamiento logístico del vuelo. Se procedió a escalar las variables para garantizar su comparabilidad. La depuración de outliers se realizó con el método del rango intercuartílico (IQR) en dos iteraciones sucesivas, con lo cual se logró una muestra final libre de atípicos extremos.

## 3. Análisis comparativo entre modelos

### 3.1 K-Means con análisis del número óptimo de clusters

Se aplicó el algoritmo K-Means sobre las variables escaladas: "Age", "Flight Distance", "Departure Delay in Minutes" y "Arrival Delay in Minutes". El número óptimo de clusters fue determinado mediante el método del codo y validado con el coeficiente de Silhouette. Se evaluaron los valores de k = 4 y k = 5, siendo k = 4 el seleccionado por alcanzar un mayor puntaje (0.4431 frente a 0.3868).

| KMeans_Cluster | Age   | Flight Distance | Departure Delay in Minutes | Arrival Delay in Minutes |
|----------------|-------|------------------|-----------------------------|---------------------------|
| 0              | 52.39 | 608.68           | 0.00                        | 0.00                      |
| 1              | 25.33 | 693.36           | 0.00                        | 0.00                      |
| 2              | 43.56 | 2460.85          | 0.0015                      | 0.00                      |
| 3              | 38.90 | 1181.80          | 1.43                        | 0.00                      |

### 3.2 DBSCAN con ajuste de eps y min_samples

Se utilizó DBSCAN para captar formas no esféricas y detectar observaciones ruidosas. Se implementó una grilla de búsqueda con eps = [0.05, 0.25, 0.5, 0.75, 1] y min_samples = [1, 5, 10, 15, 20]. La mejor combinación fue eps = 0.25 y min_samples = 5.

| DBSCAN_Cluster | Age   | Flight Distance | Departure Delay in Minutes | Arrival Delay in Minutes |
|----------------|-------|------------------|-----------------------------|---------------------------|
| 0              | 39.50 | 1080.42          | 0.0                         | 0.0                       |
| 1              | 39.01 | 855.96           | 1.0                         | 0.0                       |
| 2              | 38.75 | 685.79           | 2.0                         | 0.0                       |
| 3              | 34.00 | 2599.70          | 2.0                         | 0.0                       |
| 4              | 8.33  | 850.67           | 2.0                         | 0.0                       |
| 5              | 59.67 | 2201.83          | 2.0                         | 0.0                       |
| 6              | 45.11 | 1972.37          | 2.0                         | 0.0                       |
| 7              | 34.25 | 1860.75          | 2.0                         | 0.0                       |
| 8              | 21.79 | 2206.71          | 2.0                         | 0.0                       |
| 9              | 40.05 | 2355.32          | 1.0                         | 0.0                       |
| 10             | 29.31 | 2099.85          | 1.0                         | 0.0                       |
| 11             | 32.80 | 2670.40          | 1.0                         | 0.0                       |
| 12             | 29.50 | 2080.00          | 2.0                         | 0.0                       |
| 13             | 46.00 | 3380.50          | 2.0                         | 0.0                       |
| 14             | 21.00 | 2192.20          | 1.0                         | 0.0                       |

### 3.3 PCA para reducción lineal y visualización 2D

Para facilitar la visualización y validación de los resultados de clustering, se aplicó PCA con dos componentes principales. En los resultados de K-Means, los grupos se visualizaron con formas relativamente compactas y bien separadas. En contraste, los clusters de DBSCAN mostraron mayor dispersión y formas irregulares, revelando estructuras de densidad más complejas.

### 3.4 t-SNE para detección visual de agrupamientos complejos

Se utilizó t-SNE con diferentes configuraciones. Los mejores resultados se lograron con perplexity = 30 y learning rate = 200. Los clusters de K-Means aparecieron como islas diferenciadas, mientras que los resultados de DBSCAN mostraron una estructura más orgánica con zonas de alta densidad bien delimitadas y áreas intermedias ocupadas por puntos considerados ruido.

## 4. Conclusiones y recomendaciones

El análisis permitió identificar perfiles como: adultos mayores con vuelos cortos sin demoras, jóvenes en vuelos medianos, adultos en trayectos largos sin incidentes y pasajeros con mayores demoras en salida. DBSCAN permitió detectar microgrupos como niños o adultos mayores en vuelos intercontinentales. Las diferencias clave entre ambos modelos radican en su sensibilidad a la forma y densidad de los datos.

Entre las principales limitaciones se encuentra la necesidad de reducir el tamaño de la muestra por restricciones computacionales y la exclusión de variables categóricas. Se recomienda para futuras investigaciones utilizar algoritmos como HDBSCAN o GMM, incorporar variables cualitativas transformadas y ampliar la muestra para evaluar la robustez de los resultados.
