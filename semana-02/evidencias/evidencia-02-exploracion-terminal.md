# Evidencia 2 — Exploración de la terminal

* **Módulo:** [Software Carpentry – The Unix Shell](https://swcarpentry.github.io/shell-novice/) | **Fecha:** 9 de septiembre de 2026

> **Objetivo:** Utilizar una terminal Linux (WSL) para ejecutar operaciones fundamentales de navegación por el sistema de archivos, creación, manipulación y organización de directorios, y reflexionar sobre la eficiencia de la interfaz de línea de comandos en proyectos de desarrollo y administración de sistemas.

---

## 1. Registro de Comandos Ejecutados

Secuencia completa realizada en entorno Ubuntu sobre WSL:

```bash
# 1. Navegación e inspección inicial
mkdir -p ~/practica-terminal
cd ~/practica-terminal
pwd
ls -la

# 2. Creación y acceso al directorio de la semana
mkdir semana-02
cd semana-02
pwd

# 3. Creación e inspección de archivos
echo "# Semana 2 - Herramientas Fundamentales" > README.md
echo "Exploración de la terminal Linux y manejo de archivos." > apuntes.txt
cat README.md

# 4. Organización en subdirectorios y reubicación
mkdir ejercicios evidencias
mv apuntes.txt evidencias/

# 5. Verificación de la estructura resultante
tree
```

---

## 2. Salida en Terminal y Estructura Resultante

```text
klever@KLEVER-Victus:~$ mkdir -p ~/practica-terminal
klever@KLEVER-Victus:~$ cd ~/practica-terminal
klever@KLEVER-Victus:~/practica-terminal$ pwd
/home/klever/practica-terminal
klever@KLEVER-Victus:~/practica-terminal$ ls -la
total 8
drwxr-xr-x  2 klever klever 4096 Sep 11 23:22 .
drwxr-x--- 14 klever klever 4096 Sep 11 23:22 ..
klever@KLEVER-Victus:~/practica-terminal$ mkdir semana-02
klever@KLEVER-Victus:~/practica-terminal$ cd semana-02
klever@KLEVER-Victus:~/practica-terminal/semana-02$ pwd
/home/klever/practica-terminal/semana-02
klever@KLEVER-Victus:~/practica-terminal/semana-02$ echo "# Semana 2 - Herramientas Fundamentales" > README.md
klever@KLEVER-Victus:~/practica-terminal/semana-02$ echo "Exploración de la terminal Linux y manejo de archivos." > apuntes.txt
klever@KLEVER-Victus:~/practica-terminal/semana-02$ cat README.md
# Semana 2 - Herramientas Fundamentales
klever@KLEVER-Victus:~/practica-terminal/semana-02$ mkdir ejercicios evidencias
klever@KLEVER-Victus:~/practica-terminal/semana-02$ mv apuntes.txt evidencias/
klever@KLEVER-Victus:~/practica-terminal/semana-02$ tree
.
├── README.md
├── ejercicios
└── evidencias
    └── apuntes.txt

3 directories, 2 files
```

---

## 3. Ventajas del Uso de la Terminal en Proyectos de TI

Encuentro dos ventajas principales al utilizar la terminal:

1. **Rapidez y control:** Tareas como crear jerarquías de carpetas estructuradas, mover archivos o inspeccionar contenidos se realizan en segundos con un par de comandos directos, sin la lentitud de depender del ratón o de exploradores visuales pesados.
2. **Operación en entornos sin interfaz gráfica:** En servidores remotos (como un VPS) o entornos de desarrollo en Linux mediante WSL, no se cuenta con un escritorio gráfico; la terminal es la herramienta nativa e indispensable para administrar archivos de forma ligera, consumiendo el mínimo de recursos y asegurando que los pasos se puedan repetir fácilmente.
