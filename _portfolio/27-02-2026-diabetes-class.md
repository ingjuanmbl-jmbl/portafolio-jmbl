# 🩺 Predicción de Diabetes en Bucaramanga con Machine Learning

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-%23F9A825.svg?style=for-the-badge&logo=googlecolab&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-%23337AB7.svg?style=for-the-badge&logo=xgboost&logoColor=white)
![Estado](https://img.shields.io/badge/Estado-En%20Revisi%C3%B3n%20Editorial-orange?style=for-the-badge)

> **Investigación académica en revisión editorial** — Corporación Unificada Nacional de Colombia (CUN), 2026.

---

## ¿De qué trata este proyecto?

La diabetes mellitus es una de las enfermedades crónicas con mayor impacto en los sistemas de salud a nivel global. En Colombia, su diagnóstico tardío genera una carga clínica y económica considerable tanto para los pacientes como para las instituciones de salud pública.

Este proyecto nació con una pregunta concreta: **¿es posible predecir el riesgo de diabetes en la población de Bucaramanga usando exclusivamente datos abiertos del gobierno colombiano?**

Para responderla, diseñé y ejecuté un pipeline completo de ciencia de datos — desde la extracción automatizada de datos hasta la comparación sistemática de modelos de clasificación — con el objetivo de identificar qué algoritmo ofrece el mejor desempeño para la detección temprana de esta enfermedad en un contexto de salud pública local.

---

## El dataset

Los datos provienen del **Portal de Datos Abiertos del Estado Colombiano**, del conjunto titulado *"39. Enfermedades crónicas en el municipio de Bucaramanga"*, administrado por la Alcaldía de Bucaramanga.

| Característica | Detalle |
|----------------|---------|
| Registros | 110.693 |
| Variables | 22 (clínicas y sociodemográficas) |
| Variable objetivo | Presencia de diabetes (binaria) |
| Fuente | [datos.gov.co](https://www.datos.gov.co/Salud-y-Protecci-n-Social/39-Enfermedades-cr-nicas-en-el-municipio-de-Bucara/4iz7-suhz/about_data) |

El acceso al dataset se realizó de forma completamente automatizada mediante la **API Socrata (SODA)** con la librería `sodapy`, utilizando paginación dinámica para garantizar la descarga íntegra de los registros sin saturar el servidor.

---

## Lo que hice: pipeline completo en dos fases

### Fase 1 — ETL y Análisis Exploratorio (EDA)

El dataset presentaba varios retos de calidad de datos que debieron resolverse antes de modelar:

- **Valores faltantes no estándar:** los nulos no estaban codificados como `NaN` sino como la etiqueta textual `'NO DISPONIBLE'`. Se aplicó normalización semántica para convertirlos al formato estándar y posteriormente se eliminaron, representando menos del 2% del total de registros.
- **Inconsistencias en variables categóricas:** la variable `TIPO_ERC` contenía múltiples etiquetas para una misma modalidad clínica (ej. variantes textuales de hemodiálisis, diálisis peritoneal, prediálisis). Se realizó estandarización semántica y agrupación bajo categorías unificadas.
- **Codificación de variables:** las variables binarias se codificaron como `0/1` y las variables multiclase (`ciclo_de_vida`, `tipo_erc_limpio`, `erc_trr_limpio`, `régimen`) se procesaron con **One-Hot Encoding** usando `drop='first'` para evitar multicolinealidad perfecta, garantizando compatibilidad tanto con modelos lineales como con modelos de árbol.
- **Validación estadística:** se aplicó la **prueba Chi-cuadrado (χ²) de Pearson** e **Información Mutua (MI)** para evaluar la relevancia de cada variable respecto a la variable objetivo. La mayoría de predictores presentaron `p < 0.001`. Variables con menor significancia bivariada, como `SEXO` e `INSUFICIENCIA CARDIACA`, se conservaron para permitir que los modelos de ensamble capturen interacciones multivariadas no detectables con pruebas individuales.

### Fase 2 — Modelado, Evaluación y Optimización

El diseño experimental priorizó dos aspectos críticos en proyectos de salud: **evitar la fuga de datos** y **manejar correctamente el desbalance de clases**.

**Partición y prevención de data leakage:**
Se utilizó `GroupShuffleSplit` (70% entrenamiento / 30% prueba) bloqueando grupos de perfiles similares, garantizando que ningún registro del conjunto de prueba contaminara el entrenamiento.

**Tratamiento del desbalance — SMOTE dentro de Pipelines:**
La clase positiva (pacientes con diabetes) era minoritaria en el dataset. Se integró **SMOTE** dentro de **Pipelines de Imbalanced-learn**, asegurando que el sobremuestreo sintético se aplicara únicamente dentro de cada pliegue de entrenamiento durante la validación cruzada, no sobre el conjunto de prueba. Esto evita resultados artificialmente optimistas.

**Algoritmos evaluados:**

| Categoría | Modelo |
|-----------|--------|
| Lineal | Regresión Logística (RL) |
| Árbol simple | Decision Tree (DT) |
| Ensamble | Random Forest (RF) |
| Ensamble | Gradient Boosting (GB) |
| Ensamble | XGBoost (XGB) |

Cada modelo fue optimizado con **GridSearchCV** (k=5 pliegues), usando **F1-Score** como métrica de referencia. Adicionalmente, se realizó un **análisis de sensibilidad de umbrales** (de 0.10 a 0.70) para identificar el punto de operación clínica óptimo.

---

## Resultados

### Comparación de modelos (umbral estándar = 0.5)

| Modelo | Recall | F1-Score | ROC-AUC |
|--------|--------|----------|---------|
| **XGBoost** | 0.919 | ~0.530 | **0.676** |
| Gradient Boosting | 0.914 | ~0.529 | 0.671 |
| Random Forest | 0.930 | ~0.530 | — |
| Árbol de Decisión | 0.354 | — | 0.669 |
| Regresión Logística | 0.666 | 0.483 | — |

Los modelos de ensamble dominaron en recall y AUC-ROC, mientras que el Árbol de Decisión mostró mayor precisión pero una capacidad de detección muy limitada. **XGBoost fue identificado como el modelo con mayor capacidad discriminativa global.**

### Optimización del umbral de decisión

En tamizaje de enfermedades crónicas, el costo de un **falso negativo** (paciente enfermo no detectado) supera significativamente al de un falso positivo. Por eso, el análisis de umbrales fue clave.

Al ajustar el umbral de decisión del modelo XGBoost de 0.5 a **0.4**, se obtuvo:

> **Recall = 0.958** — el modelo identifica correctamente el 95.8% de los individuos en riesgo.

Este resultado posiciona al modelo como una herramienta de tamizaje altamente efectiva para apoyar decisiones clínicas proactivas.

### Variables más influyentes (XGBoost — métrica Gain)

| Variable | Importancia |
|----------|-------------|
| Persona mayor (ciclo de vida) | 18.47% |
| Cáncer | 9.69% |
| Adultez (ciclo de vida) | 8.02% |
| Asma | 8.02% |
| EPOC | 6.95% |
| Hipertensión | 6.13% |
| Artritis | 5.89% |

La edad avanzada y la presencia de comorbilidades crónicas concentran el mayor poder predictivo, lo que es coherente con la evidencia epidemiológica disponible para la región.

---

## Stack tecnológico

| Herramienta | Uso |
|-------------|-----|
| Python 3.12 | Lenguaje principal |
| Google Colab | Entorno de ejecución en la nube |
| `sodapy` | Extracción de datos vía API Socrata |
| `pandas` | Manipulación y transformación de datos |
| `scikit-learn` | Modelado, validación cruzada, GridSearchCV |
| `imbalanced-learn` | Pipelines con SMOTE |
| `xgboost` | Modelo de mejor desempeño |
| Google Drive | Almacenamiento del proyecto |

---

## Conclusiones clave

1. **XGBoost es la arquitectura más adecuada** para este tipo de problema, logrando el mayor AUC-ROC (0.676) y un recall de 0.919 con umbral estándar.
2. **El ajuste del umbral a 0.4 es la decisión clínica más importante del proyecto**: eleva el recall a 0.958, minimizando falsos negativos en tamizaje poblacional.
3. **SMOTE dentro de Pipelines es obligatorio** al trabajar con registros administrativos gubernamentales desbalanceados para evitar sesgos y resultados optimistas artificiales.
4. **La edad avanzada y las comorbilidades** (cáncer, asma, EPOC, hipertensión, artritis) son los predictores más determinantes del riesgo de diabetes en la población analizada.
5. **La viabilidad tecnológica está demostrada**: todo el pipeline fue ejecutado en Google Colab sin infraestructura local, lo que facilita la replicabilidad y democratiza el acceso a herramientas de IA en ciudades intermedias colombianas.

---

## Repositorio

🔗 [github.com/ingjuanmbl-jmbl/diabetes-bucaramanga-classification](https://github.com/ingjuanmbl-jmbl/diabetes-bucaramanga-classification)

---

*Investigación realizada en el marco de la Especialización en Analítica de Datos — Corporación Unificada Nacional de Colombia (CUN). Actualmente en proceso de revisión editorial.*
