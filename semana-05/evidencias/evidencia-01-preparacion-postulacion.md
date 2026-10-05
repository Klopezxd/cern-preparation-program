# Evidencia 1 — Preparación de Postulación y Perfil Profesional Consolidado

* **Módulo:** [Application Preparation — CERN Application Workshop](https://cern.primesys.site/) | **Fecha:** 02 de octubre de 2026

> **Objetivo:** Consolidar el perfil técnico y los documentos preparatorios para oportunidades académicas e internacionales (CERN Summer Student Programme y posgrados), integrando la versión actualizada del currículum bajo estándares europeos (Europass / ESCO), una carta de motivación técnica independiente en inglés formal (~435 palabras), perfiles profesionales verificables en GitHub y LinkedIn, el desglose de proyectos de software reales con restricciones de ingeniería superadas, definición de áreas de interés en infraestructura de TI y una reflexión crítica honesta sobre las competencias técnicas y lingüísticas a fortalecer.

---

## 1. Currículum Vítae Técnico Internacional (Europass & Taxonomía ESCO)

La postulación internacional exige un formato normalizado reconocido por evaluadores europeos. El currículum se mantiene estructurado bajo el estándar oficial **Europass** y la taxonomía ocupacional **ESCO** (*European Skills, Competences, Qualifications and Occupations*), abarcando exactamente dos páginas sin sobrecargas estéticas:

* **Titular profesional:** `IT Engineering Student | Systems, Infrastructure & Linux Environments`.
* **Educación universitaria:** Cursando el 4.º semestre de Ingeniería en Tecnologías de la Información en la Universidad de las Fuerzas Armadas – ESPE (Ecuador), titulación de tercer nivel oficial equivalente a EQF Nivel 6 (*Bachelor level*), con alto rendimiento académico y distinción institucional.
* **Competencias técnicas ESCO categorizadas:**
  * *Systems & Infrastructure:* `operating systems` (Linux Ubuntu / WSL2), `manage ICT virtualisation environments` (Docker Engine nativo en Linux, Docker Compose), `server administration` (Ubuntu Server LTS, SSH, Tailscale).
  * *Software & Automation:* `Python (computer programming)`, `use scripting programming` (Bash, PowerShell), `computer programming` (C# .NET), `tools for software configuration management` (Git CLI, ramas, resolución de conflictos, pull requests).
  * *Data & Tools:* `perform data analysis` (NumPy, Scikit-HEP, Matplotlib, procesamiento de arreglos).
* **Idiomas certificados:** Español (nativo) e Inglés acreditado oficialmente mediante examen **EF SET (57/100, B2 Upper Intermediate)** con verificación pública en [`cert.efset.org/es/zmcucg`](https://cert.efset.org/es/zmcucg).
* **Archivo de respaldo:** La versión PDF estructurada se encuentra archivada localmente para adjuntar en Moodle.

---

## 2. Carta de Motivación Técnica (*Technical Motivation Statement*)

Para convocatorias internacionales como el **CERN Summer Student Programme**, la carta de motivación constituye un documento formal independiente de **una página exacta** (~435 palabras, dentro del estándar de SmartRecruiters de 400 a 500 palabras / ~3,000 caracteres).

Se redactó en inglés formal bajo el principio **BLUF** (*Bottom Line Up Front*), sustentada en restricciones de hardware reales y libre de clichés corporativos:

* **Documento oficial completo:** [✉️ carta-de-motivacion-cern.md](./carta-de-motivacion-cern.md)

### Síntesis de la Estructura Argumentativa:
1. **Apertura (BLUF):** Candidatura directa al programa de verano del CERN en el área de infraestructura de sistemas, Linux y automatización de datos.
2. **Proyectos reales con restricciones:** Justificación de C# .NET Native AOT y SQLite WAL para entregar un ejecutable de 13 MB con numeración atómica para Agrocalidad (`vet-prescription-generator`), y microservicio en Hugging Face con ZeroGPU para diarización y transcripción sin costo local (`whisperx-transcriptor`).
3. **Procesamiento de datos científicos:** Manipulación de arreglos irregulares en CMS NanoAOD con `uproot` y `awkward-array`, reconstrucción cinemática del bosón Z a 91.2 GeV y reproducibilidad en Docker.
4. **Motivación en el CERN:** Aprender cómo opera el *Worldwide LHC Computing Grid* (WLCG) a escala de petabytes y cómo se administran clústeres distribuidos.
5. **Cierre protocolar:** Enfoque en hábitos de terminal pura, Git ordenado y despedida formal europea (`Yours faithfully`).

---

## 3. Perfil Profesional Digital y Portafolio

La identidad técnica se respalda mediante perfiles públicos actualizados y auditables:

* **GitHub:** [https://github.com/Klopezxd](https://github.com/Klopezxd)
  * Repositorio del programa: [`cern-preparation-program`](https://github.com/Klopezxd/cern-preparation-program) con el historial completo de ejercicios, cuadernos y entornos Docker.
  * Repositorios de software en producción y utilidades de automatización con pipelines de integración continua en GitHub Actions.
* **LinkedIn:** [https://www.linkedin.com/in/lkleverjosue/](https://www.linkedin.com/in/lkleverjosue/)
  * Titular técnico sobrio: `IT Engineering Student | Systems, Infrastructure & Scientific Computing`.
  * Módulo «Destacado» vinculado al portafolio de código en GitHub y validación de aptitudes técnicas centrales (Linux, Docker, Python, Git).

---

## 4. Proyectos Técnicos Relevantes

Se documentan tres proyectos representativos analizados bajo el método STAR (Situación, Tarea, Acción y Resultado medible):

### Proyecto 1: `cern-preparation-program` — Procesamiento de Datasets CMS Open Data
* **Situación:** Necesidad de explorar y analizar eventos de colisiones de física de partículas a partir de archivos de datos abiertos (`.root`) sin instalar stacks pesados en la máquina anfitriona.
* **Tarea:** Filtrar candidatos dimuónicos y reconstruir cinemáticamente el pico de masa invariante del bosón Z a $91.2\text{ GeV}$ garantizando la reproducibilidad del entorno.
* **Acción:** Implementación de un flujo de análisis en Python utilizando librerías del ecosistema Scikit-HEP (`uproot` para lectura directa de árboles ROOT, `awkward-array` para la manipulación de arreglos irregulares o *jagged arrays*, y `vector` para cuadrivectores relativistas). Todo el pipeline fue empaquetado y validado dentro de un contenedor Docker (`root-vnc`), ejecutado sobre Docker Engine nativo en Ubuntu/WSL2.
* **Resultado:** Reconstrucción exitosa de la distribución de masa invariante en Matplotlib y entorno de análisis científico 100% aislado y portable.

### Proyecto 2: `vet-prescription-generator` — Software de Escritorio Autónomo
* **Situación:** Profesionales veterinarios sujetos a la normativa de control de Agrocalidad (Ecuador) debían generar recetas oficiales manualmente en Word o Excel, provocando fricción operativa, riesgo de sanciones por inconsistencias y falta de trazabilidad contable.
* **Tarea:** Crear una herramienta de escritorio rápida, confiable y de cero mantenimiento para usuarios no técnicos, sin requerir la instalación de motores de bases de datos externos.
* **Acción:** Desarrollo en C# .NET 10 compilado bajo la arquitectura **Native AOT** (*Ahead-Of-Time*), eliminando la dependencia del runtime de .NET. Integración de una base de datos local embebida **SQLite en modo WAL** (*Write-Ahead Logging*) para permitir lecturas y escrituras concurrentes con numeración correlativa atómica. La interfaz se diseñó como un micro-servidor HTTP local que proyecta una vista web en modo aplicación (`Edge --app`), calibrando la impresión simétrica A4 vía `@media print`.
* **Resultado:** Ejecutable único (*Single-File Trimmed*) de solo **~13 MB**, inicio instantáneo (<50 ms), 28 pruebas automatizadas y automatización de despliegues mediante GitHub Actions.

### Proyecto 3: `whisperx-transcriptor` — Microservicio de Diarización en la Nube
* **Situación:** Necesidad de transcribir y segmentar por hablantes múltiples grabaciones de conferencias académicas sin agotar la memoria RAM ni la CPU de una computadora portátil local.
* **Tarea:** Procesar modelos pesados de aprendizaje profundo (WhisperX, CTranslate2 y Pyannote Audio 3.1) en un entorno acelerado por hardware a costo cero.
* **Acción:** Construcción de un microservicio en Python desplegado sobre la plataforma **Hugging Face Spaces** utilizando **ZeroGPU** (aceleración CUDA dinámica bajo demanda) con interfaz interactiva en Gradio y API REST.
* **Resultado:** Transcripción y diarización precisa de archivos de audio de larga duración ejecutados en infraestructura cloud, con cero consumo de recursos locales.

### Proyecto 4: `preview-suite` — Herramienta Web de Renderizado en Tiempo Real
* **Situación:** Dificultad para validar expresiones matemáticas en LaTeX y formato HTML semántico estricto antes de realizar entregas académicas en plataformas virtuales (Moodle).
* **Tarea:** Desarrollar una herramienta interactiva, liviana y accesible sin dependencias de backend pesado para previsualizar y depurar sintaxis técnica al vuelo.
* **Acción:** Creación de una SPA (*Single Page Application*) modular en JavaScript vanilla integrando los motores de renderizado KaTeX (matemáticas vectoriales) y Prism.js (resaltado de sintaxis), implementada bajo arquitectura serverless y desplegada de forma continua en producción mediante Vercel y GitHub Pages.
* **Resultado:** Aplicación web en producción con latencia de renderizado casi nula, compatible con estándares web modernos y utilizada activamente para validar entregables académicos.

---

## 5. Área de Interés Tecnológico y Científico

En una futura oportunidad internacional (CERN Summer Student o posgrado en Europa), el objetivo no es la física teórica pura, sino la **ingeniería de infraestructura y sistemas** que sostiene la investigación de gran escala:

1. **Infraestructura de Sistemas y Linux:** Operación, aseguramiento y monitoreo de servidores Linux de alto rendimiento dedicados a procesamiento de datos.
2. **Contenerización y Entornos Reproducibles:** Optimización de contenedores Docker, diseño de imágenes minimalistas, gestión de volúmenes persistentes y aislamiento de procesos para cargas científicas.
3. **Pipelines de Automatización y Datos:** Creación de flujos de trabajo en Python y scripts de automatización para ingestión, filtrado y verificación de integridad en conjuntos de datos distribuidos (WLCG).

---

## 6. Reflexión Crítica y Autoevaluación

Para una postulación internacional altamente competitiva, el autodiagnóstico honesto identifica dos dimensiones técnicas y formativas que requieren desarrollo prioritario antes del envío oficial:

1. **Fluidez Lingüística en Producción Activa (Inglés B1 $\rightarrow$ B2/C1 Técnico):**  
   Si bien cuento con una certificación EF SET de nivel B2 en comprensión lectora y auditiva que me permite estudiar documentación técnica compleja, reconozco que mi capacidad de **producción activa espontánea** (redacción rápida de ensayos y entrevistas orales técnicas sin apoyo asistido) se sitúa actualmente en un nivel B1 sólido. Se requiere entrenamiento deliberado en conversación técnica en tiempo real para defender decisiones de arquitectura bajo presión sin vacilación.
2. **Profundización en Redes y Sistemas Distribuidos a Gran Escala:**  
   Mi experiencia actual se concentra en máquinas individuales, servidores domésticos (Homelab con Ubuntu Server y Tailscale) y contenedores locales en WSL2. Para ser plenamente competitivo en el CERN, es indispensable expandir mis conocimientos teóricos y prácticos en redes avanzadas, protocolos de transferencia masiva de datos y modelos de almacenamiento distribuido más allá del host local.

---

## 7. Enlaces y Recursos de la Actividad

* **Carta de Motivación Técnica Independiente:** [`carta-de-motivacion-cern.md`](./carta-de-motivacion-cern.md) (versión oficial de 1 página en inglés formal).
* **Guía de Comunicación Escrita (English for Emails):** [`../ejercicios/01-comunicacion-escrita-english-for-emails.md`](../ejercicios/01-comunicacion-escrita-english-for-emails.md)
* **Guía de Entrevistas Técnicas (You're Hired):** [`../ejercicios/02-entrevistas-tecnicas-youre-hired.md`](../ejercicios/02-entrevistas-tecnicas-youre-hired.md)
* **Repositorio Oficial en GitHub:** [Klopezxd/cern-preparation-program](https://github.com/Klopezxd/cern-preparation-program/tree/main/semana-05)
