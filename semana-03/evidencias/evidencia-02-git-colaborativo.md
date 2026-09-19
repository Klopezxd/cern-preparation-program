# Evidencia 2 — Trabajo Colaborativo en GitHub

* **Módulo:** [2.1 GitHub — Trabajo colaborativo y Pull Requests](https://github.com/skills/review-pull-requests) | **Fecha:** 18 de septiembre de 2026

> **Objetivo:** Experimentar un flujo de trabajo colaborativo real en Git y GitHub basado en el modelo de repositorio compartido con control de acceso por pares, implementando ramas de características (*feature branches*), commits atómicos, apertura de Pull Requests, resolución de revisiones de código cruzadas (*code review*) e integración de cambios hacia la rama principal (*merge*).

---

## 1. Metodología y Arquitectura del Flujo Colaborativo

En el desarrollo de software científico y computación de alto rendimiento (HPC), el trabajo concurrente sobre un mismo proyecto exige mecanismos estrictos para proteger el tronco principal de producción (`main`) contra regresiones, inconsistencias y código sin validar.

Para esta actividad se adoptó el **modelo de repositorio compartido con ramas de características (*Shared Repository / Feature Branch Workflow*)**, recomendado por *Software Carpentry* e industrias de software:

* **Repositorio central del programa:** [`ajzambrano12-cloud/-cern-preparation-program-Angeles`](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles).
* **Gestión de accesos:** Asignación de permisos de colaborador con privilegios de escritura entre los desarrolladores del equipo (@ajzambrano12-cloud y @Klopezxd).
* **Aislamiento de cambios:** Prohibición estricta de commits directos sobre la rama `main`; cada modificación se aisló en una rama temáticamente acotada.
* **Revisión por pares (*Peer Code Review*):** Cada Pull Request requirió la inspección de diferencias (*diff*), retroalimentación técnica y aprobación del otro integrante antes de autorizar la integración (*merge*).

```text
                            [ Repositorio Remoto en GitHub ]
                                          │
                  ┌───────────────────────┴───────────────────────┐
                  ▼                                               ▼
     feature/limpieza-y-docs-semana03             feature/actualizar-cronograma-semana03
          (Autor: Klever López)                           (Autora: Ángeles Zambrano)
                  │                                               │
                  ▼                                               ▼
          Pull Request #1                                 Pull Request #2
    Revisado y fusionado por:                       Revisado y fusionado por:
        Ángeles Zambrano                                 Klever López
                  │                                               │
                  └───────────────────────┬───────────────────────┘
                                          ▼
                                     Rama `main`
```

---

## 2. Detalle de Contribuciones del Equipo

| Métrica / Parámetro | Contribución 1 (Klever López) | Contribución 2 (Ángeles Zambrano) |
| :--- | :--- | :--- |
| **Repositorio** | `ajzambrano12-cloud/-cern-preparation-program-Angeles` | `ajzambrano12-cloud/-cern-preparation-program-Angeles` |
| **Rama utilizada** | `feature/limpieza-y-docs-semana03` | `feature/actualizar-cronograma-semana03` |
| **Commit hash** | `4cc9d0b` | `916265e` |
| **Pull Request** | [PR #1](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/pull/1) | [PR #2](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/pull/2) |
| **Tipo de cambio** | Refactorización de tracking y documentación | Actualización de seguimiento y trazabilidad |
| **Revisor / Merger** | Ángeles Zambrano (@ajzambrano12-cloud) | Klever López (@Klopezxd) |
| **Estado final** | `Merged` en `main` | `Merged` en `main` |

---

## 3. Respuestas al Cuestionario de Evaluación Individual (Moodle)

### 1. URL del repositorio
`https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles`

### 2. Nombre de la rama utilizada
`feature/limpieza-y-docs-semana03`

### 3. URL de tu Pull Request
`https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/pull/1`

### 4. Breve descripción de tu contribución
Saneamiento estructural del repositorio mediante la remoción de archivos `.gitkeep` redundantes en directorios que ya contaban con archivos Markdown reales (`semana-01/evidencias/` y `semana-03/evidencias/`), complementado con la actualización del archivo `semana-03/README.md` para registrar formalmente la entrada y el enlace de la Evidencia 02 dentro del índice de entregables del módulo.

### 5. Una dificultad encontrada durante el trabajo colaborativo
La configuración y seguimiento del puntero *upstream* durante el primer `push` desde la terminal local con ramas temáticas (`git push -u origin <rama>`), que requirió verificar la sincronización entre el estado local y remoto. Asimismo, la coordinación del ciclo de revisión por pares en la interfaz web de GitHub para asegurar que cada integrante validara el `diff` de código y ejecutara el `merge` sin generar bifurcaciones divergentes en la historia de la rama principal (`main`).

---

## 4. Análisis Técnico de Ingeniería de TI

### A. Anatomía y ciclo de vida de un Pull Request
A diferencia de los comandos nativos del motor Git (que gestiona commits, ramas y árboles en memoria y disco), el **Pull Request** es una primitiva de nivel superior introducida por plataformas colaborativas como GitHub. Opera como una solicitud formal de revisión de un conjunto de cambios (*changeset*), proporcionando:
1. **Inspección de diferencias (*Diff Viewer*):** Desglose línea por línea de adiciones y supresiones.
2. **Auditoría de historial:** Preservación inmutable de qué desarrollador aprobó el código y cuándo se integró.
3. **Cero fricción en el tronco central:** Los errores o cambios incompletos quedan confinados en ramas aisladas, sin impactar el código en producción ni bloquear el trabajo simultáneo de otros ingenieros.

### B. El rol de `.gitkeep` y la higiene del repositorio
Git no rastrea directorios vacíos; únicamente almacena blobs correspondientes a archivos. La convención comunitaria de incluir un archivo `.gitkeep` permite preservar la jerarquía de carpetas en repositorios iniciales. No obstante, una vez que una carpeta incorpora archivos reales (como `01-exploracion-root-nanoaod.md`), el `.gitkeep` se convierte en un remanente innecesario. Su eliminación mediante `git rm` optimiza el árbol del proyecto y mantiene la higiene del código fuente.
