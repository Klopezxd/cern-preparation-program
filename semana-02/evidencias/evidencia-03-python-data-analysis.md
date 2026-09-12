# Evidencia 3 — Fundamentos de Python para análisis de datos

* **Módulo:** [3.1 Python — Fundamentos para análisis de datos](https://swcarpentry.github.io/python-novice-inflammation/) | **Fecha:** 11 de septiembre de 2026

> **Objetivo:** Aplicar las librerías NumPy y Matplotlib para cargar, manipular y visualizar matrices de datos científicos bidimensionales, identificar anomalías estadísticas mediante programación defensiva, y automatizar el procesamiento por lotes de múltiples archivos mediante bucles y la librería `glob`.

---

## 1. Cuaderno de Trabajo y Recursos

* **Cuaderno interactivo:** [03-analisis-datos.ipynb](../ejercicios/03-analisis-datos.ipynb)
* **Dataset clínico:** Archivos CSV en [`semana-02/ejercicios/data/`](../ejercicios/data/) (`inflammation-01.csv` a `inflammation-12.csv`).
* **Librerías principales:** `numpy` (2.5.3), `matplotlib` (3.11.2).

---

## 2. ¿Qué aprendí?

### A. Diferencia estructural: Listas de Python vs. Arrays de NumPy
Comprendí el modelo de memoria de NumPy frente a las listas tradicionales de Python. Mientras que una lista en Python almacena punteros dispersos a objetos independientes en memoria (lo que genera sobrecarga computacional y lentitud al iterar), un array de NumPy (`ndarray`) organiza los datos de forma homogénea en un bloque continuo de memoria RAM gestionado en lenguaje C. Esto permite la **vectorización**: ejecutar operaciones matemáticas masivas en paralelo sin requerir bucles `for` lentos.

### B. Indexación y Rebanado 2D (Slicing)
Asimilé la sintaxis matricial `matriz[filas, columnas]` y la convención de intervalos semiabiertos en Python (`inicio:fin`, donde el extremo superior queda excluido). Aprendí a extraer pacientes específicos (`data[10, :]`), días puntuales de todo el grupo (`data[:, 0]`) o bloques acotados de estudio (`data[0:3, 0:5]`).

### C. La regla de colapso de los Ejes (`axis=0` vs `axis=1`)
Consolidé el modelo mental de la agregación por ejes:
* **`axis=0` (colapso vertical):** Aplasta las 60 filas de pacientes hacia abajo, generando un vector de **40 promedios diarios** (`np.mean(data, axis=0)`).
* **`axis=1` (colapso horizontal):** Aplasta las 40 columnas de días de izquierda a derecha, produciendo un vector de **60 promedios por paciente** (`np.mean(data, axis=1)`).

### D. Visualización de Ingeniería y Automatización
Aprendí a no depender de gráficas por defecto: implementar cuadrículas explícitas (`grid`), calibrar pasos de ticks (`xticks`, `yticks`) y usar escalones (`step`) en lugar de interpolaciones diagonales (`plot`) para inspeccionar datos discretos. Finalmente, empaqueté el análisis en funciones reutilizables (`analizar` y `detectar_anomalias`) y sistematicé la lectura masiva de archivos con `glob.glob()`.

---

## 3. Hallazgos y Diagnóstico Forense de los Datos

Al generar el panel triple de subplots (Promedio, Máximo y Mínimo diario) se identificaron anomalías críticas en los datasets del ensayo clínico:

| Archivo | Comportamiento Observado | Diagnóstico Científico |
| :--- | :--- | :--- |
| **`inflammation-01.csv`** | Máximo lineal perfecto ($1, 2 \dots 20 \dots 0$) y mínimos en gradas exactas de 4 días. | **Datos sintéticos / simulados:** Las diferencias consecutivas (`np.diff`) son exactamente $1.0$ todos los días, demostrando una fórmula matemática artificial. |
| **`inflammation-02.csv`** | Idéntica rampa triangular y escalones en el mínimo que el archivo 01. | **Datos duplicados / plantilla artificial.** |
| **`inflammation-03.csv`** | Curva de máximos con ruido natural, pero mínimos en **cero absoluto constante** ($0.0$) durante los 40 días. | **Falla de instrumentación:** Presencia de pacientes no tratados o sensores averiados reportando ceros en cada jornada. |

---

## 4. Función más Útil e Interesante

La función más reveladora fue **`np.diff()`** combinada con `np.all()`. 

Frente a la comprobación superficial del tutorial (`max[20] == 20`), que podría cumplirse por azar en una curva fluctuante, `np.diff()` calcula la derivada discreta (la tasa de cambio entre días adyacentes). Comprobar que `np.all(np.diff(max_diario[:21]) == 1.0)` permitió demostrar con rigor matemático que el ascenso era una línea recta perfecta con pendiente unitaria, confirmando de manera irrefutable el carácter artificial del dataset.

---

## 5. Dificultad Encontrada y Cómo se Resolvió

1. **Interpretación Geométrica de las Gradas:** Al observar la gráfica de mínimos de `inflammation-01.csv`, se percibía visualmente que los escalones medían 3 unidades a pesar de estar formados por 4 días con el mismo valor. Se resolvió identificando el "problema de los postes de la cerca" ($N$ puntos generan $N-1$ intervalos de distancia horizontal) y sustituyendo la interpolación lineal de `plt.plot()` por `plt.step()`, lo que renderizó escalones ortogonales exactos a 90 grados.
2. **Vinculación del Intérprete en el IDE:** VS Code mantuvo en caché los entornos previos sin listar de inmediato el nuevo entorno virtual en su selector gráfico de Jupyter. Se resolvió configurando el intérprete en `.vscode/settings.json` y registrando el kernelspec formalmente mediante `python -m ipykernel install`.
