Predicción de Tabaquismo mediante Machine Learning

Descripción

Este proyecto tiene como objetivo desarrollar modelos de Machine Learning capaces de predecir si una persona es fumadora (smoking) a partir de variables demográficas, antropométricas y clínicas.

Para ello se realizaron tareas de análisis exploratorio, preprocesamiento de datos, entrenamiento de modelos predictivos, optimización de hiperparámetros y análisis de interpretabilidad.


Dataset

El conjunto de datos utilizado se encuentra en el archivo:

smoking_prediction.xlsx

ubicado en la carpeta \data\raw


La variable objetivo del conjunto de datos es:

smoking

0: No fumador
1: Fumador


Principales variables:

gender 
age 
height(cm) 
weight(kg)
waist(cm)
eyesight(left)
eyesight(right)
hearing(left)
hearing(right)
systolic
relaxation
fasting blood sugar
Cholesterol
triglyceride
HDL
LDL
hemoglobin
Urine protein
serum creatinine
AST
ALT
Gtp
oral
dental caries
tartar

Objetivos:

Analizar el comportamiento de la población estudiada.
Identificar las variables más relevantes asociadas al tabaquismo.
Construir modelos predictivos de clasificación.
Optimizar los hiperparámetros de los modelos.
Explicar las predicciones mediante técnicas de interpretabilidad.


Herramientas Utilizadas:

Python (version 3.14.6)
Pandas (version 3.0.3)
NumPy (version 2.4.6)
Matplotlib (version 3.11.0)
Seaborn (version 0.13.2)
Scikit-Learn (version 1.9.0)
XGBoost (version 3.4.1)
Optuna (version 5.0.0)
SHAP 0.54.1 slicer-0.0.8


Lectura y descubrimiento de datos:

Luego de la verificacion de datos contenidos en el conjunto de datos, se observan muchas variabes con distribuciones muy asimétricas:

Gtp
LDL
HDL
triglyceride


Análisis exploratorio de Datos (EDA):

En esta etapa, mediante la interpretación de distintos tipos de gráficos, obtuve algunos datos de interes.
1 - El 36,7% de los integrantes en este conjunto de datos, son fumadores.
2 - Solo el 4,27% de las mujeres del conjunto de datos, fuman.
3 - Mientras que el porcentaje de hombres fumadores es del 55,2% (mas de la mitad de los hombres de la muestra son fumadores)
4 - A partir de los 76 kg de peso, se equilibra cantidad de fumadores y no fumadores. Suena lógico en base al punto anterior.
5 - De las personas con valores de la encima Gtp, superiores a 1,71 , la mayoría son fumadores.
6 - De los individuos con valores de triglicéridos superiores a 7,8 , hay mas cantidad de fumadores que no fumadores.


Preprocesamiento:

Las etapas de preparación de datos incluyeron:

Eliminación de variables fijas.
Codificación de variables categóricas mediante One-Hot Encoding (OHE).
División en conjuntos de entrenamiento y prueba.
Validación de consistencia de los datos.


Modelos Implementados

Arbol de decisión 
(abraviado durante el código como dtc)


Random Forest 
(abraviado durante el código como rf)

Parámetros utilizados para el modelo:

n_estimators = 137
max_depth=31
min_samples_split = 5
min_samples_leaf =300


XGBoost
(abraviado durante el código como xgb)

Parámetros utilizados para el modelo:

n_estimators = 300
max_depth = 3
learning_rate = 0.02

Se realizó búsqueda de hiperparámetros mediante Optuna, sin obtener mejoras respecto a los parametros probados manualmente.
Estas pruebas de mejoras de hiperparametros, pueden verse en la notebook Nro. 7 (Pruebas Optuna XGB)



Evaluación:

Los modelos fueron evaluados utilizando métricas de clasificación:

Accuracy
Precision
Recall
F1-Score


Interpretabilidad:

Para comprender el comportamiento de los modelos se utilizaron:

Importancia Relativa de Atributos

Permite identificar cuáles son las variables que más influyen en la predicción.


SHAP (SHapley Additive exPlanations)

Permite conocer:

Impacto global de cada variable.
Impacto local sobre cada predicción.
Relaciones entre variables y probabilidad de tabaquismo.


Estructura del Proyecto:

proyecto/

│
│
├── data/
│
│   ├── raw/
│         ├── smoking_prediction.xlsx
│         └── smoking_prediction_entrega.xlsx
│
│   ├── processed/
│          ├── X_test_final.xlsx
│          ├── X_train_final.xlsx 
│          ├── y_test.xlsx   
│          └── y_train.xlsx    
│        
│   ├── predictions/
│          └── smoking_prediction_entrega_rf.xlsx    
│
│
├── notebooks/
│      ├── 01_lectura_y_discovery.ipynb
│      ├── 02_eda.ipynb
│      ├── 03_preprocesamiento.ipynb
│      ├── 04_entrenamiento_y_optimizacion.ipynb
│      ├── 05_validacion.ipynb
│      ├── 06_prediccion.ipynb
│      └── 07_pruebas_optuna_xgb.ipynb

│

├── objects/
│      ├── models/
│             ├── modelo_arbol_decision.pkl
│             ├── modelo_random_forest.pkl
│             └── modelo_XGBoost.pkl
│
│      └── encoders/
│             └── ohe.joblib
│
├── requirements.txt
└── README.md
