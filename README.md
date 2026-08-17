# 📊 Análisis de Comportamiento y Segmentación de Usuarios — ConnectaTel

Este repositorio contiene el proyecto de procesamiento de datos, limpieza, análisis exploratorio (EDA), detección de *outliers* y segmentación de clientes para la empresa de telecomunicaciones **ConnectaTel**.

El objetivo es diagnosticar la calidad de los datos, comprender los patrones de consumo (llamadas, mensajes, minutos) y perfil demográfico (edad, plan), para formular recomendaciones estratégicas y oportunidades de negocio.

---

## 🎯 Objetivo del Proyecto

* **Limpieza y Preparación de Datos:** Identificar y tratar valores *sentinels* (`-999` en `age`, `'?'` en `city`), fechas incoherentes fuera de rango (`reg_date` en 2026) y nulos marginales o estructurales.
* **Análisis Exploratorio (EDA):** Analizar la distribución de variables clave (edad, número de llamadas, número de mensajes, total de minutos) según el plan contratado (*Básico* vs *Premium*).
* **Tratamiento e Interpretación de Outliers:** Evaluar los límites intercuartílicos (IQR) en consumos extremos y justificar su conservación como *heavy users* de alto valor comercial.
* **Segmentación de Clientes:** Clasificar a los usuarios según su nivel de consumo (`grupo_uso`: *Bajo uso*, *Uso medio*, *Alto uso*) y su perfil demográfico (`grupo_edad`: *Joven*, *Adulto*, *Adulto Mayor*).
* **Diagnóstico Ejecutivo:** Proporcionar conclusiones orientadas al negocio, identificando segmentos clave y propuestas de optimización de planes.

---

## 💾 Datasets Utilizados

El análisis se basa en dos fuentes de datos principales:

1. **`users.csv`** (Información de usuarios):
   * `user_id`: Identificador único del usuario (rango continuo 10000 a 13999, 4,000 registros).
   * `age`: Edad del usuario.
   * `city`: Ciudad de residencia.
   * `reg_date`: Fecha de alta en el servicio.
   * `plan`: Modalidad del plan (*Básico* o *Premium*).
   * `churn_date`: Fecha de cancelación del servicio (88.4% nulos, correspondiente a usuarios activos).

2. **`usage.csv`** (Historial de interacciones y consumo):
   * `user_id`: Identificador único del cliente.
   * `date`: Fecha de la transacción/evento (50 nulos, <0.1%).
   * `type`: Tipo de interacción (`call` o `text`).
   * `duration`: Duración en minutos para llamadas (nulo estructural en mensajes).
   * `length`: Cantidad de caracteres para mensajes (nulo estructural en llamadas).

---

## 🚀 Etapas del Análisis Realizadas

1. **Exploración de Calidad de Datos:**
   * Diagnóstico de nulos estructurales (MAR) y marginales.
   * Detección de caracteres y valores *sentinel* (`-999`, `'?'`).
   * Validación de consistencia temporal en fechas.

2. **Limpieza y Curación:**
   * Sustitución de `-999` por la mediana de edad.
   * Reclasificación de `'?'` en `city` como `'Desconocido'`.
   * Conversión de fechas a `datetime` y manejo de inconsistencias (`pd.NaT`).
   * Eliminación de nulos marginales en `date`.

3. **Agregación y Construcción del `user_profile`:**
   * Consolidación por cliente mediante `merge` para integrar métricas acumuladas de llamadas, mensajes y minutos.

4. **Análisis Exploratorio y Visualización:**
   * Histogramas de distribución con curvas KDE por tipo de plan.
   * Diagramas de caja (*boxplots*) para identificar sesgos y valores atípicos.
   * Evaluación de simetría y forma de distribuciones.

5. **Análisis del Rango Intercuartílico (IQR):**
   * Cálculo de límites inferiores y superiores en métricas de consumo.
   * Justificación técnica y comercial para mantener los *outliers*.

6. **Segmentación y Análisis Ejecutivo:**
   * Categorización en `grupo_uso` y `grupo_edad`.
   * Visualización con `sns.countplot`.
   * Redacción del resumen ejecutivo e *insights* de negocio.

---

* **Herramientas:** Python (Pandas, NumPy, Seaborn, Matplotlib)), Jupyter / Google Colab

---

## ▶ Cómo abrir el notebook en Google Colab

Haz clic en el siguiente botón:

(https://github.com/thaliamejiapotafolio/telecom-analysis/blob/main/S7%20Version-Estudiante-Project-ConnectaTel%20(1).ipynb)

1. Abre el archivo `.ipynb` en GitHub
2. Haz clic en **Open in Colab**

## 📘 Cómo reproducir el análisis

1. Abre `S7 Version-Estudiante-Project-ConnectaTel (1).ipynb`
2. Ejecuta las celdas en orden
3. El notebook carga automáticamente el dataset desde `/data/` o desde un enlace público (según corresponda)
