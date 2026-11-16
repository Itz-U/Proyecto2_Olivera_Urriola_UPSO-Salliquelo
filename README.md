# Predicción de salarios de desarrolladores de software

**Proyecto 2 — Programación Python Avanzada**  
Tecnicatura Universitaria en Tecnologías de Programación — UPSO (2026)
Integrantes: Olivera Yohana - Urriola Itziar

## Descripción del proyecto

En este proyecto desarrollamos un modelo de **regresión lineal múltiple** para estimar el salario de desarrolladores de software en dólares estadounidenses a partir de características profesionales como la experiencia laboral, el país de residencia, la formación académica, los lenguajes de programación, los frameworks utilizados y el tamaño de la empresa.

El trabajo se realizó en **Python**, utilizando **Jupyter Notebook en Visual Studio Code**, e incluye exploración de datos, preparación de variables, entrenamiento, evaluación e interpretación de resultados.

## Dataset

**Fuente:** [Software Developer Salary Prediction — Kaggle](https://www.kaggle.com/datasets/nudratabbas/software-developer-salary-prediction-dataset)

Se unificaron los archivos originales `train.csv` (40.000 registros) y `test.csv` (10.000 registros), obteniendo un conjunto de **50.000 registros y 7 columnas**. Luego se realizó una nueva partición aleatoria para el proyecto.

| Variable original | Nombre utilizado | Descripción |
|---|---|---|
| `experience` | `experiencia` | Años de experiencia profesional |
| `country` | `pais` | País de residencia |
| `education` | `educacion` | Nivel educativo |
| `languages` | `lenguajes` | Lenguajes de programación utilizados |
| `frameworks` | `frameworks` | Frameworks utilizados |
| `company_size` | `tamano_empresa` | Tamaño de la empresa |
| `salary_usd` | `salario_usd` | Salario en USD, variable objetivo |

## Objetivo

Entrenar y evaluar un modelo de regresión lineal múltiple que permita **predecir el salario (`salario_usd`)** y analizar qué variables se relacionan más con las predicciones.

## Herramientas utilizadas

- Python y Jupyter Notebook en Visual Studio Code.
- **Pandas y NumPy:** manipulación de datos.
- **Matplotlib y Seaborn:** visualización.
- **Scikit-learn:** partición, codificación, entrenamiento y evaluación de modelos.

## Resultados

### Comparación entre entrenamiento y test

| Modelo | Conjunto | MAE (USD) | RMSE (USD) | R² |
|---|---|---:|---:|---:|
| DummyRegressor | Entrenamiento | 37.839,506 | 46.421,897 | 0,000 |
| DummyRegressor | Test | 37.819,286 | 46.568,375 | ≈ 0,000 |
| LinearRegression | Entrenamiento | **13.146,065** | **15.996,208** | **0,881** |
| LinearRegression | Test | **13.185,824** | **16.001,487** | **0,882** |

La regresión lineal múltiple logró un **R² de 0,882 en test**, explicando aproximadamente el **88,2 % de la variabilidad del salario** en ese conjunto. Su **error absoluto medio (MAE) fue de 13.185,82 USD**, notablemente inferior al del modelo de referencia (37.819,29 USD).

Las métricas de entrenamiento y test fueron muy parecidas, por lo que **no se observaron señales evidentes de sobreajuste**.

### Interpretación de las variables

El modelo obtuvo un coeficiente de **+3.015,98 USD para `experiencia`**, asociado con un aumento estimado de ese monto por año adicional de experiencia, manteniendo constantes las demás variables.

Entre los coeficientes de las categorías destacaron:

| Variable | Coeficiente (USD) |
|---|---:|
| `pais_USA` | +39.733,46 |
| `pais_India` | −35.043,09 |
| `educacion_PhD` | +19.455,13 |
| `tamano_empresa_5000+` | +15.597,96 |

Los coeficientes de las variables categóricas se interpretan **respecto a sus categorías de referencia**. No representan relaciones causales ni deben compararse directamente entre variables medidas en unidades distintas.

La importancia por permutación mostró que **`experiencia` fue la variable individual de mayor contribución predictiva** (disminución media de R² de **1,1738** al permutarla), seguida por `pais_USA` (**0,3502**) y `pais_India` (**0,1027**). Los lenguajes y frameworks tuvieron importancias individuales mucho menores.

### Limitaciones del modelo

El análisis de residuos mostró una **dispersión creciente de los errores para salarios predichos más elevados**, es decir, no tienen una varianza constante a lo largo de los distintos niveles de las variables explicativas. Aunque el ajuste global es bueno, la incertidumbre de las predicciones no es uniforme en todos los niveles salariales.

## Conclusiones finales

**1. ¿Cuál fue el desempeño del modelo?**  
`LinearRegression` superó claramente a `DummyRegressor`, con **R² = 0,882**, **MAE = 13.185,82 USD** y **RMSE = 16.001,49 USD** en test.

**2. ¿Qué variable fue la más influyente según los coeficientes?**  
`pais_USA` presentó el **coeficiente positivo de mayor magnitud** (+39.733,46 USD), mientras que `pais_India` presentó el mayor coeficiente negativo en valor absoluto (−35.043,09 USD). Sin embargo, al evaluar la contribución predictiva por permutación, **`experiencia` fue la variable individual más importante**.

**3. ¿Las variables fueron buenas predictoras? ¿Qué otras se sugieren?**  
En conjunto, las variables seleccionadas permitieron buenas predicciones dentro del dataset. La experiencia y determinadas categorías de país aportaron especialmente al desempeño; los lenguajes y frameworks mostraron una contribución individual pequeña. Como mejoras, sería interesante incorporar especialización (Frontend, Backend, Full Stack, Data Science), nivel de responsabilidad y modalidad de trabajo.

**4. ¿Cómo se comparan entrenamiento y test?**  
El desempeño fue muy similar: **R² de 0,881 en entrenamiento y 0,882 en test**, sin señales evidentes de sobreajuste. Sin embargo, el patrón de residuos sugiere mayor variabilidad en los errores de salarios elevados.

En conclusión, el proyecto permitió construir un modelo de regresión lineal múltiple con **buen desempeño predictivo en el dataset evaluado**, reconociendo tanto sus aportes como sus limitaciones.

## Archivos en el repositorio

1. Csv originales: `train.csv` y `test.csv`.
2. Csv con el diccionario de variables: `data_dictionary.csv`


