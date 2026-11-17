# Eficiencia en la ejecución del gasto público en Argentina

**Machine Learning aplicado a datos presupuestarios** · Coderhouse – Data Science

## Problema
La diferencia entre lo que se **presupuesta** y lo que efectivamente se **ejecuta** (crédito devengado) muestra qué tan eficiente es el proceso presupuestario. El proyecto busca anticipar qué tipo de ejecución tendrá cada partida del presupuesto nacional:

- **Ejecución normal**: se presupuestó y se ejecutó.
- **Reasignación**: no se presupuestó, pero se ejecutó.
- **Sin ejecución**: se presupuestó, pero no se ejecutó.

## Datos
- **Presupuesto de gastos y su ejecución** (2002 en adelante), del portal [datos.gob.ar](https://datos.gob.ar/): más de 2,5 millones de registros con todos los clasificadores presupuestarios.
- **Tipo de cambio**, descargado de la API del BCRA.
- **Inflación (IPC)**, a partir de las series del BIS (Bank for International Settlements).

## Método
1. **Limpieza y transformación** de los archivos anuales: tipos de datos, nulos, partidas sin movimiento y outliers, con criterio presupuestario.
2. **Variables macroeconómicas**: variación del tipo de cambio, inflación, brecha entre ambas y regímenes cambiarios.
3. **Análisis estadístico**: correlaciones, ANOVA y chi-cuadrado.
4. **Modelos de clasificación multiclase**: Random Forest (optimizado con GridSearchCV), regresión logística y XGBoost, con tratamiento del desbalance de clases.

## Resultados
- El **95 % de las partidas** muestra algún tipo de desvío (reasignación o falta de ejecución). Solo el 5 % se ejecuta según lo planificado, pero ese 5 % concentra el **37 % del gasto devengado**.
- **2015 es un punto de inflexión**: se duplican las partidas sin ejecución.
- La jurisdicción **Obligaciones a Cargo del Tesoro** concentra el 60 % del gasto reasignado.
- El régimen cambiario **no explica por sí solo** la eficiencia de la ejecución (ANOVA, p = 0,44).
- Mejor modelo: **Random Forest balanceado** (F1-macro 0,47). Todos los modelos llegan a un techo similar, lo que indica que el límite está en la información disponible y no en el algoritmo.

| Modelo | F1-macro | Accuracy |
|--------|----------|----------|
| Regresión logística | 0,43 | ~0,50 |
| **Random Forest (optimizado)** | **0,47** | **0,57** |
| XGBoost | 0,45 | 0,72* |
| XGBoost balanceado | 0,47 | 0,57 |

\* Accuracy engañosa: el modelo predice casi siempre la clase mayoritaria.

## Herramientas
Python · pandas · NumPy · SciPy · scikit-learn · XGBoost · Matplotlib · Seaborn · Plotly · Altair · APIs (requests)

📓 [Ver el notebook completo](eficiencia_gasto_publico.ipynb) · 📊 [Presentación](presentacion_eficiencia_gasto_publico.pptx)
