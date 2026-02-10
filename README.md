# DS-Challenge3
# Auditoría Analítica y Optimización de Redes: TechLogistics S.A.

Este proyecto documenta una auditoría integral de datos agrícolas y energéticos para la optimización de infraestructura y toma de decisiones en el Oriente Antioqueño. El análisis combina procesamiento de señales, teoría de grafos y modelos econométricos para diagnosticar fallas sistémicas y proponer mejoras de inversión.

## 📊 Resumen del Proyecto
La auditoría se centró en resolver tres problemáticas principales:
1.  **Baja Biomasa**: Identificación de causas para el bajo rendimiento agrícola en zonas específicas.
2.  **Integridad de Datos**: Limpieza de ruido en sensores IoT de humedad y energía.
3.  **Vulnerabilidad de Infraestructura**: Análisis de redes para detectar puntos únicos de falla y predecir demanda.

---

## 🛠️ Stack Tecnológico
* **Lenguajes**: Python 3.12
* **Análisis de Datos**: Pandas, NumPy
* **Procesamiento de Señales**: SciPy (FFT, Filtros Butterworth, Espectrogramas)
* **Teoría de Grafos**: NetworkX
* **Modelado Estadístico**: Statsmodels (ADF, Granger Causality, SARIMAX)
* **Métricas de Error**: Scikit-learn (RMSE)

---

## 🔍 Hallazgos Principales

### 1. Diagnóstico Agrónomo y Geoespacial
* **Clúster Crítico**: Se localizó un grupo de sensores con bajo NDVI en un radio de **6.6 km** ($Std \approx 0.06^\circ$).
* **Causa Raíz**: El análisis de correlación (-0.03) descartó la falta de agua como causa. Se determinó que la baja biomasa se debe a la **pérdida de humedad por escurrimiento en pendientes** elevadas, validado por la alta varianza del viento en la variable `Agro_10`.
* **Recomendación**: Invertir en sistemas de **micro-goteo presurizado** para asegurar la absorción radicular antes de que el agua se desplace por la gravedad.



### 2. Procesamiento de Señales (DSP)
* **Filtrado Butterworth**: Se implementó un filtro de paso bajo en la serie `Agro_3` (Humedad), logrando reducir el **RMSE de 3.34 a 1.61**. Esto mejoró la fidelidad de la señal en un **51.7%**, optimizando la capacidad predictiva de los modelos.
* **Análisis Espectral**: Mediante FFT y espectrogramas, se identificó que el ruido inyectado en la generación eólica (`Ener_4`) se concentra en frecuencias de **0.1 a 0.5 Hz**.

### 3. Análisis de Redes y Causalidad
* **Punto Crítico de Falla**: El **Nodo 106** fue identificado como el principal "Hub" de la red, con una centralidad de grado que conecta al **62.3% de los sensores**.
* **Causalidad de Granger**: Se demostró que las variaciones en el Factor de Potencia (`Ener_10`) preceden y causan inestabilidad en el Voltaje (`Ener_9`) con un **retraso de 4 a 5 periodos** ($p < 0.02$).



### 4. Analítica Predictiva (ARIMAX)
* **Modelo de Demanda**: Se ajustó un modelo ARIMAX para `Ener_1` comparando variables exógenas.
* **Conclusión de AIC**: El modelo que solo utiliza **Temperatura** ($AIC: 8752.76$) resultó más eficiente que el que incluía Centralidad de Grado ($AIC: 8752.78$). Esto sugiere que, para este conjunto de datos, la jerarquía del nodo no aporta información predictiva adicional significativa, priorizando la parsimonia del modelo.

---

## 📈 Conclusiones Finales
La infraestructura de TechLogistics S.A. presenta una dependencia crítica del **Nodo 106**. La ventana de **4 periodos** detectada mediante el test de Granger ofrece una oportunidad técnica para mitigar fallos de voltaje antes de que ocurran. Se recomienda la modernización hídrica en el clúster de 6.6 km para estabilizar los activos biológicos.

---
**Fecha**: Febrero 2026
