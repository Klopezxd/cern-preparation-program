# Evidencia 3 — Análisis de la Estructura de un Proyecto Técnico

* **Módulo:** [3.1 Introducción al desarrollo de proyectos](https://github.com/skills/review-pull-requests) | **Fecha:** 16 de octubre de 2026
* **Estudiante:** Klever López (4.º semestre, Ingeniería en Tecnologías de la Información)
* **Institución:** Universidad de las Fuerzas Armadas – ESPE
* **Docente / Coordinadora:** Ing. Tatiana Gualotuña
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 7)

> **Objetivo:** Analizar de manera rigurosa la organización arquitectónica, gestión de datos, documentación, reproducibilidad y flujo de integración colaborativa mediante Pull Requests para el proyecto tecnológico `nanoaod-schema-linter`, contrastando su diseño técnico con las directivas observadas en los repositorios oficiales de CMS Open Data Analyses y en la plataforma GitHub Skills.

---

## 1. Referencias y Marco de Evaluación Técnica

1. **Recurso de Colaboración y Calidad de Código:**
   * *Recurso Oficial:* [GitHub Skills — Review Pull Requests](https://github.com/skills/review-pull-requests)
   * *Evidencia observada:* Flujos de trabajo basados en ramas secundarias (*feature branches*), revisión contextual línea a línea en el *diff*, hilos de discusión técnica entre colaboradores y compuertas automáticas de aprobación previa a la fusión (*merge*).
2. **Repositorio de Referencia en Computación Científica:**
   * *Recurso Oficial:* [CMS Open Data Analyses (GitHub Organization)](https://github.com/cms-opendata-analyses) y [CMS Open Data Workshops](https://github.com/cms-opendata-workshop)
   * *Evidencia observada:* Estructuras desacopladas para análisis de datos masivos del CERN, uso de especificaciones reproducibles en Docker y validación continua en GitHub Actions.
3. **Proyecto Técnico Propio Analizado:**
   * *Iniciativa:* **`nanoaod-schema-linter`** (validador de esquemas e integridad para CMS Open Data planificado en la Evidencia 1).

---

## 2. Desarrollo del Análisis Estructurado

### 2.1 Problema o necesidad que aborda el proyecto
En el ecosistema de computación científica del CERN, los investigadores procesan conjuntos de datos extensos (formato NanoAOD) provenientes de diversas campañas de colisiones. Un problema recurrente y costoso es que los trabajos de análisis que tardan horas en ejecutarse suelen fallar a mitad de proceso debido a:
* Archivos binarios ROOT corruptos o truncados por descargas incompletas.
* Árboles con cero eventos.
* Variaciones en los nombres o tipos de ramas físicas (`dtype`) entre versiones de NanoAOD (ej. diferencias entre las producciones de 2012 y 2016).

**`nanoaod-schema-linter`** aborda esta necesidad directa proporcionando una herramienta de consola (CLI) de validación previa (*pre-flight validation*) que inspecciona cientos de archivos en segundos y certifica su conformidad antes de lanzar pipelines pesados de cómputo.

---

### 2.2 Papel de los datos y de los recursos técnicos
En `nanoaod-schema-linter`, los datos y recursos técnicos interactúan de forma desacoplada:
* **Los datos analizados (Insumo):** Archivos `.root` de CMS Open Data alojados localmente o consultados remotamente. La herramienta únicamente inspecciona los metadatos de las cabeceras del árbol `Events` mediante `uproot`, sin volcar las colisiones a memoria RAM.
* **Contratos declarativos (Esquemas):** Archivos YAML legibles por humanos (ej. `schemas/cms_2016_dimuon.yaml`) donde el físico define las ramas obligatorias y tipos requeridos.
* **Recursos técnicos (Infraestructura):** Un entorno de ejecución encapsulado en Docker (`python:3.11-slim`) con dependencias estrictas (`uproot`, `pyyaml`), permitiendo validar datos en estaciones convencionales sin necesidad de instalar la pesada infraestructura institucional de CMSSW.

---

### 2.3 Cómo ayuda el repositorio a organizar el trabajo
El repositorio en Git opera como la **fuente única de verdad (*Single Source of Truth*)**, organizando la herramienta en módulos con responsabilidades claras:
* `schemas/`: Directorio centralizado de contratos de datos para diferentes campañas del CERN.
* `src/`: Código fuente desacoplado (módulo de introspección de cabeceras, motor de validación de conjuntos de claves y formateador de consola CLI).
* `tests/`: Batería de pruebas unitarias y datasets ROOT sintéticos (válidos, vacíos y deliberadamente corruptos).
* `.github/workflows/`: Automatización de linting con `ruff` y ejecución de tests con `pytest` ante cada evento de cambio.
* **Gestión colaborativa:** Uso de *Issues* para rastrear incompatibilidades de esquemas reportadas por usuarios y *Milestones* alineados a los sprints de desarrollo.

---

### 2.4 Importancia de la documentación y la reproducibilidad
Para una herramienta de aseguramiento de calidad de datos, la reproducibilidad y la documentación técnica no son opcionales:
* **Guía operativa ejecutable:** Un `README.md` exhaustivo debe documentar con precisión los comandos CLI (ej. `nanoaod-linter --schema schemas/2016.yaml --input data/*.root`), la interpretación de los códigos de salida POSIX (`exit 0`, `1` o `2`) y la integración en scripts de automatización.
* **Eliminación de la degradación de dependencias:** El uso de Docker garantiza que dentro de cinco o diez años cualquier estudiante o investigador pueda validar exactamente los mismos archivos NanoAOD con idéntico comportamiento, mitigando la obsolescencia de librerías.

---

### 2.5 Función de la revisión de Pull Requests en el equipo de desarrollo
Conforme a las directivas prácticas aprendidas en *GitHub Skills: Review Pull Requests*, el flujo de PRs cumple un rol determinante en `nanoaod-schema-linter`:
1. **Control de calidad e integridad (*Peer Review*):** Cuando un colaborador propone un nuevo esquema de campaña o modifica el motor de lectura, la revisión de PR permite auditar el *diff* línea por línea para asegurar que no se introduzcan fugas de memoria ni lecturas masivas a RAM.
2. **Validación automática obligatoria:** Todo PR dispara los flujos de integración continua en GitHub Actions; si los tests de validación sobre archivos corruptos fallan, el código no puede fusionarse.
3. **Discusión técnica contextualizada:** Permite que el líder técnico y el analista de datos discutan mejoras de sintaxis o sugieran cambios directos (*Suggested changes*) dentro de la propia plataforma de GitHub antes de autorizar el *merge* a la rama `main`.

---

### 2.6 Práctica aplicable a proyectos propios
* **Práctica seleccionada:** **Reglas estrictas de protección de ramas (*Branch Protection Rules*) combinadas con plantillas estructuradas de Pull Request (*PR Templates*) y validación continua automatizada.**
* **Aplicación directa en mis proyectos:** En el repositorio del programa ([`cern-preparation-program`](https://github.com/Klopezxd/cern-preparation-program)) y en la implementación de `nanoaod-schema-linter`, se protegerá la rama `main` bloqueando los commits directos. Todo incremento exigirá una rama secundaria (`feature/*`), una plantilla de PR con lista de verificación obligatoria (¿se ejecutó el linter?, ¿pasan los tests?, ¿se actualizó el README?) y aprobación técnica formal antes de la fusión.

---

## 3. Síntesis para Entrega en Plataforma Moodle

```html
<p><strong>Problema y necesidad:</strong> En CMS Open Data, los análisis científicos suelen fallar tras horas de ejecución debido a archivos ROOT corruptos, árboles vacíos o cambios de nombres de ramas entre campañas. El proyecto <em>nanoaod-schema-linter</em> aborda esta problemática proporcionando una herramienta CLI rápida de validación previa (pre-flight validation) para certificar la integridad de los datos antes de lanzar pipelines pesados.</p>

<p><strong>Papel de los datos y recursos técnicos:</strong> Los archivos ROOT NanoAOD son el insumo primario que se inspecciona únicamente a nivel de cabecera con Uproot sin volcar eventos a RAM. Los esquemas declarativos YAML actúan como contratos de datos donde se definen las ramas requeridas, mientras que Docker estandariza el entorno de ejecución en hardware convencional sin depender de CMSSW.</p>

<p><strong>Organización del repositorio:</strong> El repositorio opera como fuente única de verdad, desacoplando esquemas declarativos (<code>schemas/</code>), lógica del CLI (<code>src/</code>), datasets de prueba (<code>tests/</code>) y flujos de automatización (<code>.github/workflows/</code>), permitiendo trazabilidad histórica y desarrollo colaborativo seguro.</p>

<p><strong>Documentación y reproducibilidad:</strong> En herramientas de aseguramiento de calidad, la documentación clara de comandos CLI y códigos de salida POSIX (exit 0, 1, 2) junto con contenedores Docker congelados garantiza que cualquier investigador pueda replicar idénticas validaciones en cualquier entorno sin degradación por dependencias.</p>

<p><strong>Revisión de Pull Requests:</strong> Siguiendo el estándar de GitHub Skills (<a href="https://github.com/skills/review-pull-requests" target="_blank">Review Pull Requests</a>), los PRs aseguran el control de calidad mediante revisión de diffs línea a línea, ejecución obligatoria de pruebas en CI y discusión técnica antes de fusionar nuevos esquemas o código a la rama main.</p>

<p><strong>Práctica aplicable a proyectos propios:</strong> Implementaré reglas de protección en main con plantillas obligatorias de PR y checks automáticos en GitHub Actions tanto en cern-preparation-program como en nanoaod-schema-linter para blindar la estabilidad del código.</p>
```
