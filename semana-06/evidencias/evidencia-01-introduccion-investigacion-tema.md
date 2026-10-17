# Evidencia 1 — Introducción a la Investigación Científica y Delimitación Temática

* **Módulo:** [1.1 Introducción a la investigación científica](https://researcheracademy.elsevier.com/research-preparation) | **Fecha:** 05 de octubre de 2026
* **Estudiante:** Klever López (4.º semestre, Ingeniería en Tecnologías de la Información)
* **Institución:** Universidad de las Fuerzas Armadas – ESPE
* **Docente / Coordinadora:** Ing. Tatiana Gualotuña
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 6)

> **Objetivo:** Formular una propuesta inicial de investigación tecnológica basada en los principios de búsqueda de literatura especializada, identificación de fuentes confiables, detección de brechas y delimitación de problemas adquiridos en los módulos de *Research Preparation* de Elsevier Researcher Academy, aplicada de manera realista a la optimización de inferencia de modelos de inteligencia artificial en hardware de consumo.

---

## 1. Fundamentos Metodológicos de Investigación (Elsevier Researcher Academy)

A partir de la revisión de los módulos de preparación para la investigación de Elsevier, se identificaron cuatro principios rectores aplicables a proyectos de ingeniería y ciencias de la computación:

1. **Estrategia estructurada de búsqueda:** Uso de lógica booleana (`AND`, `OR`, `NOT`) y términos controlados en bases científicas indexadas (Scopus, IEEE Xplore, ACM Digital Library) y repositorios abiertos especializados (arXiv, CERN Document Server) para mapear antecedentes sin sesgo de algoritmos comerciales.
2. **Identificación de literatura confiable:** Validación del rigor metodológico mediante el arbitraje de pares (*peer-review*), indexación en cuartiles Scopus/SJR o conferencias CORE en computación. En preprints técnicos, se prioriza la verificación de código fuente reproducible y datasets en repositorios públicos auditables (GitHub, Zenodo).
3. **Reconocimiento de brechas (*Research Gaps*):** Identificación de limitaciones explícitas reportadas por autores en las secciones de discusión y trabajo futuro, particularmente cuellos de botella de hardware, sobrecostos de memoria o falta de evaluación en escenarios de cómputo restringido.
4. **Delimitación mediante técnica de embudo:** Reducción sistemática desde un campo amplio (Inteligencia Artificial y Procesamiento de Señales) hacia un problema medible y factible de experimentar con herramientas disponibles en un entorno local (Python, WSL2, Docker).

---

## 2. Ficha de Delimitación de Investigación

### Tema
* **Título preliminar:** Evaluación de técnicas de cuantización para la inferencia local de modelos abiertos de reconocimiento automático del habla (ASR).
* **Área técnica:** Inteligencia Artificial Aplicada y Procesamiento Digital de Audio.

### Problema
Los modelos abiertos de transcripción automática basados en arquitecturas Transformer (como Whisper y sus variantes) ofrecen alta precisión, pero exigen una cantidad considerable de memoria RAM y VRAM. Al ejecutarse localmente en estaciones de trabajo convencionales o computadores personales, suelen presentar problemas de latencia elevada o desbordamientos de memoria al procesar audios de mediana y larga duración, limitando su aprovechamiento práctico sin recurrir a costosas GPUs de servidor.

### Pregunta de Investigación
> **¿En qué medida la aplicación de cuantización post-entrenamiento (como INT8) reduce el consumo de memoria y los tiempos de procesamiento en la inferencia local de modelos abiertos de transcripción, manteniendo una tasa de error de palabras (WER) aceptable en audio en español?**

### Relevancia
1. **Viabilidad técnica accesible:** Permite acercar tecnologías avanzadas de procesamiento del habla a computadores estándar, democratizando el acceso a herramientas de transcripción para estudiantes, investigadores y pequeñas organizaciones sin requerir hardware de centro de datos.
2. **Privacidad y autonomía:** La inferencia local procesa archivos de voz sin transmitir datos confidenciales a APIs externas ni incurrir en costos recurrentes de infraestructura en la nube.
3. **Alineación con formación en TI:** Permite aplicar conceptos prácticos de benchmarking, medición de métricas de rendimiento (latencia, uso de memoria, tasa de error por palabra o *WER*) y reproducibilidad experimental en entornos Linux.

---

## 3. Síntesis Estructurada para Entrega en Plataforma Moodle

```html
<p><strong>Tema:</strong> Evaluación de técnicas de cuantización para la inferencia local de modelos abiertos de reconocimiento automático del habla (ASR).</p>

<p><strong>Problema:</strong> Los modelos abiertos de transcripción automática basados en arquitecturas Transformer (como Whisper y sus variantes) ofrecen alta precisión, pero exigen una cantidad considerable de memoria RAM y VRAM. Al ejecutarse localmente en estaciones de trabajo convencionales o computadores personales, suelen presentar problemas de latencia elevada o desbordamientos de memoria al procesar audios de mediana y larga duración, limitando su aprovechamiento práctico sin recurrir a costosas GPUs de servidor.</p>

<p><strong>Pregunta de investigación:</strong> ¿En qué medida la aplicación de cuantización post-entrenamiento (como INT8) reduce el consumo de memoria y los tiempos de procesamiento en la inferencia local de modelos abiertos de transcripción, manteniendo una tasa de error de palabras (WER) aceptable en audio en español?</p>

<p><strong>Relevancia:</strong> Investigar este aspecto permite habilitar el procesamiento local de voz en equipos estándar de cómputo, garantizando la privacidad de los datos de audio sensibles sin depender de servicios en la nube. Además, ofrece una base práctica de ingeniería de software para medir compromisos (trade-offs) entre eficiencia computacional y calidad de transcripción.</p>
```
