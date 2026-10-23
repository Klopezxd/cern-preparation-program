# Ejercicio 2 — Registro de Avances e Incidencias Técnicas

* **Fecha:** 14 de octubre de 2026
* **Estudiante:** Klever López (Ingeniería en Tecnologías de la Información)
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 7)

---

## 1. Bitácora de Sesión y Avance

* **Contexto de trabajo:** Sesión de trabajo autónomo enfocada en la planificación técnica de proyectos y registro de incidencias (Semana 7).
* **Actividades ejecutadas:**
  * Revisión y síntesis de los recursos de Atlassian (*Agile Fundamentals* y *Project Roadmap*), complementando los conocimientos previos adquiridos en la asignatura de *Metodologías de Desarrollo de Software*.
  * Definición conceptual de la propuesta técnica **`nanoaod-schema-linter`** (validador de integridad estructural y esquemas para datasets abiertos de CMS del CERN).
  * Elaboración completa de la ficha de planificación inicial (Evidencia 1), delimitando objetivos, alcance, 3 hitos verificables, asignación de roles, matriz de riesgos y roadmap por sprints.
  * Generación y verificación de artefactos documentales en el repositorio local.

---

## 2. Registro de Incidencias Técnicas y Soluciones

### Incidencia 1: Brecha de conocimiento de dominio físico (Física de Partículas vs. TI)
* **Dificultad:** Desconocimiento de la semántica de ramas cinemáticas, física de colisiones y esquemas internos de NanoAOD.
* **Intento de abordaje:** Intentar abarcar análisis de física o modelos complejos resultaba inviable para un estudiante de 4.º semestre de TI sin formación en física cuántica.
* **Solución aplicada:** Reencuadre del problema hacia la **ingeniería de software y contratos de datos**. La herramienta `nanoaod-schema-linter` se definió de manera desacoplada: valida claves, existencia de columnas y tipos de datos mediante un esquema declarativo YAML, sin requerir interpretación de física de partículas.

### Incidencia 2: Incertidumbre técnica en la inspección de metadatos de Uproot
* **Dificultad:** Falta de certeza sobre cómo la librería `uproot` expone los tipos de datos internos de C++/ROOT (`Float_t`, arrays irregulares de Awkward) y si es posible validar cabeceras sin cargar eventos a memoria RAM.
* **Intento de abordaje:** Revisión de la documentación de `uproot.open`.
* **Solución propuesta:** Formalizar un *Spike* técnico en el Sprint 1 del roadmap para ejecutar pruebas de introspección con `tree.typenames()` sobre un archivo real de CMS Open Data antes de iniciar la codificación del validador.

---

## 3. Estado de Pendientes y Próximos Pasos

* **Actividades pendientes:**
  * Descargar o acceder vía remota (XRootD / HTTP) a una muestra pequeña de NanoAOD de CMS Open Data (ej. corrida 2016) para inspeccionar la estructura real del árbol `Events`.
  * Redactar un primer borrador del archivo de contrato `schema.yaml` de prueba.
  * Desarrollar la Actividad 3.1 de la Semana 7 (CMS Open Data Hackathon & GitHub Skills: Review Pull Requests).
* **Próximos pasos inmediatos:**
  * Crear el entorno virtual con `uproot` y ejecutar el script exploratorio de introspección de cabeceras.
  * Implementar el algoritmo de validación de conjuntos (diferencia de claves en Python) para verificar ramas requeridas.
