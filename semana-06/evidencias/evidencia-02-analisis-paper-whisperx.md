# Evidencia 2 — Lectura y Análisis Crítico de Artículo Científico (Guía de S. Keshav)

* **Módulo:** [2.1 Lectura y análisis de artículos científicos](https://cs.uwaterloo.ca/~brecht/courses/856/readings/how-to-read/keshav-paper-reading.pdf) | **Fecha:** 07 de octubre de 2026
* **Estudiante:** Klever López (4.º semestre, Ingeniería en Tecnologías de la Información)
* **Institución:** Universidad de las Fuerzas Armadas – ESPE
* **Docente / Coordinadora:** Ing. Tatiana Gualotuña
* **Iniciativa:** Programa de Preparación para Oportunidades CERN (Semana 6)

> **Objetivo:** Aplicar la metodología de lectura estructurada de tres pasadas propuesta por S. Keshav para analizar un artículo científico del área de Inteligencia Artificial aplicada y procesamiento de señales de audio, identificando su problema central, objetivos, metodología desacoplada, resultados cuantitativos, limitaciones técnicas y formulando una reflexión crítica orientada a la ingeniería de software.

---

## 1. Ficha Técnica y Referencia Bibliográfica

* **Título:** *WhisperX: Time-Accurate Speech Transcription of Long-Form Audio*
* **Autores:** Max Bain, Jaesung Huh, Tengda Han y Andrew Zisserman
* **Filiación:** *Visual Geometry Group (VGG)*, Department of Engineering Science, University of Oxford
* **Congreso / Publicación:** *Proceedings of INTERSPEECH 2023* (Conferencia internacional de referencia en procesamiento del habla)
* **Enlace oficial (arXiv / Open Access):** [https://arxiv.org/abs/2303.00747](https://arxiv.org/abs/2303.00747)

---

## 2. Análisis Estructurado del Artículo

### A. Problema que intenta resolver
El modelo OpenAI Whisper representa un estándar moderno en reconocimiento automático del habla (ASR) por su robustez ante ruidos y acentos; no obstante, presenta tres deficiencias críticas al procesar audios extensos:
1. **Desfase en marcas de tiempo (*timestamps*):** Sus marcas temporales se generan a nivel de ventana gruesa (30 segundos), provocando desalineaciones de varios segundos entre la palabra hablada y el texto subtitulado.
2. **Alucinaciones en silencios:** En secciones de silencio, pausas largas o música ambiental, el decodificador autorregresivo suele entrar en bucles repetitivos de frases inexistentes.
3. **Baja velocidad de procesamiento:** La inferencia secuencial bloque a bloque resulta lenta e ineficiente para audios de larga duración (como clases, conferencias o grabaciones extensas).

### B. Objetivo
Diseñar una arquitectura modular y eficiente que transforme a Whisper en un sistema de transcripción para audio largo con **marcas de tiempo ultra-precisas a nivel de palabra y fonema**, acelerando el tiempo de procesamiento mediante paralelización por lotes y eliminando las alucinaciones ocasionadas por silencios.

### C. Metodología y Procedimientos
Los autores estructuran un pipeline desacoplado en tres fases sin necesidad de reentrenar los pesos neuronales de Whisper:
1. **Detección de Actividad de Voz (VAD):** Implementan el modelo pre-entrenado *Pyannote-audio* para aislar exclusivamente los fragmentos donde existe voz humana, descartando silencios y ruido antes de la transcripción.
2. **Transcripción por Lotes (*Batched Inference*):** Cortan el audio en los límites naturales del habla detectados por el VAD y los agrupan en lotes paralelos procesados simultáneamente por Whisper, eliminando el cuello de botella secuencial.
3. **Alineación Fonética Forzada (*Forced Alignment*):** Toman el texto transcrito y lo proyectan sobre el audio original utilizando un modelo acústico fonético externo (*Wav2Vec 2.0* o *HuBERT*), calculando marcas de tiempo exactas mediante programación dinámica.

### D. Resultados Principales
* **Precisión temporal milimétrica:** Reducción del error de alineación de marcas de tiempo de más de 1–2 segundos en Whisper base a un error medio inferior a **50 milisegundos** por palabra.
* **Aceleración drástica del procesamiento:** Incremento de velocidad de entre **60x y 70x** en audios largos al aprovechar la inferencia por lotes en tarjetas gráficas.
* **Robustez ante alucinaciones:** Eliminación total de repeticiones de texto espurio al no alimentar a Whisper con segmentos de silencio prolongado.

### E. Limitaciones Técnicas Identificadas
* **Dependencia lingüística del modelo fonético:** La precisión de la alineación forzada depende estrictamente de contar con un modelo Wav2Vec2 entrenado para el idioma específico del audio. En idiomas con pocos recursos acústicos, la alineación por palabra decae o no está soportada.
* **Sobrecosto de memoria RAM/VRAM en equipos locales:** Al encadenar tres modelos independientes en memoria (VAD + Whisper + Wav2Vec2), el consumo de recursos computacionales se incrementa sensiblemente en comparación con una ejecución aislada, requiriendo GPUs con suficiente memoria de video para lotes grandes.

---

## 3. Reflexión Crítica

* **¿Qué aprendí?:**
  Aprendí que en ingeniería de software e inteligencia artificial no siempre es necesario entrenar un modelo gigantesco desde cero para resolver problemas complejos. Los autores de WhisperX demostraron que desacoplar el problema (usar un modelo especializado para detectar silencios, otro para transcribir y otro para alinear tiempos) supera con creces al enfoque monolítico original de OpenAI.
* **¿Qué pregunta técnica me queda?:**
  *¿Cómo impactaría la aplicación de técnicas de cuantización (como INT8 mediante CTranslate2) sobre este pipeline de tres etapas al ejecutarse en estaciones de trabajo convencionales de uso académico, y si dicha cuantización degrada la precisión de la alineación fonética en español?*

---

## 4. Síntesis para Entrega en Plataforma Moodle

```html
<p><strong>Referencia y enlace:</strong> <em>WhisperX: Time-Accurate Speech Transcription of Long-Form Audio</em>. Autores: Max Bain, Jaesung Huh, Tengda Han y Andrew Zisserman (Universidad de Oxford, INTERSPEECH 2023). URL: <a href="https://arxiv.org/abs/2303.00747" target="_blank">https://arxiv.org/abs/2303.00747</a>.</p>

<p><strong>Problema:</strong> El modelo Whisper de OpenAI tiene dificultades en audios largos: genera marcas de tiempo inexactas a nivel de palabra, alucina repitiendo texto en silencios y procesa de forma secuencial y lenta.</p>

<p><strong>Objetivo:</strong> Diseñar un pipeline modular para audios largos que logre marcas de tiempo exactas por palabra (< 50 ms), incremente la velocidad mediante procesamiento por lotes y elimine alucinaciones en silencios.</p>

<p><strong>Metodología:</strong> Integran tres componentes desacoplados: 1) Detección de Actividad de Voz (VAD con Pyannote) para filtrar silencios; 2) Transcripción en lotes paralelos con Whisper; 3) Alineación forzada fonética mediante modelos Wav2Vec 2.0.</p>

<p><strong>Resultados:</strong> Reducción del error de marcas de tiempo a menos de 50 ms por palabra, aceleración del procesamiento de 60x a 70x en audios extensos y supresión de repeticiones en silencios.</p>

<p><strong>Limitaciones:</strong> Requiere modelos fonéticos pre-entrenados para cada idioma específico e incrementa el consumo de memoria RAM/VRAM al mantener tres modelos encadenados en el pipeline.</p>

<p><strong>Reflexión y pregunta abierta:</strong> Aprendí el valor del diseño desacoplado en IA en lugar de depender de modelos monolíticos. Me queda la pregunta: ¿cómo afectaría la cuantización INT8 en este pipeline al ejecutarse en computadores convencionales y afectará la precisión acústica en español?</p>
```
