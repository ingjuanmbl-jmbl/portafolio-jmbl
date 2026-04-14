---
title: "Health Analytics Platform - Hospital Homeris"
excerpt: "Construí un Análisis Avanzado de Agrupamiento y Reducción de Dimensionalidad para la Caracterización del Paciente en Salud Mental del hospital Homeris"
collection: portfolio
date: 2025-03-01
header:
  teaser: "/assets/images/perfil.jpg"
---


## 📊 Origen de los Datos y Contexto del Problema

Este proyecto aborda un **problema real de salud pública** utilizando datos oficiales del departamento de Risaralda, Colombia. 

Los datos provienen del **Registro de Casos de Atención del Hospital Mental Universitario de Risaralda (HOMERIS)**, disponibles en el portal de Datos Abiertos de Colombia:
* **Fuente:** [Datos.gov.co - Casos de Atención HOMERIS](https://www.datos.gov.co/Salud-y-Protecci-n-Social/REGISTRO-DE-CASOS-DE-ATENCION-HOMERIS-RISARALDA/izfv-6qvv/about_data)

### El Desafío Real
La gestión de servicios en salud mental requiere una comprensión profunda de la demanda. Este proyecto utiliza técnicas de **Machine Learning No Supervisado** para segmentar a la población atendida, permitiendo identificar perfiles críticos de pacientes. El objetivo es transformar datos administrativos en información accionable que permita optimizar recursos hospitalarios y diseñar programas de intervención focalizados según el género, la edad y el diagnóstico.


## 🌐 Acceso a la Plataforma en Vivo
Puedes interactuar con los modelos y explorar los clústeres en tiempo real aquí:
🚀 **[Hospital Homeris Analytics - Demo en la Nube](https://hospital-homeris-analysis-5e3mu8p9ypcsprptu4abtx.streamlit.app/)**




## 🎯 Objetivo del Proyecto

Modelar la estructura de la demanda asistencial mediante **técnicas de agrupación avanzada** para caracterizar fenotipos de pacientes,
permitiendo la extracción de evidencia estadística que fundamente la toma de decisiones clínicas y la optimización estratégica
de los servicios hospitalarios



## 🔬 Arquitectura y Metodología

El proyecto sigue un enfoque modular basado en **Principios de Ingeniería de Software** aplicado a la Ciencia de Datos:

1.  **Ingeniería de Características & PCA:** Implementación de pipelines de preprocesamiento robustos, incluyendo codificación de variables categóricas clínicas y **Reducción de Dimensionalidad (PCA)** para mitigar el ruido y la redundancia de los datos.
2.  **Clustering Avanzado:** Aplicación de algoritmos de agrupación (K-Means / Hierarchical) validados mediante métricas de cohesión y separación (**Coeficiente de Silueta**)
3.  **Visualización Científica:** Dashboard interactivo desarrollado en Streamlit con visualizaciones dinámicas (Plotly) para la interpretación de componentes principales y perfiles de segmento.


## 🚀 Funcionalidades

### 📈 Análisis Descriptivo
- Exploración de datos iniciales principalmente basado en:
  - Género
  - Edad
  - Régimen
  - Diagnóstico

### 🔍 Clustering (Machine Learning)
- Segmentación de pacientes mediante algoritmos no supervisados y reducción de la dimensionalidad (PCA)
- Identificación de grupos homogéneos

### 👥 Caracterización de Pacientes
- Análisis detallado de cada cluster:
  - Perfil demográfico
  - Diagnóstico predominante
  - Diferencias entre grupos


  
## 🧠 Principales Hallazgos y Caracterización

A través de la reducción de dimensionalidad (**PCA**) conservando el 70% de la varianza y algoritmos de clustering, se identificaron dos perfiles de pacientes con comportamientos epidemiológicos claramente diferenciados:

### 1. Segmento de Riesgo Joven Masculino (30% de la población)
* **Perfil:** Exclusivamente hombres en rango de edad joven.
* **Hallazgo:** Presentan la mayor concentración de diagnósticos críticos de salud mental. Este grupo muestra un comportamiento "especializado", sugiriendo que acceden al sistema principalmente ante crisis o patologías agudas, con menor incidencia en consultas preventivas.
* **Impacto:** Identifica una oportunidad crítica para diseñar programas de captación temprana y prevención enfocados específicamente en la población masculina joven.

### 2. Segmento de Gestión Integral Adulta (70% de la población)
* **Perfil:** Composición diversa con fuerte predominio femenino (70%) y población adulta.
* **Hallazgo:** Es el segmento de mayor volumen y variedad diagnóstica. La presencia mayoritaria de mujeres sugiere que este grupo constituye el núcleo de la demanda recurrente, abarcando un espectro clínico más amplio que va desde el control administrativo hasta el seguimiento crónico.
* **Impacto:** Representa la base operativa principal del hospital, donde la eficiencia en la asignación de citas y la continuidad del tratamiento son los mayores pilares de gestión.


### 🧪 Nota Técnica sobre el Modelo
Para lograr esta segmentación, se aplicó un **Análisis de Componentes Principales (PCA)**. Se determinó que el **género y la etapa del ciclo vital** son los predictores más robustos de la ruta de atención en HOMERIS. La elección de un modelo de 2 clústeres responde al aseguramiento para que los grupos sean interpretables y accionables para el negocio.

## 🛠️ Tecnologías utilizadas

- Python
- Streamlit
- Pandas
- Scikit-learn
- Plotly

### 🔗 Enlaces del Proyecto
* **Repositorio en GitHub:** [Health Analytics Platform - Hospital Homeris](https://github.com/ingjuanmbl-jmbl/hospital-homeris-analysis)