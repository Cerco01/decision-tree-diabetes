# Proyecto de Árbol de Decisión

## Contexto

Este conjunto de datos proviene originalmente del Instituto Nacional de Diabetes y Enfermedades Digestivas y Renales. El objetivo es predecir en base a medidas diagnósticas si un paciente tiene o no diabetes.

## Variables del dataset

| Variable | Descripción | Tipo |
|----------|-------------|------|
| `Pregnancies` | Número de embarazos del paciente | Numérico |
| `Glucose` | Concentración de glucosa en plasma a las 2 horas de un test de tolerancia oral a la glucosa | Numérico |
| `BloodPressure` | Presión arterial diastólica (medida en mm Hg) | Numérico |
| `SkinThickness` | Grosor del pliegue cutáneo del tríceps (medida en mm) | Numérico |
| `Insulin` | Insulina sérica de 2 horas (medida en mu U/ml) | Numérico |
| `BMI` | Índice de masa corporal | Numérico |
| `DiabetesPedigreeFunction` | Función de pedigrí de diabetes | Numérico |
| `Age` | Edad del paciente | Numérico |
| `Outcome` | Variable de clase (0 = negativo en diabetes, 1 = positivo) | Numérico |

## Cómo usar este proyecto

1. Clonar el repositorio.
2. Instalar las dependencias: `pip install -r requirements.txt`
3. El dataset `diabetes.csv` ya está incluido en `data/raw/`.
4. Abrir y ejecutar el notebook `src/explore.ipynb`.
5. Al ejecutar el notebook se generan los datasets procesados en `data/processed/`.

## Qué incluye el proyecto

- Carga y exploración del dataset `diabetes.csv`.
- Análisis Exploratorio de Datos (EDA): distribuciones, correlaciones, outliers.
- Preprocesamiento: feature engineering, split train-test, encoding, escalado.
- Modelo base de árbol de decisión con diferentes criterios de pureza (gini, entropy, log_loss).
- Optimización de hiperparámetros con `GridSearchCV`.
- Comparación de modelos y visualización de resultados.
- Guardado del modelo final en `models/`.
- Guardado de datasets procesados en `data/processed/`.

## Archivos principales

- `src/explore.ipynb`: notebook principal con EDA, modelado y conclusiones.
- `src/apple.mplstyle`: estilo personalizado para las visualizaciones.
- `data/raw/`: carpeta para el dataset original (`diabetes.csv`).
- `data/processed/`: carpeta para los datasets procesados.
- `models/`: carpeta para guardar el modelo entrenado.
- Los datos no se suben a Git.

## Créditos

Este proyecto fue realizado como parte del [Bootcamp de Data Science y Machine Learning](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning) de 4Geeks Academy.
