---
title: "Aplicación de modelos clasificatorios para detectar usuarios insatisfechos en una empresa de dispensación de medicamentos utilizando estadística multivariada y algoritmos supervisados"
excerpt: "Desarrollé un modelo de analítica predictiva basado en algoritmos de machine learning para identificar usuarios potencialmente insatisfechos en una empresa de dispensación de medicamentos. A partir de la integración, limpieza y análisis de datos operativos y de encuestas, entrené y evalué varios modelos de clasificación, seleccionando el de mejor desempeño para anticipar experiencias negativas y apoyar la toma de decisiones orientadas a mejorar el servicio."
collection: portfolio
date: 2025-08-29
header:
  teaser: "/assets/images/perfil.jpg"
---

## 🧠 Descripción del Proyecto
Este proyecto desarrolla un modelo de analítica predictiva orientado a identificar usuarios potencialmente insatisfechos en una empresa de dispensación de medicamentos.

El problema principal radica en la baja tasa de respuesta de encuestas (<1.5%) y el retraso en el procesamiento de información, lo que limita la capacidad de reacción operativa.

La solución propuesta utiliza modelos de clasificación supervisados para anticipar la insatisfacción sin depender directamente de la retroalimentación del usuario.
> Este proyecto se llevo a cabo en el marco de la tesis para obtener el titulo de especialista en analitica de datos

---

## 🎯 Objetivo
Desarrollar e implementar un modelo de clasificación que permita predecir usuarios insatisfechos, facilitando la toma de decisiones proactiva en experiencia del cliente.

---

## ⚙️ Tecnologías y Herramientas
- Python (Pandas, NumPy, Scikit-learn)
- KNIME
- SAP Business Objects
- Jupyter Notebook
- Machine Learning (Supervised Learning)

---

## 🧩 Metodología

### 1. Centralización de Datos
- Integración de múltiples fuentes:
  - Encuestas de satisfacción
  - Datos de dispensación
  - Variables operativas
- Consolidación en SAP Business Objects

### 2. Preprocesamiento
- Limpieza de datos
- Imputación de valores faltantes
- Codificación de variables categóricas (One-Hot Encoding)
- Normalización de variables

### 3. Modelado
Se entrenaron y compararon los siguientes algoritmos:

- Regresión Logística
- Árbol de Decisión
- Random Forest
- Naive Bayes
- XGBoost

### 4. Evaluación
Métricas utilizadas:
- Recall (prioridad principal)
- F1-Score
- Accuracy
- AUC-ROC
- Matriz de confusión

---

## 📈 Resultados

- 🔹 Mejor modelo: **XGBoost optimizado**
- 🔹 Recall (usuarios insatisfechos): **0.81**
- 🔹 F1-Score: **0.73**

El modelo logró identificar de forma efectiva usuarios con alta probabilidad de insatisfacción, priorizando la detección de casos críticos.

---

## 💡 Impacto del Proyecto

- Anticipación de experiencias negativas sin depender de encuestas
- Priorización de acciones de mejora en servicio
- Reducción del riesgo reputacional
- Soporte a decisiones basadas en datos
- Escalabilidad a otras EPS o líneas de servicio

---

## ⚠️ Limitaciones

- Dependencia de la calidad de datos históricos
- No incluye variables externas (ej. cambios regulatorios)
- Horizonte de predicción limitado a corto plazo (1 mes)
- Modelo no implementado aún en producción

---

## 🚀 Próximos Pasos

- Implementación en tiempo real (modelo productivo)
- Ampliación del horizonte predictivo
- Inclusión de variables externas (supply chain, políticas públicas)
- Dashboard de visualización para toma de decisiones

---

## 📌 Conclusión

Este proyecto demuestra cómo la analítica avanzada puede transformar la gestión de la experiencia del cliente en el sector salud, pasando de un enfoque reactivo a uno predictivo.

El uso de modelos de machine learning permite identificar patrones no evidentes y generar valor estratégico a partir de los datos operativos.

---

## 👤 Autor
**Juan Manuel Betancur López**  
Especialización en Analítica de Datos  
Pereira, Colombia