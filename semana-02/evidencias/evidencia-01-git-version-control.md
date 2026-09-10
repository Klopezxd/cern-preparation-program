# Evidencia 1: Control de Versiones con Git y Flujo con GitHub

* **Participante:** Klever López
* **Programa:** Preparación para Oportunidades CERN (2026) – ESPE
* **Módulo:** Control de Versiones con Git
* **Fecha:** 7 de septiembre de 2026

---

## 1. Repositorio en GitHub

* **URL:** [https://github.com/Klopezxd/git-fundamental-practice](https://github.com/Klopezxd/git-fundamental-practice)
* **Rama principal:** `main`

---

## 2. ¿Qué aprendí?

Aprendí a utilizar correctamente los tres estados de Git: el directorio de trabajo (archivos locales), el área de preparación o staging area (`git add`) y el repositorio local (`git commit`).

Entendí que el área de preparación no es un paso de más, sino una herramienta para hacer commits ordenados y limpios. Por ejemplo, si edito una función en un script de Python y al mismo tiempo corrijo unas líneas en el README, no tengo que meter todo en un solo commit desordenado; puedo preparar y confirmar primero el código y luego la documentación con mensajes claros. Además, aprendí la utilidad de configurar un `.gitignore` desde el inicio para evitar subir archivos innecesarios como la caché de Python (`__pycache__`), entornos virtuales, archivos pesados o, muy importante, archivos sensibles (como contraseñas, llaves o variables de entorno `.env`) que jamás deberían exponerse públicamente.

---

## 3. Comando más útil o interesante

El comando que más me llamó la atención fue **`git diff`** (junto con **`git diff --staged`**).

Normalmente uno se acostumbra a usar solo `git status` para ver qué archivos cambiaron, pero `git diff` te muestra exactamente qué líneas agregaste, quitaste o modificaste dentro de cada archivo. Me pareció muy útil porque sirve como una revisión previa antes de hacer el commit, asegurando que no se suban por descuido líneas de prueba (como `print` temporales) o código incompleto.

---

## 4. Dificultad encontrada y cómo se resolvió

Al trabajar en Windows, una duda que surgió al ejecutar los commits fueron las advertencias sobre saltos de línea (`LF will be replaced by CRLF`). Al revisar la causa, entendí que se debe a la diferencia en cómo Windows y Linux manejan el fin de línea en archivos de texto, y que Git avisa que los normalizará automáticamente para que el proyecto sea compatible en cualquier sistema operativo.

También fue importante verificar que la rama local estuviera nombrada como `main` antes de vincular el repositorio remoto, para que al ejecutar `git push -u origin main` el historial subiera directamente a la rama principal de GitHub sin generar confusiones.

---

## 5. Historial de Commits

Salida de la inspección con `git log --graph --oneline --decorate`:

```text
* d887f8a (HEAD -> main, origin/main) refactor: agregar calculo de pt promedio y documentar ejecucion
* 1a0e58c feat: agregar script base de procesamiento y configurar .gitignore
* 966c772 docs: inicializar repositorio con README
```
