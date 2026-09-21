# Evidencia 3 — Primer CV Técnico Internacional

* **Módulo:** [3.1 CV Técnico Internacional — Europass](https://cern.primesys.site/mod/url/view.php?id=21) | **Fecha:** 20 de septiembre de 2026

> **Objetivo:** Elaborar la primera versión de un currículum vítae técnico en idioma inglés orientado a oportunidades académicas internacionales (como el CERN Summer Student Programme y pasantías de investigación), estructurado bajo el formato oficial europeo Europass y el catálogo de competencias ESCO, integrando información de contacto, formación académica universitaria, perfil técnico categorizado, proyectos reales en producción e investigación, idiomas según el marco CEFR y actividades extracurriculares verificables.

---

## 1. Fundamentos y Uso de la Plataforma Europass (Estándar ESCO)

Para postular a programas internacionales como el **CERN** o a intercambios académicos en Europa, el formato de presentación es clave. Muchos reclutadores y comités evalúan cientos de perfiles de distintos países donde los nombres de las materias o títulos varían mucho.

Por esta razón se utilizó la plataforma oficial **Europass** (`https://europass.europa.eu/`), que utiliza el estándar **ESCO** (*European Skills, Competences, Qualifications and Occupations*). Este sistema permite:
* Normalizar las habilidades técnicas bajo nombres comunes reconocidos en toda la Unión Europea (identificadas con la bandera de la UE 🇪🇺).
* Organizar el perfil de forma limpia y directa, priorizando las competencias que realmente se dominan.
* Mantener un perfil digital editable en la nube de Europass para futuras actualizaciones conforme avance la carrera.

```text
               ┌──────────────────────────────────────────────────┐
               │         ESTRUCTURA DEL CV EN EUROPASS            │
               │             Klever López (@Klopezxd)             │
               └────────────────────────┬─────────────────────────┘
                                        │
         ┌──────────────────────────────┼──────────────────────────────┐
         ▼                              ▼                              ▼
 ┌───────────────┐              ┌───────────────┐              ┌───────────────┐
 │   EDUCACIÓN   │              │ HABILIDADES   │              │  PROYECTOS Y  │
 │   E IDIOMAS   │              │   ESCO / UE   │              │  MEMBRESÍAS   │
 ├───────────────┤              ├───────────────┤              ├───────────────┤
 │ • B.S. en TI  │              │ • Systems &   │              │ • CERN Prep.  │
 │   (ESPE, EQF6)│              │   Cloud Infra │              │   (NanoAOD)   │
 │ • Distinción  │              │ • Software &  │              │ • WhisperX    │
 │   académica   │              │   Automation  │              │   (AI / CUDA) │
 │ • Inglés B2/B1│              │ • Scientific  │              │ • Preview-App │
 │   (EF SET)    │              │   Computing   │              │ • Beca y IEEE │
 └───────────────┘              └───────────────┘              └───────────────┘
```

---

## 2. Contenido y Secciones del CV Generado

El currículum se estructuró para abarcar exactamente **dos páginas**, manteniendo la lectura ágil y enfocada en lo técnico:

### 2.1. Información Personal y de Contacto
* **Titular profesional:** `IT Engineering Student | Systems, Infrastructure & Scientific Computing`.
* **Resumen inicial:** Breve descripción orientada al interés en infraestructura de sistemas, entornos Linux, contenedores y análisis de datos científicos.
* **Ubicación general:** Ecuador.
* **Enlaces profesionales públicos:** Enlaces directos al perfil de [GitHub (@Klopezxd)](https://github.com/Klopezxd) y [LinkedIn (lkleverjosue)](https://www.linkedin.com/in/lkleverjosue/).
* **Datos de contacto personal:** Teléfono celular, correo institucional y dirección particular constan en el PDF oficial entregado en Moodle (omitidos en este repositorio público por privacidad y prevención de recolección automatizada).

### 2.2. Formación Académica (*Education and Training*)
* **Carrera:** *Bachelor of Science in Information Technology Engineering*.
* **Universidad:** Universidad de las Fuerzas Armadas – ESPE (Sangolquí, Ecuador).
* **Nivel europeo:** EQF Nivel 6 (*Bachelor level*).
* **Estado académico:** Cursando el 4.º semestre (de 8) | Graduación proyectada: 2029.
* **Rendimiento:** Alto rendimiento académico, acreedor a Beca por Distinción Académica de la ESPE. *(Detalle cuantitativo formalizado en el PDF oficial entregado en Moodle)*.
* **Materias relevantes:** Estructuras de Datos y Algoritmos, Modelos Discretos, Métodos Numéricos, Sistemas Operativos, Bases de Datos y Cómputo Científico.

### 2.3. Habilidades Técnicas Clasificadas (ESCO)
En lugar de una lista desordenada, las competencias se organizaron en 3 categorías claras:

| Categoría | Competencias Oficiales (ESCO) | Aplicación Práctica |
| :--- | :--- | :--- |
| **Systems & Cloud Infrastructure** | • `operating systems` 🇪🇺<br>• `manage ICT virtualisation environments` 🇪🇺<br>• `cloud technologies` 🇪🇺<br>• `DevOps` 🇪🇺<br>• `Git/github, Docker, Gitlab` | Manejo de Linux (Ubuntu en WSL2), Docker Engine nativo, redes de contenedores y despliegues en Oracle Cloud y Vercel. |
| **Software Development & Automation** | • `Python (computer programming)` 🇪🇺<br>• `use scripting programming` 🇪🇺<br>• `computer programming` 🇪🇺<br>• `tools for software configuration management` 🇪🇺<br>• `Agile development` 🇪🇺 | Automatización en Python, scripts de administración en Bash y PowerShell, control de versiones con Git y trabajo con ramas/PRs. |
| **Data Analysis & Scientific Computing** | • `perform data analysis` 🇪🇺 | Procesamiento de arreglos con NumPy, filtrado de eventos en Scikit-HEP y reconstrucción de masa invariante. |

### 2.4. Proyectos Técnicos Relevantes (*Projects*)
Dado que aún no cuento con contratos laborales formales en empresas, el CV prioriza proyectos reales con código verificable:

1. **CERN Preparation Programme — Scientific Computing & CMS Open Data:**
   * Análisis de colisiones reales del detector CMS (CERN Open Data Run 1) usando librerías de Scikit-HEP (`uproot`, `awkward-array`, `vector`).
   * Filtrado de eventos con dos muones y reconstrucción de la masa invariante del bosón Z ($91.2\text{ GeV}$).
   * Uso de contenedores Docker con imágenes oficiales de ROOT para garantizar reproducibilidad.
   * Repositorio: [`cern-preparation-program`](https://github.com/Klopezxd/cern-preparation-program).
2. **WhisperX Audio Transcriptor & Diarization Pipeline (AI / Cloud):**
   * Herramienta para transcripción de audio y separación de hablantes (diarización) con WhisperX, PyTorch y Pyannote Audio.
   * Cuenta con interfaz de consola (CLI) y aplicación web interactiva en Gradio.
   * Despliegue automatizado con GitHub Actions hacia Hugging Face Spaces con soporte de GPU (CUDA / ZeroGPU).
   * Repositorio: [`whisperx-transcriptor`](https://github.com/Klopezxd/whisperx-transcriptor) | Demo en vivo: [`transcriptor-whisperx`](https://huggingface.co/spaces/Klopezxd/transcriptor-whisperx).
3. **Preview Suite — Real-time Markdown & Educational HTML Web App:**
   * Aplicación web (v3.1.0) para previsualizar y validar código Markdown y HTML semántico en tiempo real, pensada para tareas de Moodle.
   * Desplegada en producción en Vercel y GitHub Pages.
   * Repositorio: [`preview-suite`](https://github.com/Klopezxd/preview-suite) | Demo: [`preview-suite.vercel.app`](https://preview-suite.vercel.app).

### 2.5. Idiomas (*Language Skills*)
* **Español:** Lengua materna.
* **Inglés:** Nivel intermedio independiente según el marco europeo (CEFR):
  * Listening (Comprensión auditiva): **B2**
  * Reading (Lectura): **B2**
  * Spoken interaction (Interacción oral): **B1**
  * Spoken production (Expresión oral): **B1**
  * Writing (Escritura): **B1**
* **Certificado adjunto:** Examen oficial **EF SET (57/100 - B2 Intermedio Alto)** rendido en diciembre de 2024, con código de verificación pública en [`cert.efset.org/es/zmcucg`](https://cert.efset.org/es/zmcucg).

### 2.6. Becas y Membresías
* **Beca por Distinción Académica (ESPE):**
  * Concesión institucional correspondiente al período académico SI 2026 (abril - agosto 2026) en reconocimiento al alto rendimiento en la carrera. *(Resolución y contrato formalizados en el PDF institucional entregado en Moodle)*.
* **Membresías IEEE:**
  * Miembro estudiantil activo de la **IEEE** y la **IEEE Computer Society** (Ecuador Section). *(Número de membresía registrado en el PDF oficial)*.
  * Participación en el Club de Software de la ESPE.

---

## 3. Entregables Generados

| Recurso | Archivo | Descripción |
| :--- | :--- | :--- |
| **CV Europass en PDF** | `CV_Klever_Lopez_Europass.pdf` | Currículum oficial de 2 páginas generado en Europass en idioma inglés (entregado en Moodle, protegido en `.gitignore`). |
| **Informe de Evidencia (PDF)** | `Evidencia3_CV_Tecnico_Internacional.pdf` | Documento formal de entrega con el respaldo técnico y detalles de la actividad (entregado en Moodle, protegido en `.gitignore`). |
| **Documentación en el Repositorio** | `evidencia-03-cv-tecnico.md` | Archivo Markdown de respaldo técnico público en el repositorio. |

---

## 4. Conclusiones y Aprendizajes de la Actividad

1. **Honestidad en el perfil técnico:** Al principio evaluamos si poner el programa de preparación del CERN como experiencia laboral formal, pero fue mucho más acertado marcar la opción *"Not yet"* en empleo y ubicarlo donde corresponde: como un **proyecto técnico de investigación**. Esto evita inflar el perfil y permite defender con solvencia cada línea del documento ante cualquier evaluador.
2. **Priorizar proyectos verificables:** Para un estudiante de tercer/cuarto semestre, lo que valida el conocimiento no son los títulos de cargos ficticios, sino los enlaces a proyectos reales. Incluir la reconstrucción del bosón Z con datos del CMS, la herramienta de transcripción en Hugging Face con GPU y la app web en producción demuestra capacidad práctica y autonomía.
3. **Utilidad del estándar Europass y ESCO:** Aprender a utilizar la plataforma europea sirvió para categorizar las tecnologías que realmente domino (Linux, Docker, Python y Git) bajo una nomenclatura formal que entienden en cualquier universidad o centro científico del exterior.
4. **Base lista para convocatorias internacionales:** Con este borrador consolidado en inglés, respaldado por mi certificado de inglés EF SET y mi membresía en IEEE, ya cuento con un currículum base que puedo seguir actualizando durante las semanas restantes del programa y utilizar para postular formalmente a estancias de investigación como el *CERN Summer Student Programme*.
