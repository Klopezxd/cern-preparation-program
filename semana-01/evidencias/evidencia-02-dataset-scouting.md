# Evidencia 2 — Exploración de un dataset CMS

* **Módulo:** [2.1 Finding & Using Open Data — Dataset Scouting](https://cms-opendata-workshop.github.io/workshopqcd-2024-lesson-dataset-scouting/) | **Fecha:** 2 de septiembre de 2026

> **Objetivo:** Identificar y documentar un dataset de interés en el portal de CMS Open Data, analizando su identificador oficial, el tipo de información que almacena, su relevancia técnica, su posible utilidad y las dificultades de comprensión documental.

---

### 1. Nombre del dataset
* **Nombre:** `Run2012B_DoubleMuParked dataset in reduced NanoAOD format for education and outreach`
* **Identificador / Enlace:** [CERN Open Data - Record 12365](https://opendata.cern.ch/record/12365) (DOI: `10.7483/OPENDATA.CMS.04XV.ESBR`)
* **Experimento:** CMS (CERN).

---

### 2. Tipo de información
Contiene datos reales de colisiones del detector CMS tomadas en 2012 a 8 TeV, filtrados para eventos donde se detectaron al menos dos muones.

A diferencia del dataset de investigación crudo, esta versión está simplificada y en formato tabular (NanoAOD): se eliminaron los datos internos del detector y solo se guardaron las propiedades esenciales de los muones (momento, coordenadas espaciales y carga eléctrica) en un único archivo de ~3 GB.

---

### 3. ¿Qué te llamó la atención?
Me llamó la atención el contraste en la gestión de datos: el dataset original (AOD) pesa casi 8 Terabytes distribuidos en más de 2,200 archivos y requiere software especializado del CERN, mientras que esta versión reducida condensa los mismos eventos en un solo archivo de 3 GB pensado para educación. Esto permite que estudiantes que no venimos de la carrera de física podamos explorar datos reales del LHC sin colapsar el almacenamiento de nuestra computadora.

---

### 4. Posible utilidad
Este dataset es un caso de estudio ideal para prácticas de ciencia de datos e ingeniería de la información: permite trabajar con millones de registros reales para aplicar pipelines de procesamiento (ETL), filtrado y limpieza de datos tabulares a gran escala, usando librerías como `pandas`, `uproot` y `matplotlib` para generar histogramas y distribuciones estadísticas de variables continuas, todo sin depender de software especializado de física de partículas.

---

### 5. Dificultad encontrada
La mayor dificultad fue la sobrecarga de vocabulario técnico de física y la nomenclatura interna del CERN. Al inicio fue abrumador entender por qué existían tantas versiones del mismo dataset con nombres crípticos y acrónimos como RAW, AOD, triggers o HLT, hasta que comprendí que representan diferentes niveles de procesamiento y compresión de los datos.
