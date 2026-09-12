# Evidencia 3 — Primer análisis de datos con Python

* **Módulo:** [3.1 Python — Fundamentos para análisis de datos](https://swcarpentry.github.io/python-novice-inflammation/) | **Fecha:** 11 de septiembre de 2026

> **Objetivo:** Desarrollar un ejercicio completo de análisis de datos científicos utilizando Python, NumPy y Matplotlib, abarcando carga de datos individuales y por lotes, exploración matricial, cálculo de métricas estadísticas multidimensionales, generación de visualizaciones técnicas e interpretación fundamentada de resultados.

---

## 1. Carga de Datos y Procesamiento por Lotes

Se trabajó con la serie de conjuntos de datos tabulares provistos en el taller oficial de **Software Carpentry**:
* **Dataset individual base:** `semana-02/ejercicios/data/inflammation-01.csv` cargado mediante `np.loadtxt(fname='data/inflammation-01.csv', delimiter=',')`.
* **Procesamiento de la serie clínica completa:** Automatización por lotes utilizando el módulo `glob` (`glob.glob('data/inflammation-*.csv')`) para iterar y auditar sistemáticamente los 12 archivos de pacientes del estudio.
* **Estructura en memoria:** Almacenamiento continuo en objetos `ndarray` de NumPy, optimizando el acceso a memoria RAM y permitiendo operaciones vectorizadas de alto rendimiento sin bucles explícitos.

---

## 2. Exploración Inicial

Mediante inspección matricial sobre los datos se obtuvieron las propiedades estructurales del estudio:
* **Dimensiones (`data.shape`):** `(60, 40)` $\rightarrow$ Representa **60 pacientes** (filas) monitoreados durante **40 días consecutivos** (columnas).
* **Tipo de dato interno (`data.dtype`):** `float64` (valores numéricos continuos de punto flotante de 64 bits).
* **Inspección por Rebanado (Slicing 2D):**
  * Valor inicial del estudio (`data[0, 0]`): Valor `0.0`.
  * Punto medio del estudio (`data[30, 20]`): Paciente 30 en el día 20 con inflamación de `13.0`.
  * Submatriz muestral (`data[0:3, 0:5]`): Extracción de bloque $3 \times 5$ correspondiente a los 3 primeros pacientes durante sus primeros 5 días.

---

## 3. Análisis Estadístico y Funciones de Auditoría

Se aplicaron agregaciones vectorizadas sobre las dos dimensiones matriciales mediante el parámetro `axis`:

1. **Métricas Diarias Globales (`axis=0`):** Colapso vertical de los 60 pacientes para calcular el comportamiento longitudinal de la enfermedad en cada uno de los 40 días:
   * Media diaria: `promedio_diario = np.mean(data, axis=0)` $\rightarrow$ `(40,)`
   * Máximo diario: `maximo_diario = np.max(data, axis=0)` $\rightarrow$ `(40,)`
   * Mínimo diario: `minimo_diario = np.min(data, axis=0)` $\rightarrow$ `(40,)`
2. **Métricas Individuales Transversales (`axis=1`):** Colapso horizontal de los 40 días para cuantificar el impacto medio en cada individuo:
   * Media individual: `promedio_pacientes = np.mean(data, axis=1)` $\rightarrow$ `(60,)`
3. **Análisis Diferencial (`np.diff`):** Cálculo de tasas de cambio discretas entre días adyacentes para evaluar la pendiente de las curvas.
4. **Modularización:** Implementación de funciones reutilizables (`detectar_anomalias` y `analizar`) para ejecutar reglas heurísticas de validación clínica de manera automatizada.

---

## 4. Visualización Técnica

Se implementaron dos estrategias gráficas utilizando `matplotlib.pyplot`:

1. **Mapa de Calor Bidimensional (`imshow`):** Proyección integral de las 2400 observaciones en un plano cromático que permite distinguir a simple vista la fase aguda de la enfermedad (días 15 al 25).
2. **Panel Multieje en Tríptico (Subplots 1x3):** Gráficos simultáneos de promedio, máximo y mínimo diario con márgenes calibrados (`tight_layout(rect=[0, 0, 1, 0.95])`), cuadrículas auxiliares (`major` y `minor`) y renderizado ortogonal en escalones (`step`):
   * *Panel 1 (Promedio):* Curva de evolución temporal suave con marcadores circulares.
   * *Panel 2 (Máximo):* Curva de picos diarios con marcadores cuadrados.
   * *Panel 3 (Mínimo):* Curva basal trazada en escalones con marcadores triangulares.
3. **Auditoría Gráfica por Lotes:** Generación automatizada de trípticos para los archivos de la serie clínica (`inflammation-01.csv`, `inflammation-02.csv`, `inflammation-03.csv`).

---

## 5. Interpretación de Resultados y Diagnóstico Clínico

Del análisis exploratorio, estadístico y comparativo de los archivos se concluye:
1. **Dinámica Temporal:** En condiciones estándar, la inflamación describe una curva acampanada con inicio bajo (días 0–5), un pico generalizado hacia el día 20 y un descenso progresivo hacia el día 40.
2. **Detección Forense de Datos Sintéticos (`inflammation-01.csv` e `inflammation-02.csv`):**
   * La curva de **máximos** describe una rampa lineal geométricamente exacta ($0 \to 20 \to 0$). Al aplicar `np.diff()`, la tasa de cambio es estrictamente $1.0$ durante todo el ascenso, comportamiento matemáticamente determinista incompatible con datos biológicos reales.
   * La curva de **mínimos** asciende y desciende en **gradas fijas de 4 días** por escalón.
   * *Diagnóstico:* Ambos conjuntos de datos provienen de algoritmos sintéticos generados por computadora.
3. **Detección de Falla Instrumental (`inflammation-03.csv`):**
   * La curva de **mínimos** se mantiene en `0.0` durante los 40 días consecutivos (`np.sum(min_diario) == 0`).
   * *Diagnóstico:* Pérdida de señal de sensor o registros clínicos defectuosos durante la toma de datos.

---

## 6. Recursos y Entregables

* **Archivo Adjunto:** Cuaderno interactivo [`03-analisis-datos.ipynb`](../ejercicios/03-analisis-datos.ipynb) adjunto en el envío (contiene las 18 celdas ejecutadas con salidas y gráficos renderizados).
* **Repositorio Oficial en GitHub:** [Klopezxd/cern-preparation-program](https://github.com/Klopezxd/cern-preparation-program/tree/main/semana-02)
* **Visualización en Línea del Cuaderno:** [03-analisis-datos.ipynb en GitHub](https://github.com/Klopezxd/cern-preparation-program/blob/main/semana-02/ejercicios/03-analisis-datos.ipynb)
