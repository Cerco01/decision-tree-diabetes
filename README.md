# Prediciendo la diabetes con árbol de decisión

Este proyecto trabaja con un dataset médico cuyo objetivo es predecir si un paciente tiene o no diabetes a partir de distintas medidas diagnósticas. El flujo completo se desarrolla en un notebook: carga de datos, EDA, preprocesamiento, entrenamiento de un árbol de decisión, optimización con `GridSearchCV` y guardado del modelo final.

## Objetivos del proyecto

- Comprender un dataset nuevo.
- Procesarlo aplicando análisis exploratorio de datos (EDA).
- Construir un modelo de árbol de decisión.
- Analizar los resultados del modelo.
- Optimizar el modelo mediante búsqueda de hiperparámetros.
- Guardar el modelo final entrenado.

## Dataset

El conjunto de datos proviene originalmente del Instituto Nacional de Diabetes y Enfermedades Digestivas y Renales. La variable objetivo es `Outcome`, donde:

- `0`: negativo en diabetes.
- `1`: positivo en diabetes.

### Variables

| Variable | Descripción | Tipo |
|----------|-------------|------|
| `Pregnancies` | Número de embarazos del paciente | Numérico |
| `Glucose` | Concentración de glucosa en plasma a las 2 horas de un test de tolerancia oral a la glucosa | Numérico |
| `BloodPressure` | Presión arterial diastólica, medida en mm Hg | Numérico |
| `SkinThickness` | Grosor del pliegue cutáneo del tríceps, medido en mm | Numérico |
| `Insulin` | Insulina sérica de 2 horas, medida en mu U/ml | Numérico |
| `BMI` | Índice de masa corporal | Numérico |
| `DiabetesPedigreeFunction` | Función de pedigrí de diabetes | Numérico |
| `Age` | Edad del paciente | Numérico |
| `Outcome` | Variable de clase: 0 negativo, 1 positivo | Numérico |

El dataset utilizado está en:

```text
data/raw/diabetes.csv
```

## Estructura del proyecto

```text
.
├── data/
│   └── raw/
│       └── diabetes.csv
├── models/
│   └── decision_tree_diabetes.pkl
├── src/
│   ├── apple.mplstyle
│   └── explore.ipynb
├── requirements.txt
└── README.md
```

## Flujo de trabajo realizado

### 1. Carga y exploración del dataset

Se carga el dataset desde `data/raw/diabetes.csv` y se revisan:

- valores nulos,
- duplicados,
- estructura del dataframe,
- distribución de la variable objetivo,
- correlaciones,
- posibles outliers,
- valores 0 sospechosos en variables médicas.

### 2. Preprocesamiento

Durante el EDA aparecen valores 0 en columnas donde médicamente no tienen sentido, como `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin` y `BMI`.

Las decisiones principales son:

- eliminar filas con demasiadas mediciones faltantes,
- descartar `Insulin` por tener una proporción muy alta de valores en 0,
- dividir el dataset en train y test antes de imputar,
- imputar los ceros restantes usando medianas calculadas solo con `X_train`, para evitar data leakage.

También se comparan dos versiones del dataset:

- una conservando `SkinThickness`,
- otra eliminando `SkinThickness`.

La versión con `SkinThickness` obtiene mejores resultados, así que se utiliza para el modelado final.

### 3. Modelo de árbol de decisión

Se entrena un modelo base con `DecisionTreeClassifier` y después se comparan los criterios de pureza disponibles:

- `gini`,
- `entropy`,
- `log_loss`.

En este caso, `gini` obtiene los mejores resultados.

### 4. Optimización del modelo

Después de seleccionar `gini`, se optimizan los hiperparámetros con `GridSearchCV`.

Se prueban dos enfoques:

- optimización priorizando `f1`,
- optimización priorizando `recall`.

Ambos GridSearch llegan al mismo árbol final:

```python
{
    "criterion": "gini",
    "max_depth": 4,
    "min_samples_leaf": 10,
    "min_samples_split": 2
}
```

### 5. Evaluación final

El modelo optimizado mejora el recall de la clase positiva frente al modelo base, aunque baja en accuracy, precision y F1-score.

Como el problema está relacionado con salud, se prioriza reducir falsos negativos. Es decir, se prefiere detectar más posibles casos de diabetes aunque eso pueda aumentar los falsos positivos.

El modelo se interpreta como una herramienta de cribado inicial, no como un diagnóstico médico definitivo.

### 6. Guardado del modelo

El modelo final se guarda en:

```text
models/decision_tree_diabetes.pkl
```

Nota: el archivo `.pkl` guarda el modelo entrenado, pero el preprocesamiento se realiza en el notebook. Para usar el modelo fuera del notebook habría que aplicar el mismo tratamiento de datos.

## Cómo ejecutar el proyecto

1. Clonar el repositorio.

2. Instalar las dependencias:

```bash
pip install -r requirements.txt
```

3. Abrir el notebook principal:

```text
src/explore.ipynb
```

4. Ejecutar las celdas en orden.

## Archivos principales

| Archivo | Descripción |
|---------|-------------|
| `src/explore.ipynb` | Notebook principal con EDA, preprocesamiento, modelado y conclusiones |
| `src/apple.mplstyle` | Estilo visual personalizado para los gráficos |
| `data/raw/diabetes.csv` | Dataset original |
| `models/decision_tree_diabetes.pkl` | Modelo final entrenado |
| `requirements.txt` | Dependencias del proyecto |

## Referencias consultadas

- Documentación de scikit-learn sobre árboles de decisión.
- Documentación de scikit-learn sobre errores comunes y data leakage.
- Artículo *Decision tree methods: applications for classification and prediction* de Song y Lu (2015).
- Recurso de NCBI Bookshelf sobre sensibilidad y especificidad.

## Créditos

Proyecto realizado como parte del Bootcamp de Data Science y Machine Learning de 4Geeks Academy.
