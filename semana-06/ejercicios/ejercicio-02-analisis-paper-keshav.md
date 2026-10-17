# Ejercicio 2 — Aplicación de la Metodología de S. Keshav: Análisis de WhisperX

* **Metodología de referencia:** S. Keshav, *How to Read a Paper* (ACM SIGCOMM Computer Communication Review, 2007).
* **Artículo analizado:** *WhisperX: Time-Accurate Speech Transcription of Long-Form Audio* (Bain et al., INTERSPEECH 2023 / arXiv:2303.00747).
* **Fecha:** 07 de octubre de 2026
* **Estudiante:** Klever López (4.º semestre, Ingeniería en TI)

---

## 1. Primera Pasada (*First Pass*): Visión Panorámica y las 5 "C"

Tiempo invertido: ~10 minutos.  
Lectura focalizada: Título, Abstract, Introducción, títulos de sección, figuras y Conclusiones.

### Evaluación de las 5 "C" de Keshav:
1. **Categoría (*Category*):** Artículo de ingeniería de sistemas y mejora de pipelines en inteligencia artificial aplicada (ASR y alineación temporal). No inventa una nueva red neuronal desde cero, sino que diseña un pipeline modular para optimizar un modelo existente (OpenAI Whisper).
2. **Contexto (*Context*):** Se sitúa en la transcripción de audio largo y diarización de hablantes. Se relaciona directamente con el paper fundacional de Whisper (Radford et al., 2022) y modelos de alineación fonética acústica (Wav2Vec 2.0).
3. **Corrección (*Correctness*):** Los supuestos son válidos. Es un hecho conocido en la comunidad que Whisper alucina en silencios y desalinea los sellos de tiempo porque su mecanismo de atención no fue diseñado para resolución a nivel de milisegundos.
4. **Contribución (*Contributions*):**
   * Incorporación de VAD (*Voice Activity Detection*) previo para filtrar silencios y particionar el audio.
   * Transcripción en lotes (*batched inference*) que multiplica la velocidad de procesamiento hasta 70x.
   * Alineación forzada fonética con Wav2Vec2 para lograr marcas de tiempo a nivel de palabra con error < 50 ms.
5. **Claridad (*Clarity*):** Alta. El artículo tiene 5 páginas, diagramas de arquitectura claros (Figura 1) y tablas de evaluación comparativas precisas.

---

## 2. Segunda Pasada (*Second Pass*): Comprensión de Componentes y Resultados

### Diagrama del Pipeline Desacoplado:
```text
[ Audio Largo de Entrada ]
           │
           ▼
[ 1. Voice Activity Detection (VAD) ] ──► Elimina silencios y segmenta regiones de habla activa
           │
           ▼
[ 2. Batched Whisper Inference ]       ──► Transcribe fragmentos en lotes paralelos (alta velocidad)
           │
           ▼
[ 3. Forced Alignment (Wav2Vec2) ]     ──► Asigna marcas de tiempo exactas por palabra (< 50 ms)
           │
           ▼
[ Salida: Transcripción con Timestamps Exactos ]
```

### Hallazgos de la Segunda Pasada:
* La velocidad no se logra cambiando los pesos de Whisper, sino agrupando segmentos homogéneos gracias al VAD y procesándolos en un único tensor por lotes.
* La eliminación de alucinaciones ocurre porque Whisper nunca recibe fragmentos con silencios puros o ruido estático de fondo.
