# Análisis de Dengue en Colombia

Proyecto académico de análisis de datos epidemiológicos sobre dengue en Colombia para el periodo 2010-2024. El repositorio organiza una cadena reproducible de notebooks para comprender la estructura del dataset, explorar distribuciones, estudiar relaciones entre variables, revisar outliers, preparar datos y analizar patrones temporales.

El enfoque del proyecto es descriptivo y exploratorio. No incluye machine learning, forecasting ni inferencia causal.

## Objetivos

- Comprender la estructura de un panel epidemiológico municipio-semana.
- Evaluar calidad, completitud, duplicados, consistencia lógica y cobertura temporal.
- Caracterizar la distribución de variables epidemiológicas, climáticas, ambientales, demográficas y de movilidad.
- Identificar faltantes, ceros estructurales, asimetrías, colas largas y posibles outliers.
- Documentar decisiones analíticas con notebooks, figuras y tablas reutilizables.
- Preparar insumos para análisis posteriores y escritura académica.

## Dataset

El proyecto usa un dataset de dengue, clima, ambiente, población y movilidad para Colombia entre 2010 y 2024.

Archivo principal:

```text
data/raw/raw_dataset.csv
```

Archivo final descargado desde Kaggle o fuente externa equivalente:

```text
data/raw/final_dataset.csv
```

Cada fila representa una observación municipio-semana. Las variables principales incluyen:

- Identificadores: `COD_MUN_N`, `ANO`, `SEMANA`, `MES`, `week_start`.
- Epidemiológicas: `casos_totales`, grupos de edad, sexo y estrato socioeconómico.
- Climáticas: `temp_mean`, `prec_total`.
- Ambientales y macroclima: `ndvi_mean`, `oni_anom`, `oni_total`.
- Demográficas y movilidad: `poblacion`, `Flujo_in`.

## Estructura

```text
colombia-dengue-data-analysis/
|-- data/
|   |-- raw/
|   |   |-- raw_dataset.csv
|   |   `-- final_dataset.csv
|   |-- interim/
|   `-- processed/
|-- docs/
|   |-- article_draft.docx
|   |-- final_article.pdf
|   `-- references.bib
|-- figures/
|   |-- data_understanding/
|   |-- eda/
|   |-- eda_univariate/
|   |   |-- 00_panorama/
|   |   |-- 01_epidemiologicas/
|   |   |-- 02_estratificacion/
|   |   |-- 03_climaticas/
|   |   |-- 04_ambientales_macroclima/
|   |   |-- 05_demografia_flujo/
|   |   |-- 06_comparaciones_violin/
|   |   |-- 07_faltantes/
|   |   `-- 08_categoricas_temporales/
|   |-- outliers/
|   `-- preprocessing/
|-- notebooks/
|   |-- 00_data_understanding.ipynb
|   |-- 01_eda_univariate.ipynb
|   |-- 02_eda_multivariate.ipynb
|   |-- 03_outliers.ipynb
|   |-- 04_preprocessing.ipynb
|   `-- 05_project_documentation.ipynb
|-- tables/
|   |-- data_understanding/
|   `-- eda_univariate/
|-- LICENSE
|-- README.md
`-- requirements.txt
```

## Uso de carpetas

`data/raw/` contiene datos originales y no debe modificarse.

`data/interim/` está reservado para datasets intermedios generados durante outliers o preprocesamiento.

`data/processed/` está reservado para datasets finales listos para análisis posterior.

`figures/` almacena visualizaciones exportadas por los notebooks. El notebook `01_eda_univariate.ipynb` ya usa subcarpetas temáticas dentro de `figures/eda_univariate/`.

`tables/` almacena tablas importantes exportadas desde los notebooks. No se usa para cada tabla auxiliar, solo para resultados que documentan calidad, decisiones o hallazgos reutilizables.

Una carpeta `src/` puede incorporarse más adelante para centralizar funciones reutilizables de carga, visualización, preprocesamiento y detección de outliers. Por ahora, la lógica principal vive en los notebooks.

## Notebooks

Ejecutar los notebooks en orden:

1. `00_data_understanding.ipynb`: comprensión inicial del dataset, estructura panel, duplicados, faltantes, integridad lógica, diccionario de variables y alertas principales.
2. `01_eda_univariate.ipynb`: análisis exploratorio univariado por variable o grupo temático; distribuciones, ceros, asimetría, curtosis, escalas logarítmicas, violin plots y problemas para notebooks posteriores.
3. `02_eda_multivariate.ipynb`: correlaciones Pearson/Spearman, OLS exploratorio, VIF, relaciones bivariadas y comparaciones entre grupos.
4. `03_outliers.ipynb`: detección multi-método (IQR, MAD, Isolation Forest, LOF), clasificación contextual y decisiones de tratamiento.
5. `04_preprocessing.ipynb`: evaluación de imputación previa, tratamiento de ceros, transformaciones log, lags temporales, rolling means y exportación del dataset procesado.
6. `05_project_documentation.ipynb`: documentación del proceso analítico completo, decisiones metodológicas, hallazgos consolidados, limitaciones y líneas futuras.

## Tablas Exportadas

El notebook `00_data_understanding.ipynb` genera tablas en:

```text
tables/data_understanding/
```

Tablas principales:

- `dataset_overview.csv`
- `panel_completeness_by_year.csv`
- `missing_values_summary.csv`
- `integrity_checks.csv`
- `variable_dictionary.csv`
- `key_alerts_for_next_steps.csv`

El notebook `01_eda_univariate.ipynb` genera tablas en:

```text
tables/eda_univariate/
```

Tablas principales:

- `variables_not_for_distribution.csv`
- `univariate_summary.csv`
- `univariate_next_steps.csv`

## Instalación

Crear y activar un entorno virtual:

```bash
python -m venv .venv
```

En Windows:

```bash
.venv\Scripts\activate
```

En macOS o Linux:

```bash
source .venv/bin/activate
```

Instalar dependencias:

```bash
pip install -r requirements.txt
```

## Ejecución

Desde la raíz del proyecto:

```bash
jupyter notebook
```

Luego abrir la carpeta `notebooks/` y ejecutar cada notebook de arriba hacia abajo.

## Dependencias Principales

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- jupyter
- notebook

## Estado Actual

- `00_data_understanding.ipynb` y `01_eda_univariate.ipynb` están estructurados como notebooks iniciales de comprensión y EDA.
- `figures/` ya se usa para almacenar visualizaciones exportadas.
- `tables/` ya se usa para guardar tablas clave de los notebooks 00 y 01.
- `data/interim/` y `data/processed/` quedan disponibles para etapas posteriores del flujo.
- La carpeta `src/` queda como una mejora posible para etapas posteriores, cuando convenga mover funciones repetidas fuera de los notebooks.

## Autores

Camilo Mosquera & Jose Miguel Correa

## Licencia

Este proyecto está bajo licencia **MIT License** (ver archivo `LICENSE`).

La licencia aplica al código, notebooks y documentación creados para este repositorio. No otorga derechos sobre datasets externos incluidos o referenciados, que permanecen sujetos a sus licencias y términos de uso originales.

El dataset de dengue, clima, ambiente y población utilizado en este proyecto proviene de fuentes externas (Kaggle u equivalente) y debe citarse de acuerdo con los términos de uso de esas fuentes.
