# Ejercicio 3 — Arquitectura del Proyecto nanoaod-schema-linter y Revisión de Pull Requests

* **Recursos de referencia:**
  * [GitHub Skills — Review Pull Requests](https://github.com/skills/review-pull-requests)
  * [CMS Open Data Analyses (GitHub Organization)](https://github.com/cms-opendata-analyses)
  * [Repositorio cern-preparation-program](https://github.com/Klopezxd/cern-preparation-program)
* **Fecha:** 16 de octubre de 2026
* **Estudiante:** Klever López (Ingeniería en Tecnologías de la Información)
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 7)

---

## 1. Síntesis Metodológica: Del Hackathon a la Arquitectura Propia

Al examinar los repositorios del **CMS Open Data Hackathon** y las guías de **GitHub Skills (Review Pull Requests)**, se evidencia que los proyectos científicos de software deben resolver dos frentes simultáneos:
1. **La arquitectura interna del repositorio:** Desacoplar código fuente, datos de prueba, especificaciones de entorno y automatizaciones.
2. **El protocolo de integración continua:** Proteger la rama principal (`main`) mediante revisiones obligatorias de código por pares (*peer review*) y compuertas automáticas de CI.

En este ejercicio se traslada directamente ese modelo organizativo para definir la estructura técnica de **`nanoaod-schema-linter`**.

---

## 2. Desglose Estructural de nanoaod-schema-linter

### 1. Problema o necesidad que aborda
Resuelve la alta tasa de fallos en pipelines de computación científica del CERN debida a datos corruptos, árboles vacíos o cambios de nombre y tipo de variables entre campañas de CMS Open Data (ej. 2012 vs. 2016). Proporciona una herramienta de validación previa (*pre-flight validation*) de bajo consumo de recursos.

### 2. Papel de los datos y recursos técnicos
* **Datos (Insumo):** Archivos binarios ROOT (formato NanoAOD) provenientes del portal CERN Open Data.
* **Recursos técnicos (Herramientas):** Uproot para introspección ultrarrápida de cabeceras en memoria RAM, esquemas declarativos en YAML/JSON que definen contratos de datos, y Docker para aislar el entorno de ejecución.

### 3. Organización modular del repositorio
```text
nanoaod-schema-linter/
├── .github/workflows/    # CI: linting con ruff y pruebas con pytest
├── schemas/              # Contratos declarativos YAML (ej. cms_2016_dimuon.yaml)
├── src/                  # Módulos: parser de cabeceras, validador de conjuntos y CLI
├── tests/                # Datasets sintéticos válidos y corruptos para testeo
├── Dockerfile            # Imagen reproducible python:3.11-slim (< 200 MB)
└── requirements.txt      # Fijación estricta de dependencias (uproot, pyyaml)
```

### 4. Documentación y reproducibilidad
Sin documentación ejecutable, el software queda obsoleto rápidamente. Un `README.md` exhaustivo con ejemplos claros de CLI (`nanoaod-linter --schema schemas/2016.yaml --input data/*.root`) sumado a una imagen Docker reproducible garantiza que cualquier físico o evaluador pueda correr la herramienta con idéntico comportamiento en cualquier distribución de Linux.

### 5. Función de la revisión de Pull Requests
Permite que el equipo (desarrollador de TI, analista de datos y devops) incorpore nuevos contratos de esquemas o refactorizaciones de código mediante revisiones línea por línea en el *diff*, asegurando que ningún cambio degrade el rendimiento de lectura de cabeceras ni rompa los tests existentes.

### 6. Práctica aplicada en proyectos propios
Configuración de **Branch Protection Rules** en `main`, **Pull Request Templates** con lista de verificación (tests en verde, tipado verificado, linter sin alertas) y fusión restringida exclusivamente tras aprobación técnica formal.
