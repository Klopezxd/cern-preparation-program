# Evidencia 1 — Exploración de ROOT y CMS NanoAOD

* **Módulo:** [1.1 ROOT y Python para análisis de datos](https://cms-opendata-workshop.github.io/workshop2024-lesson-cpp-root-python/instructor/) & [1.2 Explorando CMS NanoAOD](https://cms-opendata-workshop.github.io/workshop2024-lesson-exploring-cms-nanoaod/instructor/) | **Fecha:** 18 de septiembre de 2026

> **Objetivo:** Explorar la estructura interna de los archivos ROOT y datasets CMS NanoAOD, analizando la transición técnica desde el entorno clásico C++ hacia el ecosistema moderno Scikit-HEP (`uproot` y `awkward-array`), manipulando arreglos irregulares (*jagged arrays*) y reconstruyendo la masa invariante del Bosón Z a partir de datos reales de colisiones del LHC.

---

## 1. Entorno de Ejecución y Validación de Reproducibilidad

Siguiendo las directivas del taller oficial del CERN, se implementó una estrategia dual de ejecución validando la reproducibilidad científica tanto en contenedores como en entornos locales:

1. **Entorno Contenerizado (Docker sobre WSL2 Ubuntu):**
   * **Imagen oficial:** `gitlab-registry.cern.ch/cms-cloud/root-vnc:latest` desplegada mediante Docker Engine nativo.
   * **Bind mount:** Mapeo de volumen bidireccional host-contenedor (`-v .../semana-03:/code`) para garantizar la persistencia física de artefactos y código en el sistema de archivos del host.
   * **Servidor gráfico:** Despliegue de servidor **noVNC** (puerto `6080`) para acceder a interfaces interactivas X11 (`TBrowser`, renderizado de histogramas en `TCanvas`) directamente a través de un navegador web sin requerir servidores X adicionales en Windows.
2. **Entorno Científico Moderno (Scikit-HEP Nativo en Python 3.12):**
   * Para el análisis ágil, se adoptó el stack estándar de la comunidad científica: `uproot` (v5.7.6), `awkward` (v2.13.0), `vector` (v1.8.1) y `matplotlib` (v3.11.2), eliminando la dependencia de compiladores C++ y entornos virtuales pesados en tareas interactivas.

---

## 2. Inspección del Formato ROOT y Acceso Columnar

Se analizó el dataset oficial de colisiones `SMHiggsToZZTo4L.root` (42.4 MB) publicado en el **CERN Open Data Portal**:

* **Estructura Interna (`TFile`):** El archivo opera como una jerarquía estructurada de objetos indexados mediante claves (`f.keys()`), alojando el árbol tabular maestro de colisiones denominado `Events;1`.
* **Volumen Experimental:** La tabla aloja un total de **299.973 colisiones** (`events.num_entries`), donde cada fila representa un evento temporalmente delimitado de cruce de haces en el LHC.
* **Acceso Columnar:** A diferencia de formatos orientados a filas (como CSV o bases de datos relacionales estándar), `uproot` permite la lectura diferida y selectiva (*lazy loading*) de ramas específicas (`TBranch`), transfiriendo a memoria únicamente los bytes correspondientes a las variables de interés (`nMuon`, `Muon_pt`, etc.).

---

## 3. Manejo de Arreglos Irregulares (*Jagged Arrays*)

En colisiones de partículas de alta energía, la multiplicidad de partículas salientes es intrínsecamente variable: cada evento produce un número arbitrario de muones o electrones.

* **Limitación de NumPy:** Las matrices estándar de `NumPy` exigen dimensiones rectangulares homogéneas ($N \times M$). Al procesar listas de diferente longitud, NumPy degrada la matriz a un arreglo genérico de objetos Python (`dtype=object`), provocando que operaciones aritméticas escalares (ej. `2 * pt`) dupliquen los elementos de las listas en lugar de operar matemáticamente los valores numéricos.
* **Solución mediante Awkward Array:** La estructura `ak.Array` separa el buffer de datos continuos en memoria de una tabla de índices y desplazamientos (*offsets*). Esto genera el tipo estructural `N * var * float64`, permitiendo operaciones vectorizadas a velocidad de C++ compilado sobre datos heterogéneos sin desperdicio de memoria ni bucles explícitos.
* **Correspondencia Escalar-Vectorial:** Se verificó que la rama escalar `nMuon` coincide con la longitud de cada subarreglo en la rama vectorial `Muon_pt` (ej. para los primeros 5 eventos: `nMuon = [3, 0, 0, 7, 0]` $\leftrightarrow$ `Muon_pt = [[63.0, 38.1, 4.05], [], [], [54.3, 23.5, ...], []]`).

---

## 4. Reconstrucción Relativista y Masa Invariante

Para aislar el decaimiento del **Bosón Z** en pares de muones ($Z \to \mu^+\mu^-$), se aplicó el siguiente pipeline analítico:

1. **Corte Cinemático Booleano:** Filtrado de eventos con multiplicidad mínima de dos muones (`nMuon >= 2`), aislando **145.597 colisiones candidatas** (48.54% del total).
2. **Construcción de Cuadrivectores:** Se estructuraron los momentos de Lorentz utilizando la librería `vector` en coordenadas cilíndricas del detector CMS:
   $$(p_T, \eta, \phi, m)$$
   donde $p_T$ es el momento transversal, $\eta$ la pseudorapidez polar, $\phi$ el ángulo azimutal y $m \approx 0.10566 \text{ GeV}$ la masa en reposo del muón.
3. **Suma de Cuadrimomentos y Masa Invariante:**
   $$P_{\text{total}} = P_{\mu 1} + P_{\mu 2}$$
   $$M_{\mu\mu} = \sqrt{P_{\text{total}} \cdot P_{\text{total}}} = \sqrt{(E_1 + E_2)^2 - |\vec{p}_1 + \vec{p}_2|^2}$$
4. **Resonancia Experimental:** El espectro de masa invariante exhibe un pico centrado en **91.2 GeV**, consistente con el valor de la literatura científica para el Bosón Z ($M_Z = 91.1876 \pm 0.0021 \text{ GeV}$), descrito por una distribución de Breit-Wigner superpuesta sobre un continuo de ruido Drell-Yan.

---

## 5. Respuestas al Cuestionario de Evaluación Oficial

### 1. ROOT
**¿Qué función cumple ROOT dentro del análisis de datos de física de partículas?**  
ROOT es el software estándar del CERN para almacenamiento masivo, procesamiento estadístico y visualización de datos experimentales. Proporciona el formato binario comprimido `TTree` que permite almacenar petabytes de colisiones con estructura columnar, facilitando lecturas selectivas de datos sin decodificar archivos completos.

### 2. Python
**¿Qué ventajas observas al utilizar Python para trabajar con archivos ROOT?**  
Permite desacoplar el análisis de los entornos C++ monolíticos mediante librerías modernas de Scikit-HEP (`uproot`, `awkward`, `vector`). Facilita el desarrollo interactivo en Jupyter Notebooks, integración nativa con el ecosistema de ciencia de datos (`NumPy`, `Matplotlib`, `Pandas`) y ejecución vectorizada sin compilaciones manuales ni dependencias de sistema complejas.

### 3. NanoAOD
**¿Qué es NanoAOD y qué tipo de información puede contener?**  
Es el formato de datos más compacto y optimizado del experimento CMS (~1–2 kB por colisión). Contiene parámetros físicos ya calibrados y reconstruidos (número de partículas, cinemática $p_T, \eta, \phi, m$, carga eléctrica, calidad de identificación y aislamiento) almacenados exclusivamente como tipos de datos primitivos (`float`, `int`, `bool`).

### 4. NanoAOD vs. MiniAOD
**Menciona una diferencia que hayas identificado entre ambos formatos.**  
MiniAOD almacena objetos C++ complejos (`pat::Muon`, `pat::Electron`) que requieren el framework CMSSW (~30–50 kB/evento), mientras que NanoAOD aplana toda la información en tablas de tipos primitivos independientes de software CMS, permitiendo su análisis directo en Python puro sin contenedores especiales.

### 5. Aplicación
**Imagina que tienes que analizar una gran cantidad de eventos registrados por CMS. ¿Por qué podría ser útil utilizar NanoAOD y herramientas como Python/ROOT?**  
Porque reduce drásticamente los requerimientos de hardware: el tamaño reducido de NanoAOD ahorra ancho de banda y almacenamiento, mientras que `uproot` lee únicamente las columnas requeridas en memoria RAM. Esto permite procesar cientos de miles de eventos en segundos en laptops ordinarias o recursos cloud mediante vectorización nativa.

### 6. Reflexión Conceptual
**¿Qué parte de la actividad te resultó más difícil de comprender?**  
El concepto y manipulación de los **arreglos irregulares (*jagged arrays*)**: asimilar la razón por la cual las matrices rectangulares clásicas de NumPy fallan al operar choques con multiplicidad variable de partículas y cómo `awkward` administra los punteros y offsets en memoria para realizar cálculos vectorizados sin aplanar destructivamente las dimensiones.

---

## 6. Recursos y Enlaces a Entregables

* **Cuaderno Interactivo Ejecutado:** [`01-exploracion-root-nanoaod.ipynb`](../ejercicios/01-exploracion-root-nanoaod.ipynb) (todas las celdas ejecutadas con salidas y gráficos embebidos).
* **Gráfico del Espectro Dimuón:** [`dimuon_spectrum.png`](../ejercicios/dimuon_spectrum.png) generado y guardado a 150 DPI.
* **Repositorio Oficial en GitHub:** [Klopezxd/cern-preparation-program](https://github.com/Klopezxd/cern-preparation-program/tree/main/semana-03)
