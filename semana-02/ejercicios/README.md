# Ejercicios Prácticos – Semana 2

Este directorio documenta la resolución de los ejercicios prácticos de la Semana 2.

---

## 1. Control de Versiones con Git (Repositorio Satélite)

* **Repositorio en GitHub:** [Klopezxd/git-fundamental-practice](https://github.com/Klopezxd/git-fundamental-practice)
* **Objetivo:** Ejecutar un flujo de trabajo completo de Git desde la terminal:
  1. Inicialización de repositorio local con rama `main`.
  2. Construcción de historial con 3 commits atómicos y descriptivos.
  3. Configuración de exclusiones científicas mediante `.gitignore`.
  4. Inspección diferencial con `git diff` y `git diff --staged`.
  5. Sincronización remota mediante `git remote` y `git push`.
* **Evidencia formal:** Ver [evidencia-01-git-version-control.md](../evidencias/evidencia-01-git-version-control.md).

---

## 2. Exploración de la Terminal Linux (WSL)

* **Entorno:** Ubuntu sobre WSL 2 (Windows 11).
* **Objetivo:** Poner en práctica los comandos fundamentales del Shell de Unix:
  1. Navegación e inspección de directorios (`pwd`, `ls -la`, `cd`).
  2. Creación y lectura de archivos (`echo >`, `cat`).
  3. Estructuración y reubicación de contenidos (`mkdir`, `mv`).
  4. Inspección del árbol de directorios resultante mediante `tree`.
* **Evidencia formal:** Ver [evidencia-02-exploracion-terminal.md](../evidencias/evidencia-02-exploracion-terminal.md).

---

## 3. Fundamentos de Python para Análisis de Datos (Jupyter Notebook)

* **Cuaderno interactivo:** [03-analisis-datos.ipynb](./03-analisis-datos.ipynb)
* **Dataset clínico:** Archivos CSV en [`./data/`](./data/) (`inflammation-01.csv` a `inflammation-12.csv`).
* **Objetivo:** Implementar un flujo completo de análisis de datos científicos con **NumPy** y **Matplotlib**:
  1. Carga de datos matriciales en memoria continua mediante `np.loadtxt`.
  2. Rebanado bidimensional (`data[filas, columnas]`) y agregación estadística por ejes (`axis=0` colapso de pacientes, `axis=1` colapso de días).
  3. Visualización técnica: mapas de calor (`imshow`), curvas temporales con escalones ortogonales (`step`), calibración de grilla y subplots en tríptico.
  4. Detección forense de anomalías mediante derivadas discretas (`np.diff`) y automatización por lotes con la librería `glob`.
* **Evidencia formal:** Ver [evidencia-03-python-data-analysis.md](../evidencias/evidencia-03-python-data-analysis.md).

