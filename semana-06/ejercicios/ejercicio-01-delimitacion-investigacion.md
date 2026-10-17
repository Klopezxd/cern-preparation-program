# Ejercicio 1 — Fundamentos de Investigación y Delimitación Temática

* **Recurso de referencia:** [Elsevier Researcher Academy — Research Preparation](https://researcheracademy.elsevier.com/research-preparation)
* **Fecha:** 05 de octubre de 2026
* **Estudiante:** Klever López (Ingeniería en Tecnologías de la Información)

---

## 1. Síntesis Metodológica (Elsevier Researcher Academy)

### A. Estrategia de Búsqueda de Literatura
* **Operadores booleanos:** Estructuración de cadenas con `AND`, `OR` y `NOT` para filtrar ruido técnico.
* **Bases de datos confiables:** Scopus, IEEE Xplore, arXiv (secciones de computación e inteligencia artificial) y repositorios abiertos institucionales.
* **Técnica de bola de nieve (*Snowballing*):** Rastreo retrospectivo (referencias citadas en papers base) y prospectivo (artículos que citan al trabajo de referencia) para mapear la evolución del estado del arte.

### B. Criterios de Confiabilidad
* Validación mediante revisión por pares (*peer-review*).
* Evaluación de preprints en arXiv mediante verificación de filiación de los autores y disponibilidad pública de código/datos reproducibles (GitHub/Zenodo).

### C. Detección de Brechas de Investigación (*Research Gaps*)
* Focalización en las secciones de *Limitations* y *Future Work* en lugar de conclusiones comerciales.
* Identificación de problemas de escalabilidad, consumo excesivo de memoria o barreras de hardware en herramientas existentes.

---

## 2. Aplicación de la Técnica del Embudo para Delimitación

```text
[ Área General ]
   Inteligencia Artificial Aplicada y Procesamiento Digital de Audio
           │
           ▼
[ Subcampo ]
   Reconocimiento Automático del Habla (ASR) e Inferencia Local
           │
           ▼
[ Problema Concreto ]
   Alto consumo de memoria RAM/VRAM y latencia de modelos Transformer abiertos en estaciones de trabajo convencionales
           │
           ▼
[ Pregunta Delimitada ]
   ¿En qué medida la cuantización post-entrenamiento (como INT8) reduce el consumo de recursos sin degradar severamente la precisión acústica (WER) en español?
```

---

## 3. Ficha de Trabajo Inicial

* **Tema:** Evaluación de técnicas de cuantización para la inferencia local de modelos abiertos de reconocimiento automático del habla (ASR).
* **Problema identificado:** Los modelos abiertos de transcripción automática basados en arquitecturas Transformer (como Whisper y sus variantes) ofrecen alta precisión, pero exigen una cantidad considerable de memoria RAM y VRAM. Al ejecutarse localmente en estaciones de trabajo convencionales o computadores personales, suelen presentar problemas de latencia elevada o desbordamientos de memoria al procesar audios de mediana y larga duración, limitando su aprovechamiento práctico sin recurrir a costosas GPUs de servidor.
* **Pregunta de investigación:** ¿En qué medida la aplicación de cuantización post-entrenamiento (como INT8) reduce el consumo de memoria y los tiempos de procesamiento en la inferencia local de modelos abiertos de transcripción, manteniendo una tasa de error de palabras (WER) aceptable en audio en español?
* **Relevancia:** Investigar este aspecto permite habilitar el procesamiento local de voz en equipos estándar de cómputo, garantizando la privacidad de los datos de audio sensibles sin depender de servicios en la nube. Además, ofrece una base práctica de ingeniería de software para medir compromisos (*trade-offs*) entre eficiencia computacional y calidad de transcripción.
