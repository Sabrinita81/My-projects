# Abandono de clientes de tarjetas de crédito (churn)

**Primer proyecto de Machine Learning** · Coderhouse – Data Science · 2024

## Problema
Un banco quiere anticipar qué clientes van a dar de baja su tarjeta de crédito, para poder actuar antes de perderlos.

## Datos
[Prediction of Churning Credit Card Customers](https://www.kaggle.com/datasets/thedevastator/predicting-credit-card-customer-attrition-with-m) (Kaggle): 10.127 clientes y 23 variables (demográficas, tipo de tarjeta, consumo y saldos). Sin valores nulos.

## Método
1. **Análisis exploratorio**: perfil de los clientes que abandonan según género, estado civil, edad, tipo de tarjeta e ingresos.
2. **Tests estadísticos (t-test)** para comparar saldos y antigüedad entre clientes vigentes y no vigentes.
3. **Reducción de dimensionalidad**: PCA, forward selection y análisis de correlación.
4. **Modelos de clasificación**: regresión logística (con y sin outliers) y Naive Bayes.

## Resultados
- Las variables con mayor poder predictivo son las de **comportamiento de uso**: cantidad de transacciones, variación del uso entre trimestres y saldo refinanciado. Las variables demográficas casi no explican el abandono.
- Los clientes que se dieron de baja **usaban la tarjeta por debajo de su límite** y tenían saldos refinanciados menores.
- Mejor modelo: **Naive Bayes**, con **93 % de accuracy** y mejor detección de los clientes que abandonan que la regresión logística (recall de la clase "abandona": 84 % vs. 79 %).

| Modelo | Accuracy |
|--------|----------|
| Regresión logística | 88,5 % |
| Regresión logística sin outliers | 93,4 % |
| **Naive Bayes sin outliers** | **93 %** |

## Herramientas
Python · pandas · NumPy · SciPy · scikit-learn · Matplotlib · Seaborn

📓 [Ver el notebook completo](churn_tarjetas_credito.ipynb)
