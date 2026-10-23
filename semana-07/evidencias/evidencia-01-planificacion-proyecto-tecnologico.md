# Evidencia 1 — Planificación Inicial de un Proyecto Tecnológico

* **Módulo:** [1.1 Planificación inicial de un proyecto tecnológico](https://www.atlassian.com/es/agile/project-management/project-roadmap) | **Fecha:** 12 de octubre de 2026
* **Estudiante:** Klever López (4.º semestre, Ingeniería en Tecnologías de la Información)
* **Institución:** Universidad de las Fuerzas Armadas – ESPE
* **Docente / Coordinadora:** Ing. Tatiana Gualotuña
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 7)

> **Objetivo:** Formular la planificación inicial de una herramienta de software de infraestructura y aseguramiento de calidad de datos (*developer tooling*) para el ecosistema de CMS Open Data del CERN, aplicando los fundamentos ágiles y hojas de ruta (*project roadmaps*) de Atlassian para estructurar objetivos, alcance, hitos verificables, asignación de responsabilidades, gestión de riesgos y cronograma por sprints sin requerir conocimientos de física teórica.

---

## 1. Ficha Técnica y Planificación Inicial del Proyecto

### 1.1 Nombre del Proyecto
**nanoaod-schema-linter: Validador de Esquemas e Integridad de Archivos ROOT para CMS Open Data**

---

### 1.2 Objetivo del Proyecto
Diseñar e implementar una herramienta de línea de comandos (CLI) ligera, rápida y reproducible en Python para validar la integridad estructural y la conformidad de esquemas de datos en archivos ROOT (formato NanoAOD) provenientes del portal CMS Open Data antes de su ejecución en pipelines de análisis científico, previniendo fallos en tiempo de ejecución debidos a archivos truncados, ramas faltantes o discrepancias de tipado.

---

### 1.3 Alcance (*Scope*)

* **Incluido en el proyecto (*In-Scope*):**
  1. **Introspección ultrarrápida de cabeceras:** Inspección directa de árboles `Events` mediante la librería `uproot` sin cargar eventos ni datos numéricos a memoria RAM.
  2. **Contratos declarativos de esquema:** Definición de esquemas de validación legibles en archivos YAML o JSON que especifican ramas obligatorias y tipos de datos esperados (`dtype`).
  3. **Comprobación defensiva de integridad:** Detección de archivos binarios ROOT corruptos, árboles vacíos (cero eventos) o descargas incompletas.
  4. **Reportes estructurados por consola:** Resumen legible en terminal indicando ramas conformes, ausentes o con tipos incompatibles, y exportación de reportes en JSON.
  5. **Códigos de retorno estándar POSIX:** Emisión de códigos de salida (`0` = conforme, `1` = error de esquema, `2` = archivo corrupto) para integración en pipelines de CI/CD y scripts de bash.
  6. **Contenedorización reproducible:** Imagen Docker ultraligera basada en `python:3.11-slim` (< 200 MB) con dependencias mínimas congeladas.

* **Excluido del proyecto (*Out-of-Scope*):**
  1. Cálculos de física de partículas, análisis cinemático o filtrado de eventos (la herramienta se enfoca exclusivamente en la integridad y el esquema de los datos).
  2. Desarrollo de interfaces gráficas complejas (GUI) o paneles web interactivos.
  3. Reparación o reconstrucción automática de bytes dañados dentro de los archivos ROOT.
  4. Compatibilidad con formatos legados u oscuros de ROOT anteriores a la versión 6.

---

### 1.4 Hitos Principales (*Milestones*)

* **Hito 1 — Introspección de Cabeceras y Lector de Esquemas (Semana 1):**
  * *Entregable:* Script base capaz de inspeccionar los nombres de ramas y metadatos de un archivo NanoAOD en menos de 0.5 segundos y cargar un contrato de esquema en formato YAML.
* **Hito 2 — Motor de Validación y Códigos de Salida POSIX (Semana 2):**
  * *Entregable:* Algoritmo de comparación de conjuntos de ramas y comprobación de tipos `dtype`, emitiendo reportes legibles en terminal y códigos de salida estándar para scripts de automatización.
* **Hito 3 — Validación por Lotes, Docker y Pruebas Continuas (Semana 4):**
  * *Entregable:* Procesamiento concurrente de directorios con múltiples archivos `.root`, imagen Docker optimizada y flujo de GitHub Actions con pruebas automáticas frente a archivos deliberadamente alterados.

---

### 1.5 Asignación de Responsabilidades y Roles

| Rol en el Proyecto | Miembro Asignado | Responsabilidades Principales |
| :--- | :--- | :--- |
| **Líder Técnico & Desarrollador de Software** | Klever López | Diseño de la arquitectura del CLI en Python, integración de `uproot` para lectura de cabeceras de bajo consumo, lógica de validación de esquemas, manejo de argumentos y Dockerfile. |
| **Analista de Datos & Usuario Científico** | Colaborador 1 (Colaboración externa) | Redacción de los esquemas YAML de referencia para las campañas oficiales de CMS Open Data (ej. 2012 y 2016) y suministro de archivos de prueba válidos y corruptos. |
| **Ingeniero DevOps & Aseguramiento de Calidad (QA)** | Colaborador 2 (Colaboración externa) | Automatización de pruebas unitarias con `pytest` en GitHub Actions, pruebas de estrés y concurrencia en Linux/WSL2 y control de calidad de código. |

---

### 1.6 Análisis y Mitigación de Riesgos

1. **Riesgo 1: Tiempos excesivos de I/O al verificar directorios con cientos de archivos ROOT.**
   * *Probabilidad:* Alta | *Impacto:* Moderado.
   * *Descripción:* Escanear secuencialmente directorios grandes puede ralentizar los pipelines de análisis previos a la ejecución.
   * *Estrategia de Mitigación:* Implementar concurrencia mediante hilos ligeros (`concurrent.futures.ThreadPoolExecutor`) y restringir la lectura estrictamente a los metadatos de cabecera con `object_cache=None`.

2. **Riesgo 2: Variaciones en los nombres de tipos de datos entre versiones de Uproot y tipos primitivos de ROOT/NumPy.**
   * *Probabilidad:* Media | *Impacto:* Moderado.
   * *Descripción:* Discrepancias sintácticas (ej. `float32` vs. `Float_t`) pueden generar falsos positivos en la validación de tipos.
   * *Estrategia de Mitigación:* Construir una capa interna de normalización de firmas de datos que homologue los tipos de ROOT a primitivos estándar de Python/NumPy antes de ejecutar la comparación.

3. **Riesgo 3: Archivos truncados o corruptos que interrumpan la ejecución global del lote con excepciones no controladas.**
   * *Probabilidad:* Alta | *Impacto:* Crítico.
   * *Descripción:* Si un archivo binario está dañado, `uproot.open` puede generar errores de lectura que aborten todo el proceso.
   * *Estrategia de Mitigación:* Implementar un bloque de manejo defensivo de excepciones (`try/except`) que capture fallos de deserialización, categorice el archivo como "Corrupto" y continúe procesando el resto del lote sin abortar.

---

### 1.7 Hoja de Ruta (*Project Roadmap*) Secuencial

El proyecto se planifica en cuatro sprints semanales bajo una metodología iterativa e incremental:

```text
+---------------------------------------------------------------------------------------+
| SPRINT 1: INTROSPECCIÓN DE CABECERAS Y ESQUEMAS YAML (Semana 1)                       |
| • Spike técnico con Uproot: lectura de cabeceras vs. carga de eventos en RAM.        |
| • Diseño del formato declarativo del archivo schema.yaml.                             |
| • Parser inicial de argumentos de línea de comandos (argparse).                       |
+---------------------------------------------------------------------------------------+
                                           │
                                           ▼
+---------------------------------------------------------------------------------------+
| SPRINT 2: MOTOR DE VALIDACIÓN Y CÓDIGOS DE RETORNO POSIX (Semana 2)                   |
| • Implementación de validación de conjuntos (ramas requeridas vs. existentes).        |
| • Rutina de comprobación de compatibilidad de tipos (dtype matching).                |
| • Emisión de códigos de salida POSIX estándar (exit 0, 1, 2) y mensajes en consola.   |
+---------------------------------------------------------------------------------------+
                                           │
                                           ▼
+---------------------------------------------------------------------------------------+
| SPRINT 3: PROCESAMIENTO CONCURRENTE POR LOTES Y REPORTES JSON (Semana 3)              |
| • Escaneo recursivo de directorios con ThreadPoolExecutor.                            |
| • Exportación estructurada de resultados a formato JSON para integración con CI/CD.   |
| • Manejo defensivo robusto de excepciones para archivos truncados.                    |
+---------------------------------------------------------------------------------------+
                                           │
                                           ▼
+---------------------------------------------------------------------------------------+
| SPRINT 4: INTEGRACIÓN CONTINUA, DOCKERIZACIÓN Y DOCUMENTACIÓN (Semana 4)              |
| • Creación de tests unitarios automáticos con pytest y datasets de prueba sintéticos.  |
| • Configuración del pipeline de GitHub Actions para ejecución continua.               |
| • Empaquetado en imagen Docker ultraligera (< 200 MB) y documentación técnica final.  |
+---------------------------------------------------------------------------------------+
```

---

## 2. Texto en Línea para Entrega en Plataforma Moodle

```html
<p><strong>Nombre del proyecto:</strong> nanoaod-schema-linter: Validador de Esquemas e Integridad de Archivos ROOT para CMS Open Data.</p>

<p><strong>Objetivo:</strong> Diseñar e implementar una herramienta de línea de comandos (CLI) ligera, rápida y reproducible en Python para validar la integridad estructural y la conformidad de esquemas de datos en archivos ROOT (formato NanoAOD) provenientes de CMS Open Data antes de su procesamiento en pipelines de análisis científico, previniendo fallos en tiempo de ejecución debidos a archivos truncados, ramas faltantes o discrepancias de tipado.</p>

<p><strong>Alcance:</strong> <em>Incluye:</em> Introspección ultrarrápida de cabeceras ROOT con Uproot sin cargar datos a memoria, definición de contratos de esquema declarativos en formato YAML, detección de archivos corruptos o vacíos, reportes en consola con códigos de retorno estándar POSIX (exit 0, 1, 2), procesamiento concurrente por lotes en directorios locales y empaquetado en contenedor Docker ultraligero (< 200 MB). <em>Excluye:</em> Cálculos físicos o cinemáticos de partículas, interfaces gráficas complejas (GUI), reparación automática de archivos dañados y formatos legados anteriores a ROOT 6.</p>

<p><strong>Hitos principales:</strong> 1) Introspección de cabeceras y lectura de esquemas YAML en menos de 0.5 segundos por archivo; 2) Motor de validación de conjuntos de ramas y tipos de datos emitiendo códigos POSIX para automatización; 3) Validación concurrente por lotes, contenedor Docker optimizado y pruebas continuas en GitHub Actions.</p>

<p><strong>Asignación de responsabilidades:</strong> <em>Klever López (Líder Técnico):</em> arquitectura del software en Python, integración de Uproot para lectura eficiente de cabeceras, lógica de validación de esquemas, CLI y Dockerfile. <em>Colaborador 1 (Analista de Datos):</em> redacción de esquemas YAML de referencia para campañas de CMS y provisión de datasets de prueba. <em>Colaborador 2 (DevOps/QA):</em> pruebas unitarias con Pytest en GitHub Actions, pruebas de concurrencia y profiling en Linux/WSL2.</p>

<p><strong>Riesgos y mitigación:</strong> 1) <em>Lentitud de I/O en lotes grandes:</em> mitigado con procesamiento concurrente multi-hilo y lectura restringida a metadatos; 2) <em>Incompatibilidad sintáctica de tipos de datos:</em> mitigado con una capa interna de normalización de firmas de ROOT a primitivos de NumPy/Python; 3) <em>Archivos corruptos que aborten el proceso:</em> mitigado mediante manejo defensivo de excepciones registrando fallos sin detener el lote.</p>

<p><strong>Roadmap temporal:</strong> Organizado en cuatro sprints: Sprint 1 (introspección de cabeceras y esquemas YAML); Sprint 2 (motor de validación y códigos POSIX); Sprint 3 (validación concurrente por lotes y exportación JSON); y Sprint 4 (pruebas en GitHub Actions, contenedor Docker y cierre de documentación técnica).</p>
```
