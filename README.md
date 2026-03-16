# Detección de Spam en SMS con Naive Bayes

Este proyecto implementa un sistema de detección de spam en mensajes SMS utilizando técnicas clásicas de **Procesamiento del Lenguaje Natural (NLP)** y un modelo **Multinomial Naive Bayes**.

El objetivo es construir un modelo sencillo pero eficaz capaz de distinguir entre mensajes legítimos (*ham*) y mensajes de spam utilizando patrones estadísticos presentes en el texto.

---

# Dataset

El dataset utilizado contiene mensajes SMS etiquetados en dos clases:

- **Ham** → mensaje legítimo
- **Spam** → mensaje no solicitado o publicitario

Este dataset es uno de los conjuntos de datos clásicos utilizados para problemas de clasificación de texto.

---

# Metodología

El flujo de trabajo seguido en el proyecto es el siguiente:

## 1. Preprocesado del texto

Los mensajes se normalizan mediante varias técnicas básicas de limpieza:

- Conversión a minúsculas
- Eliminación de signos de puntuación
- Eliminación de enlaces
- Eliminación de palabras con números
- Eliminación de **stopwords**

Este paso permite reducir ruido en el texto y simplificar el vocabulario utilizado por el modelo.

---

## 2. Vectorización del texto

El texto se convierte en variables numéricas mediante **Bag-of-Words** utilizando `CountVectorizer`.

Se incluyen además **n-gramas (1,2)** para capturar no solo palabras individuales sino también combinaciones frecuentes de palabras, lo que permite detectar expresiones características del spam como:

- "free prize"
- "call now"
- "claim reward"

También se aplican filtros sobre el vocabulario:

- `min_df` → elimina palabras demasiado raras
- `max_df` → elimina palabras demasiado frecuentes
- `max_features` → limita el tamaño del vocabulario

---

## 3. Modelo de clasificación

Se entrena un modelo **Multinomial Naive Bayes**, un algoritmo probabilístico ampliamente utilizado en clasificación de texto debido a su simplicidad y buen rendimiento en problemas de NLP.

El modelo estima la probabilidad de que un mensaje pertenezca a cada clase basándose en la frecuencia de las palabras.

---

# Evaluación del modelo

El modelo se evaluó utilizando una **matriz de confusión** y la **curva Precision-Recall**.

### Matriz de confusión

| | Pred Ham | Pred Spam |
|---|---|---|
Ham real | 1179 | 23 |
Spam real | 57 | 134 |

A partir de estos resultados se obtienen las siguientes métricas aproximadas:

- **Precision:** ~0.85  
- **Recall:** ~0.70  
- **Average Precision:** ~0.81  

### Interpretación

- El modelo mantiene una **precisión alta**, lo que significa que cuando detecta spam normalmente acierta.
- El número de **falsos positivos es bajo**, lo cual es importante para evitar bloquear mensajes legítimos.
- El modelo detecta aproximadamente **el 70% del spam**, por lo que aún existe margen de mejora en la capacidad de detección.

La **Average Precision ≈ 0.81** indica una buena capacidad de separación entre mensajes spam y ham.

---

# Conclusiones

El modelo **Naive Bayes combinado con Bag-of-Words y n-gramas** proporciona un baseline sólido para la clasificación de mensajes SMS.

A pesar de su simplicidad, el modelo es capaz de capturar patrones relevantes en el lenguaje del spam y obtener resultados competitivos.

---

# Posibles mejoras futuras

Este proyecto se ampliará en el futuro incorporando:

- Representaciones **TF-IDF**
- Comparación con otros modelos:
  - Logistic Regression
  - Linear SVM
  - XGBoost
- Ajuste de hiperparámetros mediante **GridSearch**
- Análisis de palabras más importantes para detectar spam

---

# Tecnologías utilizadas

- Python
- Pandas
- Scikit-learn
- Matplotlib
- Seaborn
