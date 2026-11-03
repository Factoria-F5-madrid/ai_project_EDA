# 📊 Proyecto EDA: Exploratory Data Analysis

<img width="11520" height="3456" alt="Banner Proyectos" src="https://github.com/user-attachments/assets/a6561ed2-24e1-451a-b75d-07e0e85aed63" />

## 📋 Planteamiento

Ustedes trabajan en el equipo de datos de una consultora. El CEO de un cliente les entrega un conjunto de datos que nadie ha mirado con calma y les pide algo muy concreto: **que le muestren datos limpios, con sentido, y la historia que hay detrás de ellos**, antes de decidir qué hacer con esa información.

El CEO no lee código: lee su informe. Por eso tienen que entender los datos, limpiarlos, explorarlos y contar lo que encontraron de forma clara.

## 🎯 Objetivo

Realizar un análisis exploratorio de datos (EDA) completo sobre un dataset real: cargarlo, entenderlo, limpiarlo, visualizarlo y comunicar sus conclusiones en un informe ejecutivo.

Pueden usar el dataset de su preferencia (ver [qué debe cumplir](#-qué-dataset-puedo-usar)). Si no tienen uno definido, usen los datos públicos de **COVID-19 en Estados Unidos** del [COVID Tracking Project](https://covidtracking.com/data/download), que registró casos, pruebas, hospitalizaciones y fallecimientos por estado hasta marzo de 2021.

> Cuéntennos la historia que leyeron en los datos :)

## 🛠️ Requisitos Técnicos

1. Python 3 y Jupyter Notebook (en VS Code o similar)
2. `requests` y/o `pandas` para cargar los datos
3. `pandas` y `numpy` para limpiar y transformar
4. `matplotlib`, `seaborn` y/o `plotly` para visualizar
5. Control de versiones con Git y GitHub (ramas ordenadas y mensajes de commit claros)

## 📅 Plazos

Una semana.

## 📦 Entregables

1. Repositorio en GitHub con al menos un **Jupyter notebook** donde el análisis esté ordenado y explicado paso a paso (con texto en markdown entre las celdas de código, no solo código).
2. Un **informe ejecutivo** con las conclusiones, pensado para alguien que no sabe de datos. Pueden ver un ejemplo [aquí](https://github.com/user-attachments/files/22068569/reporte.ejecutivo.EDA.Formula1.pdf).
3. `README.md` del repositorio con: de dónde salen los datos, cómo instalar las librerías y cómo ejecutar el notebook.
4. Archivo `requirements.txt` para que cualquier persona pueda reproducir su análisis.

## 🗂️ ¿Qué dataset puedo usar?

Si eligen uno propio, debe cumplir esto para que haya material suficiente de análisis:

- Al menos **1.000 filas** y **8 columnas**.
- Mezcla de columnas **numéricas, categóricas y de fecha** (o al menos numéricas y categóricas).
- Con **valores faltantes o datos sucios reales** (si es perfecto, no hay nada que limpiar).
- Que les interese: se nota en el informe.

Algunas fuentes: [Kaggle](https://www.kaggle.com/datasets), [datos.gob.es](https://datos.gob.es/), o cualquier API pública.

<details>
<summary><strong>🦠 Guía del dataset COVID (opcional)</strong></summary>

```python
import requests
import pandas as pd

url = "https://api.covidtracking.com/v1/states/daily.json"
df = pd.DataFrame(requests.get(url).json())
```

Qué van a encontrar (para que no los sorprenda):

- Unas **20.780 filas y 56 columnas**: un registro por estado o territorio y por día, del 13 de enero de 2020 al 7 de marzo de 2021.
- La columna `date` viene como número entero (`20200313`), no como fecha. Hay que convertirla: `pd.to_datetime(df["date"].astype(str), format="%Y%m%d")` (el `astype(str)` evita un aviso en pandas 3).
- **Muchas columnas casi vacías** (varias con más del 80% de nulos). Decidir qué hacer con ellas forma parte del análisis.
- Hay valores **negativos** en columnas de incrementos diarios (por ejemplo `deathIncrease`). Son correcciones que hicieron los estados, y conviene decidir qué hacer con ellas.
- Es una descarga grande (unos 29 MB). Guárdenla en un CSV para no pedirla cada vez.
- Los números son **acumulados** y **absolutos**: un estado grande siempre tendrá más casos que uno pequeño. Piensen cómo compararlos de forma justa.

</details>

## 🏆 Niveles de Entrega

Cada nivel incluye todo lo del anterior. Pueden elegir hasta dónde llegar, pero un nivel bien hecho vale más que dos a medias.

### 🟢 Nivel Esencial

- Cargar los datos y revisar su estructura: `shape`, `info()`, `head()`, `describe()`
- Identificar **valores faltantes y duplicados**, y decidir qué hacer con cada uno
- Corregir los tipos de datos (por ejemplo, convertir fechas)
- Eliminar o renombrar columnas explicando el porqué
- **Análisis univariado**: al menos 3 variables (histograma, conteo, boxplot)
- **Análisis bivariado**: al menos 3 relaciones entre dos variables
- Mínimo **5 visualizaciones** con título, ejes con nombre y leyenda cuando haga falta
- Responder por escrito al menos **3 preguntas** que ustedes mismos se plantearon al principio
- Notebook ordenado, con texto explicativo y que se ejecute de arriba abajo sin errores

### 🟡 Nivel Medio

- Justificar cada decisión de limpieza (por qué imputo con la mediana, por qué elimino esta columna)
- Detectar **valores atípicos** (outliers) con boxplots o el rango intercuartílico, y decidir qué hacer con ellos
- Agrupar y resumir con `groupby`, `agg` y tablas dinámicas (`pivot_table`)
- Crear **al menos 3 variables nuevas** (feature engineering): rangos o grupos de una variable numérica, partes de una fecha (mes, año), ratios, porcentajes, etc.
- **Matriz de correlación** con heatmap y su interpretación
- Si su dataset tiene fechas, análisis de **tendencias en el tiempo** (gráficos de líneas). Si no tiene, comparar cómo cambia el comportamiento entre grupos
- Informe ejecutivo de 1 a 2 páginas con conclusiones claras y gráficos que las respalden

### 🟠 Nivel Avanzado

- **Normalizar** para comparar con justicia (por ejemplo, ratios por cada 100 o 1.000 unidades, o porcentajes en lugar de totales)
- **Enriquecer el análisis con una segunda fuente de datos** (`merge`) que aporte contexto al dataset principal
- Analizar datos de calidad dudosa: valores imposibles, correcciones, inconsistencias entre columnas, y documentar cómo las trataron
- Aplicar al menos una **transformación justificada** y explicar por qué: media móvil si hay series temporales, escala logarítmica o escalado si hay distribuciones muy sesgadas
- Comparar **segmentos o grupos** (regiones, categorías, periodos) con visualizaciones claras
- Gráficos interactivos con `plotly`
- Código de limpieza reutilizable en **funciones** o en un archivo `.py` aparte

### 🔴 Nivel Experto

- **Dashboard interactivo** (Streamlit, Dash o similar) donde el CEO pueda filtrar y explorar solo
- **Pipeline reproducible**: un script que cargue los datos, los limpie y guarde el resultado, ejecutable con un solo comando
- **Tests** (con `pytest`) de sus funciones de limpieza, escritos antes que la función
- Informe de calidad de datos: qué faltaba, qué se corrigió, qué quedó pendiente y por qué
- Presentación del hallazgo principal en 5 minutos, con storytelling para público no técnico
- Publicación del dashboard o del informe en un enlace accesible

## 🌟 Competencias

- Evaluar conjuntos de datos utilizando herramientas de análisis y de visualización de datos
- Uso y gestión de formato `.csv` y de datos desde APIs
- Limpieza y preprocesado de datos
- Visualización de datos (seaborn, matplotlib, plotly)
- Análisis exploratorio detallado (EDA)
- Comunicar resultados de datos a público no técnico
