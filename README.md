# 🌾 Predicción de la Humedad de Suelo a Distintas Profundidades Mediante Modelado en Cascada

[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-111111?style=for-the-badge&logo=xgboost&logoColor=white)](https://xgboost.readthedocs.io/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)

Este repositorio contiene la implementación de una arquitectura de **Machine Learning secuencial (en cascada)** para estimar la humedad del suelo en horizontes profundos (**60 cm y 100 cm**) utilizando únicamente **datos meteorológicos superficiales** y la lectura de un **sensor físico a 20 cm**. 

Esta solución de **Sensor Virtual** reduce hasta en un **66.6% el costo de instrumentación en campo**, eliminando la necesidad de instalar sondas subterráneas profundas de alto costo y difícil mantenimiento.

---

## Arquitectura del Modelo (Pipeline en Cascada)

El flujo de trabajo se basa en un modelado jerárquico donde la predicción de la capa intermedia alimenta el siguiente nivel:

### Modelos Evaluados:
* **Regresión Lineal Múltiple** (Modelo Baseline / Ganador)
* **Random Forest Regressor**
* **XGBoost Regressor**
* **Support Vector Regression (SVR)**

---

## Principales Hallazgos

| Estación | Modelo Ganador (60 cm) | $R^2$ Score (60 cm) | Modelo Ganador (100 cm) | $R^2$ Score (100 cm) |
| :--- | :--- | :---: | :--- | :---: |
| **Estación 1** | **Regresión Lineal** | **0.9205** | Random Forest | **0.7989** |
| **Estación 2** | **Regresión Lineal** | **0.6545** | **Regresión Lineal** | **0.7735** |
| **Estación 3** | **Regresión Lineal** | **0.5402** | **Regresión Lineal** | **0.4456** |

### Conclusiones Clave:
1. **Dominio de la Regresión Lineal:** A pesar de la complejidad de los algoritmos de ensamble (RF, XGBoost), la Regresión Lineal Múltiple demostró la mayor estabilidad matemática e inmunidad al sobreajuste frente a cambios de edafología.
2. **Sensibilidad al Tipo de Suelo:** La variabilidad en las métricas entre estaciones confirmó la presencia de dinámicas de infiltración no lineales e histéresis hídrica en suelos con mayor contenido de arcilla o compactación.
3. **Propagación del Error:** El esquema secuencial valida la estimación profunda a 100 cm, aunque confirma la acumulación progresiva del error cuadrático medio (RMSE) a medida que se desciende en el perfil.

---
