# Modelos Estadísticos Avanzados de Análisis de Datos

> Aplicando **Regresión Múltiple**, **Análisis Factorial (AFE/AFC)**, **Clustering Mixto** y **Series de Tiempo** para explicar, segmentar y pronosticar fenómenos reales en movilidad urbana, educación y salud ocupacional, a través de un pipeline estadístico completo en R.

![R](https://img.shields.io/badge/R-4.x-276DC3?logo=r&logoColor=white)
![RMarkdown](https://img.shields.io/badge/RMarkdown-HTML--Report-blue?logo=rstudio&logoColor=white)
![lavaan](https://img.shields.io/badge/lavaan-SEM%2FAFC-8A2BE2)
![clustMixType](https://img.shields.io/badge/clustMixType-K--Prototypes-ED8B00)
![CUC](https://img.shields.io/badge/Colegio%20Universitario%20de%20Cartago-CUC-002F6C)
![Licencia](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey)

---

## 📑 Tabla de Contenidos

- [Descripción](#-descripción)
- [Objetivos](#-objetivos)
- [Tecnologías](#-tecnologías)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Instalación](#️-instalación)
- [Configuración](#-configuración)
- [Uso](#-uso)
- [Pipeline](#-pipeline)
- [Análisis Implementados](#-análisis-implementados)
- [Normas de Calidad](#-normas-de-calidad)
- [Autores](#-autores)

---

## 📌 Descripción

Este proyecto integra las técnicas de análisis multivariado estudiadas en el curso **BD-165** mediante su aplicación sobre **tres conjuntos de datos reales** e independientes: demanda de bicicletas compartidas, impacto de la IA generativa en estudiantes, y salud mental/burnout digital. Para cada uno se desarrolla un flujo completo — introducción, descripción, extracción, EDA, modelado y discusión — documentado en un único reporte dinámico en RMarkdown con navegación por pestañas y estilo institucional propio.

| Aspecto | Detalle |
|---|---|
| **Curso** | BD-165 · Modelos Estadísticos Avanzados de Análisis de Datos — CUC |
| **Docente** | Prof. David Martínez Salazar |
| **Datasets** | 3 conjuntos independientes (movilidad, educación, salud ocupacional) |
| **Entregable** | Reporte HTML autocontenido (`self_contained: true`) |

---

## 🎯 Objetivos

- Cuantificar el efecto de variables climáticas y temporales sobre la demanda horaria de bicicletas mediante **regresión lineal múltiple**, con diagnóstico de multicolinealidad (VIF).
- Segmentar patrones diarios de demanda con **K-Means** y proyectar el flujo de uso a corto plazo con **suavización exponencial Holt-Winters**.
- Identificar la estructura latente del uso de IA generativa en estudiantes mediante **Análisis Factorial Exploratorio (AFE)** y validarla con **Análisis Factorial Confirmatorio (AFC)** (`lavaan`, estimador WLSMV).
- Construir perfiles mixtos de estudiantes combinando variables numéricas y categóricas mediante **K-Prototypes** (distancia de Gower).
- Evaluar el efecto conjunto de variables laborales y digitales sobre el perfil sintomático de burnout mediante **MANOVA**, complementado con regresión múltiple y **K-Means**.
- Documentar cada modelo con verificación explícita de supuestos, interpretación conceptual de resultados y reproducibilidad total del pipeline de datos.
- Definir un framework de *prompting* estructurado para análisis de sentimiento de comentarios de clientes como módulo complementario de NLP.

---

## 🛠️ Tecnologías

| Herramienta | Propósito |
|---|---|
| R (4.x) | Lenguaje base del análisis |
| RMarkdown / knitr | Generación del reporte dinámico HTML |
| dplyr · tidyr · lubridate | Manipulación, limpieza y manejo de fechas |
| ggplot2 · GGally · plotly | Visualización estática e interactiva |
| psych | KMO, prueba de Bartlett, correlaciones mixtas (`mixedCor`) y AFE |
| lavaan · semPlot | Análisis Factorial Confirmatorio (AFC) y diagramas de modelo |
| factoextra · cluster · clustMixType | Selección de clústeres, silueta y K-Prototypes |
| car · gvlma | Diagnóstico de regresión (VIF, supuestos globales) |
| forecast | Series de tiempo (Holt-Winters, `accuracy`) |
| mice · corrplot | Imputación de datos faltantes y matrices de correlación |
| ade4 · nortest · modeest · tidyverse | Análisis multivariado, normalidad y estimación de moda |

---

## 📁 Estructura del Repositorio

```
Modelos-Estadisticos-Avanzados/
│
├── Data/                                            # Fuentes de datos primarias (no versionado)
│   ├── SeoulBikeData.csv                             # Dataset 1: demanda horaria de bicicletas (Seúl)
│   ├── ai_student_impact_dataset.csv                 # Dataset 2: uso de IA y desempeño estudiantil
│   └── mental_health_burnout_prediction_dataset.csv  # Dataset 3: salud mental y burnout digital
│
├── Proyecto_Final_BD165.Rmd                          # Código fuente RMarkdown principal del reporte
├── styles_proyecto_final.css                         # Hoja de estilos institucional (menú lateral, tipografía, paleta)
├── logo.png                                          # Logotipo oficial del CUC
├── .gitignore                                        # Filtros de archivos temporales e historial de R
└── README.md                                         # Documentación principal del proyecto
```

---

## ⚙️ Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/Modelos-Estadisticos-Avanzados.git
cd Modelos-Estadisticos-Avanzados
```

### 2. Instalar R y RStudio

Se requiere **R (v4.0+)** y, opcionalmente, **RStudio** como entorno de desarrollo.

### 3. Instalar dependencias

```r
install.packages(c(
  "dplyr", "tidyr", "lubridate", "ggplot2", "GGally",
  "psych", "factoextra", "car", "gvlma", "forecast",
  "mice", "corrplot", "tidyverse", "ade4", "plotly",
  "nortest", "lavaan", "semPlot", "cluster", "modeest",
  "clustMixType", "rmarkdown", "knitr"
))
```

---

## 🔧 Configuración

Cree una carpeta `Data/` en la raíz del proyecto y coloque allí los tres archivos `.csv` requeridos:

```
Data/
├── SeoulBikeData.csv
├── ai_student_impact_dataset.csv
└── mental_health_burnout_prediction_dataset.csv
```

> ⚠️ La carpeta `Data/` está incluida en `.gitignore` y **no se versiona**; cada integrante debe colocar los archivos localmente antes de compilar el reporte.

---

## ▶️ Uso

### Compilar el reporte (Knit)

```r
rmarkdown::render("Proyecto_Final_BD165.Rmd")
```

O bien, desde RStudio: abrir `Proyecto_Final_BD165.Rmd` y hacer clic en el botón **Knit**.

El sistema genera un informe dinámico en formato **HTML autocontenido**, con la hoja de estilo `styles_proyecto_final.css` y el logotipo `logo.png` integrados, organizado en pestañas (una por dataset) con navegación lateral.

---

## 🔄 Pipeline

```
Data/*.csv (SeoulBikeData · ai_student_impact · mental_health_burnout)
                    │
                    ▼
        Extracción y Preparación
      (dplyr · tidyr · mice · lubridate)
                    │
                    ▼
        Análisis Exploratorio (EDA)
   (ggplot2 · GGally · corrplot · plotly)
                    │
      ┌─────────────┼──────────────────┐
      ▼             ▼                  ▼
  Bicicletas     Impacto IA      Burnout Digital
  Regresión      AFE / AFC       MANOVA
  K-Means        K-Prototypes    Regresión Múltiple
  Holt-Winters   (Gower)         K-Means
      │             │                  │
      └─────────────┴──────────────────┘
                    ▼
         Resultados e Interpretación
                    │
                    ▼
      Reporte HTML (RMarkdown + CSS institucional)
```

---

## 📊 Análisis Implementados

### Sistema de Bicicletas Compartidas — pestaña `SeoulBikeData`

- **Regresión Lineal Múltiple** — impacto del clima sobre `Bicis_Rentadas`, con diagnóstico VIF y descarte de `Punto_Rocio` por colinealidad con `Temperatura`.
- **K-Means** — segmentación de patrones diarios climáticos (variables estandarizadas, $k=4$ por método del codo), validada contra la estación real.
- **Holt-Winters** — suavización exponencial con estacionalidad semanal (`frequency = 7`) y evaluación de precisión (`accuracy`).

### Impacto de la IA en Estudiantes — pestaña `ai-student-impact-dataset`

- **Análisis Factorial Exploratorio (AFE)** — ejes principales con rotación `oblimin` sobre correlaciones mixtas (`mixedCor`, policóricas/tetracóricas).
- **Análisis Factorial Confirmatorio (AFC)** — validación de la estructura latente con `lavaan` (estimador WLSMV) sobre una partición independiente (50 % desarrollo / 50 % confirmación).
- **K-Prototypes** (`clustMixType`) — segmentación mixta de perfiles estudiantiles con distancia de Gower y validación de silueta.

### Salud Mental y Agotamiento Digital — pestaña `mental-health-burnout-dataset`

- **MANOVA** — efecto conjunto de predictores laborales/digitales sobre el perfil sintomático multivariado.
- **Regresión Lineal Múltiple** — estimación de niveles de agotamiento, comparando modelo completo vs. modelo reducido.
- **K-Means** — segmentación de perfiles de riesgo de burnout.

### Módulo NLP — Análisis de Sentimiento (SmarTech)

- Framework de *prompting* estructurado (rol · contexto · tarea por etapas · formato de salida) para clasificar comentarios de clientes de la empresa costarricense SmarTech en Positivo, Negativo o Neutral.

---

## 📏 Normas de Calidad

De acuerdo con la rúbrica oficial del curso:

- **Justificación teórica** de cada técnica en función de la naturaleza de las variables y la pregunta de investigación.
- **Interpretación conceptual** (2–4 líneas) de cada salida de código: tablas, p-valores, $R^2$, gráficos de codo, métricas de error.
- **Reproducibilidad garantizada**: rutas relativas (`Data/`), semillas fijadas (`set.seed()`) y código sin dependencias de variables locales.

---

## 👥 Autores

**Desmond Bermúdez Rodríguez** · **Nubia Elena Brenes Valerín** · **Pablo Marín Castillo** · **Wedell Orozco González** · **Kendall Solano Solís**

---

<p align="center">
  Proyecto desarrollado para el curso <strong>BD-165 · Modelos Estadísticos Avanzados de Análisis de Datos</strong> · Diplomado en Big Data<br>
  <strong>Colegio Universitario de Cartago (CUC)</strong>
</p>
