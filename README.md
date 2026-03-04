# 📊 Análisis de Churn en Telecom X - parte 2

## 📌 Descripción del proyecto
Este proyecto tiene como objetivo analizar los datos de churn (cancelación de clientes) de Telecom X. Se implementan diversos modelos de Machine Learning como **Regresión Logística** y **Árbol Aleatorio**, para entender qué factores influyen en la cancelación de clientes.  

## 📋 **Contenido**
1. Descripción del Proyecto
2. Tecnologías Utilizadas
3. Desarrollo del Proyecto
4. Conclusiones y Recomendaciones
5. Autor

## 💻 **Tecnologías Utilizadas**
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge)
![Numpy](https://img.shields.io/badge/Numpy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Chi-Square](https://img.shields.io/badge/Chi--Square-FF9900?style=for-the-badge&logo=python&logoColor=white)
![Logistic Regression](https://img.shields.io/badge/Logistic%20Regression-34B7F1?style=for-the-badge&logo=python&logoColor=white)
![Random Forest](https://img.shields.io/badge/Random%20Forest-34B7F1?style=for-the-badge&logo=python&logoColor=white)
![One Hot Encoding](https://img.shields.io/badge/One%20Hot%20Encoding-4C72B0?style=for-the-badge&logo=python&logoColor=white)

## 🚀 **Desarrollo del Proyecto**
Se desarrolló siguiendo la siguiente estructura: 

1. Extracción de Datos

Se cargaron los datos y se hizo una revisión de los mismos (info y columnas)
      
2. Preprocesamiento

En esta etapa, se realizó el preprocesamiento de los datos para preparar los datos para el análisis y el entrenamiento de modelos. Se utilizó One-Hot Encoding para convertir las variables categóricas en variables numéricas, StandardScaler para normalizar las variables numéricas, se revisaron valores nulos y eliminamos columnas irrelevantes.
   
3. EDA
   
El análisis exploratorio de datos (EDA) fue crucial para entender la distribución de las variables y entender la relación entre las mismas, cuales influyen en la tasa de cancelación de churn.

Realizamos primeramente la Matriz de Correlación con las variables numéricas: 
   <p align="center">
     <img src="graficas_telecom2/Matriz de Correlación con Variables Numéricas.png" width="70%" />
   </p>  
Observando que Tenure presenta correlación negativa con la cancelación y ChargesMonthly muestra correlación positiva, sugiriendo que cargos más altos pueden asociarse con mayor cancelación.

En la Correlación con variables categóricas notamos variables con menos impacto como Gender y PhoneService
y variables con medio y de alto impacto como SeniorCitizen, lo que lleva a que los adultos mayores tienen casi el doble de probabilidad de cancelar. 

Seguimos con un análisis dirigido con:

Tiempo de contrato × Cancelación
 <p align="center">
     <img src="graficas_telecom2/Tiempo de contrato vs Cancelación.png" width="40%" />
</p> 
En este gráfico se muestra la relación entre el tipo de contrato y la tasa de churn. Los clientes con contrato mensual presentan una tasa de churn significativamente más alta en comparación con los clientes que tienen contratos de un año o dos años. Esto indica que los contratos a largo plazo podrían ser una estrategia efectiva para reducir la cancelación.

Gasto total × Cancelación

<p align="center">
     <img src="graficas_telecom2/Gasto total vs Cancelación.png" width="40%" />
</p> 

Se refleja que clientes con menor gasto acumulado muestran mayor tendencia a cancelar.

4. Split

El conjunto de datos se dividió en dos partes: una para el entrenamiento de los modelos y otra para la evaluación. Utilizamos train_test_split de Scikit-learn para dividir los datos.

5. Entrenamiento (Modelos)
   
Se entrenaron 2 modelos de Machine Learning para predecir el churn. Los modelos utilizados fueron:

-   Regresión Logística: Nos permitió interpretar facilmente el impacto variable.
  
-   Árbol Aleatorio: Nos ofreció otro enfoque como modelo predictivo.

-   Tomando en cuenta los datos obtenidos, realizamos un balanceamiento para mejorar el recall en la clase "Yes" (clientes que cancelan), aplicamos el parámetro class_weight='balanced' en la Regresión Logística. Esto ajusta el modelo para que dé más peso a la clase minoritaria (churn).

6. Evaluación
   
En la Regresión Logística sin balanceo de datos, el modelo muestra buen desempeño al identificar clientes que no cancelan el servicio. Sin embargo, presenta dificultad para detectar correctamente los casos reales de churn, debido al desbalance de clases.

<p align="center">
     <img src="graficas_telecom2/Matriz de Confusión - Regresión Logística No Balanceada.png" width="35%" />
</p> 

Al aplicar balanceo de datos, la Regresión Logística mejora su capacidad para identificar clientes que sí cancelan el servicio. Se observa un incremento en el recall de la clase churn, reduciendo los falsos negativos.

<p align="center">
     <img src="graficas_telecom2/Matriz de Confusión - Regresión Logística Balanceada.png" width="35%" />
</p> 

El gráfico de coeficientes de la Regresión Logística muestra el impacto de cada variable en la probabilidad de churn. Las variables con coeficientes positivos incrementan la probabilidad de cancelación, mientras que las negativas la reducen

<p align="center">
     <img src="graficas_telecom2/Impacto de Variables en Churn - Regresión Logística.png" width="50%" />
</p> 

El análisis de importancia de variables del Random Forest identifica los factores con mayor influencia en la predicción del churn. A diferencia de la Regresión Logística, este modelo captura relaciones no lineales y patrones más complejos.

<p align="center">
     <img src="graficas_telecom2/Variables más relevantes - Random Forest.png" width="50%" />
</p>


## 📋 **Conclusiones y Recomendaciones**

- El Churn no depende de una sola variable, sino de la combinacion de algunos factores como el tipo de contrato, la edad de las personas, las condiciones del servicio.
- El desbalance si influye en la capacidad del modelo para detectar las cancelaciones del servicio.
- Elegir adecuadamente las variables ayuda a mejorar la calidad del modelo y reducir el ruido en el entrenamiento obteniendo mejores resultados.


- Se recomienda ofrecer algun servicio de fidelización a los clientes nuevos
- Enfocarse en clientes con una edad media
- Optimizar las opciones de pago
- Realizar una estrategia basada en valor del cliente


## 👩‍💻 Autor
**Proyecto realizado por: Ing. Fernanda Torres** 
<p>
GitHub: https://github.com/Maffert
</p>
