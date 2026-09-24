# Evidencia 1 — Primera Contribución Open Source

* **Módulo:** [1.2 GitHub — First Contributions](https://github.com/firstcontributions/first-contributions) | **Fecha:** 23 de septiembre de 2026

> **Objetivo:** Experimentar de manera práctica y rigurosa el flujo de contribución distribuida de código abierto (*Forking Workflow*) en un repositorio público global, implementando la derivación de repositorio (*fork*), aislamiento en rama de características (*feature branch*), confirmación atómica bajo *Conventional Commits*, superación de solicitudes de cambio (*Requested Changes*) emitidas por pipelines automatizados de CI/CD (GitHub Actions) e integración final (*merge*) hacia la rama principal del proyecto.

---

## 1. Arquitectura del Flujo de Trabajo (*Forking Workflow*)

A diferencia de los entornos cerrados de trabajo en equipo (donde los colaboradores comparten permisos de escritura directa sobre el mismo repositorio), los proyectos de código abierto a nivel global operan bajo el **modelo de bifurcación (*Forking Workflow*)**. Este estándar protege la integridad de la base de código original frente a contribuciones no autorizadas, delegando la revisión a mantenedores o a pipelines de integración continua.

```text
 ┌─────────────────────────────────────────────────────────────────────────────┐
 │            REPOSITORIO CENTRAL UPSTREAM (firstcontributions)               │
 │                               Rama: main                                   │
 └──────────────────────────────────────┬──────────────────────────────────────┘
                                        │
                         [ Fork ]       │  [ Pull Request #125406 ]
                            │           │  (Aprobado y fusionado por CI/CD Bot)
                            ▼           │
 ┌──────────────────────────────────────┴──────────────────────────────────────┐
 │                REPOSITORIO FORK REMOTO (Klopezxd)                           │
 │                               Rama: ramita                                  │
 └──────────────────────────────────────▲──────────────────────────────────────┘
                                        │
                         [ git push --force origin ]
                                        │
 ┌──────────────────────────────────────┴──────────────────────────────────────┐
 │                     ESTACIÓN DE TRABAJO LOCAL (WSL 2 / Host)                │
 │       • git reset --hard (saneamiento de diff)                              │
 │       • git commit -am "docs: add Klever Lopez to contributors list"        │
 │       • git pull upstream main (sincronización de ciclo cerrado)           │
 └─────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Registro Técnico de la Contribución

| Parámetro / Métrica | Detalle de la Operación |
| :--- | :--- |
| **Proyecto Original (*Upstream*)** | [`firstcontributions/first-contributions`](https://github.com/firstcontributions/first-contributions) |
| **Repositorio Derivado (*Fork*)** | [`Klopezxd/first-contributions`](https://github.com/Klopezxd/first-contributions) |
| **Rama de Característica** | `ramita` |
| **Pull Request Oficial** | [PR #125406: docs: add Klever Lopez to contributors list](https://github.com/firstcontributions/first-contributions/pull/125406) |
| **Commit en Rama Local** | `a4fca35` (*docs: add Klever Lopez to contributors list*) |
| **Commit de Integración en Main** | [`16a2965`](https://github.com/firstcontributions/first-contributions/commit/16a2965445209ea9ba395ca00eb0bead28ea4e4d) |
| **Archivo Modificado** | `Contributors.md` (Línea 101) |
| **Resultado de Verificación CI/CD** | `github-actions[bot]` ➔ `All checks passed` ➔ `Auto-merge successful` |
| **Estado Final** | **Closed & Merged** en `main` |

---

## 3. Respuestas al Cuestionario de Evaluación Oficial (Moodle)

### 3.1. Proyecto
La actividad práctica se ejecutó sobre el proyecto de código abierto **First Contributions** ([`firstcontributions/first-contributions`](https://github.com/firstcontributions/first-contributions)), un repositorio pedagógico global diseñado para estandarizar la incorporación de desarrolladores a comunidades abiertas mediante la validación automatizada de contribuciones.

### 3.2. Pull Request
* **Enlace público al Pull Request:** [`https://github.com/firstcontributions/first-contributions/pull/125406`](https://github.com/firstcontributions/first-contributions/pull/125406)
* **Estado:** Fusionado exitosamente (*Merged*) en la rama `main` mediante el commit `16a2965`.

### 3.3. Flujo de Trabajo
El procedimiento se desarrolló terminal-first siguiendo las etapas formales del software libre:
1. **Forking:** Se generó una copia del repositorio base hacia la cuenta personal `@Klopezxd` en GitHub.
2. **Clonación local:** Se clonó el fork en un directorio satélite del entorno de trabajo local.
3. **Aislamiento en rama:** Se creó la rama temática `ramita` mediante `git switch -c ramita`, preservando intacto el branch `main`.
4. **Edición dirigida:** Se agregó la entrada `- [Klever Lopez](https://github.com/Klopezxd)` en la sección intermedia de `Contributors.md` (línea 101), acatando las directivas del proyecto para evitar colisiones concurrentes al inicio o final del archivo.
5. **Commit atómico:** Se confirmó el cambio bajo el estándar *Conventional Commits* (`docs: add Klever Lopez to contributors list`).
6. **Push remoto:** Se publicaron los objetos en la rama del fork mediante `git push -u origin ramita`.
7. **Apertura de PR y superación de revisión:** Se inició el Pull Request hacia el repositorio base, enfrentando y resolviendo una solicitud de cambios de integración continua.
8. **Sincronización:** Se configuró el remoto `upstream` y se ejecutó `git pull upstream main` para sincronizar los cambios oficiales hacia el entorno local.

### 3.4. Aprendizaje
Se consolidó la comprensión de la **gobernanza de código abierto y la integración continua (CI/CD)**:
* **El carácter "vivo" de un Pull Request:** Un PR no es una entrega estática; constituye un canal dinámico de comunicación donde cualquier nuevo push a la rama remota actualiza automáticamente la propuesta de cambio.
* **La estricta validación por bots:** En proyectos masivos, los pipelines de GitHub Actions reemplazan el triaje manual básico. Los bots exigen diffs matemáticamente atómicos (exactamente una línea neta de cambio) y bloquean el merge ante cualquier desviación de formato.
* **La preservación del upstream:** La importancia de mantener sincronizada la rama base local mediante un remoto `upstream` para reflejar la evolución del proyecto sin generar divergencias en el historial de Git.

### 3.5. Dificultad Encontrada y Resolución Técnica
La mayor fricción residió en la **alteración silenciosa de espacios en blanco (*trailing whitespace*) producida por las configuraciones automáticas del editor de código al guardar el archivo**. 

* **Incidencia:** Al guardar `Contributors.md` en el entorno gráfico, el formateador eliminó los espacios residuales de 58 líneas históricas ajenas, inflando el diff a **117 líneas modificadas** (58 eliminaciones, 58 adiciones y 1 línea propia). Esto activó un rechazo inmediato por parte de `github-actions[bot]` (*Requested Changes* por exceso de líneas).
* **Resolución técnica:** Se diagnosticó la causa raíz mediante `git diff --stat`, se reseteó la rama local al estado puro del remoto (`git reset --hard origin/main`), se insertó la línea de forma determinista aislando estrictamente la adición (+1 línea neta, 0 eliminaciones) y se actualizó la rama remota con `git push --force origin ramita`. El bot reconoció la corrección de forma autónoma, aprobó la revisión y ejecutó el merge definitivo.
