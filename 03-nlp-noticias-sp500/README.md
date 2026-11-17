# ¿Los titulares de noticias anticipan al mercado? NLP y S&P 500

**Procesamiento de lenguaje natural y deep learning** · Coderhouse – Data Science

## Problema
¿Se puede predecir si el índice **S&P 500** sube o baja en un día a partir de los titulares de noticias financieras de ese día?

## Datos
Dataset de Kaggle con **19.127 titulares** de noticias financieras y el precio de cierre diario del S&P 500 (unos 5 titulares por día). Clases balanceadas: 54 % de días de suba y 46 % de baja.

## Método
1. **Procesamiento del texto**: limpieza, tokenización y lematización con **spaCy**, comparada con NLTK.
2. **Exploración**: nubes de palabras, palabras que diferencian los días de suba y de baja, y bigramas.
3. **Análisis de sentimiento** con VADER.
4. **Modelos**:
   - TF-IDF + regresión logística
   - Red neuronal (MLP), con early stopping, dropout, batch normalization y pesos por clase
   - **FinBERT** (modelo de lenguaje preentrenado en finanzas) con fine-tuning

## Resultados
- El vocabulario sí se asocia al mercado: **"record", "rally", "gain"** aparecen más en días de suba, y **"fall", "drop", "bear"** en días de baja.
- Pero esa señal es débil para predecir: el mejor modelo, **FinBERT**, acierta el **59 %** de las veces y es el más equilibrado entre subas y bajas.
- Un modelo simple (regresión logística, 58 %) rinde casi igual que los modelos complejos. Con textos cortos, más complejidad no siempre suma.

| Modelo | Accuracy |
|--------|----------|
| Regresión logística (TF-IDF) | 0,58 |
| Red neuronal MLP | 0,55 |
| Red neuronal ajustada | 0,56 |
| **FinBERT** | **0,59** |

## Conclusión
Los resultados son coherentes con la teoría de mercados eficientes: buena parte de la información de los titulares ya está incorporada en los precios. El valor del proyecto está en el pipeline de NLP completo y en la comparación de enfoques, de los modelos clásicos a los transformers.

## Herramientas
Python · pandas · spaCy · NLTK · VADER · scikit-learn · TensorFlow/Keras · PyTorch · Hugging Face Transformers · WordCloud

📓 [Ver el notebook completo](nlp_noticias_sp500.ipynb)
