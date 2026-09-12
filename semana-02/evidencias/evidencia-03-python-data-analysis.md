# Evidencia 3 — Primer análisis de datos con Python

* **Módulo:** [3.1 Python — Fundamentos para análisis de datos](https://swcarpentry.github.io/python-novice-inflammation/) | **Fecha:** 11 de septiembre de 2026

> **Objetivo:** Desarrollar un ejercicio completo de análisis de datos científicos utilizando Python, NumPy y Matplotlib, abarcando carga de datos, exploración matricial, cálculo de métricas estadísticas, generación de visualizaciones técnicas e interpretación fundamentada de resultados.

---

## 1. Carga de Datos

Se utilizó el conjunto de datos tabular clínico provisto en el material oficial del workshop de **Software Carpentry**:
* **Archivo:** `semana-02/ejercicios/data/inflammation-01.csv`
* **Método de carga:** `np.loadtxt(fname='data/inflammation-01.csv', delimiter=',')`
* **Estructura en memoria:** Almacenamiento continuo en un objeto `ndarray` de NumPy, garantizando eficiencia y operaciones vectorizadas en C.

---

## 2. Exploración Inicial

Mediante inspección programática se obtuvieron las dimensiones y propiedades fundamentales del dataset:
* **Dimensiones (`data.shape`):** `(60, 40)` $\rightarrow$ Representa **60 pacientes** (filas) evaluados durante **40 días consecutivos** (columnas).
* **Tipo de dato interno (`data.dtype`):** `float64` (valores numéricos continuos de punto flotante de 64 bits).
* **Inspección por Rebanado (Slicing 2D):**
  * Primer registro (`data[0, 0]`): Valor `0.0`.
  * Punto medio del estudio (`data[30, 20]`): Paciente 30 en el día 20 con inflamación moderada-alta.
  * Muestra de bloque (`data[0:3, 0:5]`): Extracción de una submatriz de $3 \times 5$ correspondiente a los 3 primeros pacientes durante sus primeros 5 días.

---

## 3. Análisis Estadístico

Se aplicaron agregaciones vectorizadas sobre las dos dimensiones mediante el parámetro `axis` (regla de colapso matricial):

1. **Promedio Diario (`axis=0`):** Colapso vertical de los 60 pacientes para calcular el nivel medio de inflamación por día de tratamiento:
   ```python
   promedio_diario = np.mean(data, axis=0)  # Shape resultante: (40,)
   ```
2. **Máximo Diario (`axis=0`):** Detección del pico de inflamación diario en todo el grupo clínico:
   ```python
   maximo_diario = np.max(data, axis=0)  # Shape resultante: (40,)
   ```
3. **Mínimo Diario (`axis=0`):** Comportamiento basal o pacientes con menor inflamación diaria:
   ```python
   minimo_diario = np.min(data, axis=0)  # Shape resultante: (40,)
   ```
4. **Promedio Individual por Paciente (`axis=1`):** Colapso horizontal de los 40 días para cuantificar el impacto general en cada individuo:
   ```python
   promedio_pacientes = np.mean(data, axis=1)  # Shape resultante: (60,)
   ```
5. **Tasa de Cambio y Derivada Discreta (`np.diff`):** Medición de la pendiente entre días consecutivos para validar la naturaleza de las curvas.

---

## 4. Visualización Técnica

Se implementaron dos enfoques visuales utilizando `matplotlib.pyplot`:

1. **Mapa de Calor Bidimensional (`imshow`):** Permite inspeccionar los 2400 puntos de datos en una sola vista. Revela un incremento homogéneo de inflamación hacia el centro de la matriz (días 15 al 25).
2. **Panel Múltiple de Subplots en Tríptico:** Visualización simultánea de tres métricas clave con cuadrículas auxiliares (`grid(True, linestyle='--')`), marcas de escala explícitas (`set_xticks`) y renderizado ortogonal en escalones (`step`):
   * *Panel 1:* Curva de inflamación promedio (evolución temporal suave).
   * *Panel 2:* Curva de inflamación máxima (rampa lineal).
   * *Panel 3:* Curva de inflamación mínima (gradas discretas).

---

## 5. Interpretación de Resultados

Del análisis exploratorio y visual se desprenden las siguientes conclusiones científicas:
1. **Comportamiento Temporal:** La inflamación general evoluciona siguiendo una curva acampanada, con valores bajos al inicio (días 0–5), un pico generalizado alrededor del día 20 y un descenso gradual hacia el día 40.
2. **Anomalía de Datos Sintéticos en `inflammation-01.csv`:**
   * La curva de **máximos** forma una rampa lineal geométricamente exacta ($1, 2, 3 \dots 20$ y posterior descenso unitario). Al aplicar `np.diff()`, la tasa de cambio es idéntica a $1.0$ en todos los días de subida, lo cual no ocurre en biología real.
   * La curva de **mínimos** asciende y desciende en **gradas fijas de 4 días** por escalón (efecto identificado y comprobado visualmente con `step`).
   * *Diagnóstico:* El dataset fue generado sintéticamente mediante fórmulas programáticas discretas y no proviene de mediciones biológicas reales.

---

## 6. Cuaderno de Trabajo y Recursos Entregables

* **Cuaderno Jupyter completo:** [03-analisis-datos.ipynb](../ejercicios/03-analisis-datos.ipynb)
* **Repositorio en GitHub:** [Klopezxd/cern-preparation-program](https://github.com/Klopezxd/cern-preparation-program/tree/main/semana-02)
