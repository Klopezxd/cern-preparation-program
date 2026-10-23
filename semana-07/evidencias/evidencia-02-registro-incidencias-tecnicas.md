# Evidencia 2 — Registro de Avances e Incidencias Técnicas

* **Módulo:** [2.1 Registro de avances e incidencias técnicas](https://cern.primesys.site/) | **Fecha:** 14 de octubre de 2026
* **Estudiante:** Klever López (4.º semestre, Ingeniería en Tecnologías de la Información)
* **Institución:** Universidad de las Fuerzas Armadas – ESPE
* **Docente / Coordinadora:** Ing. Tatiana Gualotuña
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 7)

> **Objetivo:** Registrar de manera rigurosa y transparente el progreso alcanzado durante la sesión de planificación de la Semana 7, documentando la formulación del proyecto tecnológico `nanoaod-schema-linter`, las evidencias generadas, los problemas técnicos y brechas de dominio identificadas con sus soluciones, así como las actividades pendientes y próximos pasos de desarrollo.

---

## 1. Ficha de Registro de Avances e Incidencias Técnicas

### 1.1 Actividades en las que se avanzó
Durante la sesión de trabajo se completaron los siguientes hitos de planificación:
1. **Revisión y fundamentación metodológica:** Asimilación de los recursos oficiales de Atlassian (*Agile Fundamentals* y *Project Roadmap*), articulando la teoría de descomposición de trabajo e hitos con la formación previa en metodologías de desarrollo ágil y Scrum.
2. **Concepción y delimitación del proyecto tecnológico:** Definición formal de la propuesta **`nanoaod-schema-linter`**, una herramienta CLI orientada a la validación de contratos de datos e integridad estructural de archivos ROOT (NanoAOD) para CMS Open Data.
3. **Estructuración de la planificación inicial (Evidencia 1):** Delimitación precisa de objetivos, alcance (*in-scope* vs. *out-of-scope*), definición de tres hitos clave, matriz de asignación de roles, plan de mitigación de riesgos técnicos y hoja de ruta secuencial organizada en cuatro sprints semanales.
4. **Documentación local:** Generación de notas técnicas en `semana-07/ejercicios/` y formalización del reporte institucional en `semana-07/evidencias/`.

---

### 1.2 Enlaces a Repositorios, Documentos y Evidencias Relevantes
* **Repositorio oficial del programa (GitHub):** [https://github.com/Klopezxd/cern-preparation-program](https://github.com/Klopezxd/cern-preparation-program)
* **Directorio oficial de la Semana 7:** [https://github.com/Klopezxd/cern-preparation-program/tree/main/semana-07](https://github.com/Klopezxd/cern-preparation-program/tree/main/semana-07)
* **Planificación Inicial del Proyecto (Evidencia 1 en GitHub):** [https://github.com/Klopezxd/cern-preparation-program/blob/main/semana-07/evidencias/evidencia-01-planificacion-proyecto-tecnologico.md](https://github.com/Klopezxd/cern-preparation-program/blob/main/semana-07/evidencias/evidencia-01-planificacion-proyecto-tecnologico.md)
* **Recursos oficiales consultados:**
  * [Atlassian — Learn Agile Fundamentals](https://community.atlassian.com/learning/course/learn-agile-fundamentals)
  * [Atlassian — Project Roadmap](https://www.atlassian.com/es/agile/project-management/project-roadmap)

---

### 1.3 Problemas Técnicos Encontrados y Soluciones Aplicadas

1. **Problema 1: Brecha de conocimiento de dominio especializado en física de partículas.**
   * *Descripción:* Como estudiante de Ingeniería en Tecnologías de la Información de 4.º semestre, existe un desconocimiento natural respecto a la semántica física de las colisiones, variables cinemáticas avanzadas y física del detector en los datasets de CMS. Intentar formular un proyecto centrado en análisis físico puro resultaba inviable y propenso a errores conceptuales.
   * *Solución aplicada:* Se reenfocó estratégicamente el proyecto hacia la **ingeniería de software y aseguramiento de calidad de datos (*data contracts*)**. En `nanoaod-schema-linter`, la física se desacopla completamente del software: el sistema solo valida existencia de columnas y compatibilidad de tipos (`dtype`) frente a un esquema declarativo YAML, permitiendo que el usuario científico defina las reglas mientras el perfil de TI asegura la solidez y eficiencia de la herramienta.

2. **Problema 2: Incertidumbre técnica sobre la introspección de metadatos en ROOT mediante Uproot.**
   * *Descripción:* Duda técnica sobre cómo `uproot` expone las cabeceras internas de C++/ROOT sin requerir la carga completa de datos en memoria RAM, y cómo homologar tipos nativos complejos (como arreglos irregulares) a primitivos de Python/NumPy.
   * *Solución aplicada:* Se incorporó un **Spike técnico** explícito en el Sprint 1 de la planificación para realizar pruebas preliminares con `tree.typenames()` sobre un archivo real de CMS NanoAOD, resolviendo la viabilidad de lectura antes de implementar el motor de comparación.

---

### 1.4 Actividades Pendientes
* Obtener acceso a un archivo de muestra real de CMS Open Data (ej. corrida 2016) para verificar empíricamente los nombres exactos y firmas de las ramas en el árbol `Events`.
* Diseñar el archivo de contrato inicial `schema.yaml` de prueba con las ramas requeridas para análisis de muones (`Muon_pt`, `Muon_eta`, `Muon_phi`, `Muon_charge`).
* Desarrollar la **Actividad 3.1 (Viernes):** *CMS Open Data Hackathon & GitHub Skills – Review Pull Requests* sobre trabajo colaborativo distribuido.

---

### 1.5 Próximos Pasos para Continuar Avanzando
1. Configurar un script mínimo en Python con `uproot` para inspeccionar las cabeceras de un archivo ROOT remoto vía HTTPS.
2. Implementar la función básica de comparación de conjuntos (`set(requeridas) - set(presentes)`) para validar ramas obligatorias.
3. Avanzar con las lecturas y guías de revisión de Pull Requests para la sesión de cierre de la semana.

---

## 2. Texto en Línea para Entrega en Plataforma Moodle

```html
<p><strong>Actividades en las que se avanzó:</strong> Durante esta sesión se completó la revisión de los fundamentos ágiles y hojas de ruta de Atlassian, conectándolos con la formación previa en metodologías de desarrollo de software y Scrum. Se concibió y delimitó formalmente el proyecto <em>nanoaod-schema-linter</em> (validador de integridad y esquemas para CMS Open Data) y se elaboró la planificación inicial completa (Evidencia 1) con objetivos, alcance, tres hitos verificables, asignación de roles, gestión de riesgos y hoja de ruta en cuatro sprints.</p>

<p><strong>Enlaces a evidencias:</strong> Repositorio del programa en GitHub: <a href="https://github.com/Klopezxd/cern-preparation-program" target="_blank">https://github.com/Klopezxd/cern-preparation-program</a>. La planificación inicial detallada se encuentra publicada en: <a href="https://github.com/Klopezxd/cern-preparation-program/blob/main/semana-07/evidencias/evidencia-01-planificacion-proyecto-tecnologico.md" target="_blank">Evidencia 1 (GitHub)</a>, fundamentada en los recursos oficiales de Atlassian Project Roadmap.</p>

<p><strong>Problemas técnicos y soluciones:</strong> 1) <em>Brecha de conocimiento en física de partículas:</em> Al no poseer formación en física cuántica ni en la semántica de colisiones del detector CMS, resultaba inviable abordar un análisis físico puro. Se solucionó reenfocando el proyecto hacia la ingeniería de software y contratos de datos, donde la herramienta valida esquemas declarativos en YAML sin requerir cálculos físicos; 2) <em>Incertidumbre en la introspección con Uproot:</em> Duda sobre la lectura eficiente de cabeceras sin saturar RAM. Se solucionó programando un spike técnico en el Sprint 1 para evaluar <code>tree.typenames()</code> antes del desarrollo formal.</p>

<p><strong>Actividades pendientes y próximos pasos:</strong> Queda pendiente inspeccionar un archivo real de CMS NanoAOD para catalogar sus ramas físicas, redactar el primer archivo <code>schema.yaml</code> de prueba y realizar la Actividad 3.1 sobre revisión de Pull Requests en GitHub. Los próximos pasos inmediatos consisten en ejecutar el spike exploratorio de lectura de cabeceras en Python y construir la función base de validación de conjuntos.</p>
```
