# Airline Passenger Satisfaction - Clustering Analysis

## 1. Introducción del problema

Este proyecto tiene como objetivo identificar perfiles de pasajeros aéreos mediante técnicas de agrupamiento no supervisado, a partir de una base de datos de satisfacción del cliente. La finalidad es explorar patrones comunes entre los usuarios que permitan comprender mejor sus comportamientos, necesidades y experiencias de viaje.

## 2. Metodología y técnicas aplicadas

### 2.1 Análisis estadístico

Se utilizó el conjunto de datos de prueba ("test") de la base "Airline Passenger Satisfaction", el cual contiene 25.976 registros. Debido a restricciones de procesamiento en Google Colab, se trabajó con una muestra reducida de 12.322 observaciones. El análisis exploratorio incluyó boxplots e histogramas con curvas de densidad para las 12 variables numéricas. Se detectaron outliers en tres variables: "Flight Distance", "Departure Delay in Minutes" y "Arrival Delay in Minutes". A continuación, se presentan las estadísticas descriptivas de las variables seleccionadas:

| Variable                     | count   | mean       | std        | min | 25% | 50% | 75%   | max   |
|-----------------------------|---------|------------|------------|-----|-----|-----|--------|--------|
| Age                         | 12322.0 | 39.50      | 15.29      | 7.0 | 27.0| 40.0| 51.00  | 85.0   |
| Flight Distance             | 12322.0 | 1089.82    | 891.69     | 31.0| 391.0|780.0| 1603.75| 3568.0 |
| Departure Delay in Minutes | 12322.0 | 0.097      | 0.38       | 0.0 | 0.0 | 0.0 | 0.0    | 2.0    |
| Arrival Delay in Minutes   | 12322.0 | 0.0        | 0.0        | 0.0 | 0.0 | 0.0 | 0.0    | 0.0    |

### 2.2 Visualización de correlaciones y distribución
...
