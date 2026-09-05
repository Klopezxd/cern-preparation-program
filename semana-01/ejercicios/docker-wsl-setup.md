# Guía de Instalación: Docker Engine Nativo + Lazydocker en WSL 2 (Ubuntu)

Guía paso a paso para configurar Docker nativo en WSL 2 sin depender de Docker Desktop, solucionando de raíz los problemas comunes de namespaces y sockets UNIX mediante TCP local (`127.0.0.1:2375`).

> **Recomendación:** ejecuta todos los pasos desde la consola nativa de WSL (abre "Ubuntu" directo desde el menú Inicio o Windows Terminal), no desde Warp u otro emulador con capas de autocompletado/IA. Evitas dolores de cabeza con grupos de usuario y permisos que no se refrescan bien.

---

## 1. Requisitos Previos

Verificar que WSL 2 tenga `systemd` habilitado. La forma más rápida es comprobar directamente si ya está activo como PID 1 (paso siguiente); si la comprobación falla, ahí sí se revisa `/etc/wsl.conf` para agregar (o crear el archivo si no existe):

```ini
[boot]
systemd=true
```

Para comprobar que `systemd` está activo como PID 1:

```bash
ps -p 1 -o comm=
# Debe responder: systemd
```

---

## 2. Instalación de Docker Engine y Containerd

Instalar los paquetes base desde los repositorios oficiales de Ubuntu:

```bash
sudo apt update
sudo apt install -y docker.io containerd
sudo usermod -aG docker $USER
```

---

## 3. Configuración para Evitar Conflictos de Namespaces en WSL

WSL 2 puede aislar los sockets UNIX (`/run/docker.sock`) entre sesiones interactivas y servicios del sistema. La solución definitiva es exponer el demonio localmente en `127.0.0.1:2375`.

### A. Configurar `daemon.json`

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<'EOF'
{
  "hosts": ["unix:///run/docker.sock", "tcp://127.0.0.1:2375"]
}
EOF
```

### B. Crear override de Systemd

Evita que el servicio por defecto duplique flags de host:

```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo tee /etc/systemd/system/docker.service.d/override.conf <<'EOF'
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --containerd=/run/containerd/containerd.sock
EOF
```

### C. Recargar y reiniciar el servicio

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now docker
sudo systemctl restart docker
```

---

## 4. Configuración del Entorno de Usuario

Indicar al cliente CLI de Docker que se conecte a través del puerto local:

```bash
echo 'export DOCKER_HOST=tcp://127.0.0.1:2375' >> ~/.bashrc
export DOCKER_HOST=tcp://127.0.0.1:2375
```

### Comprobar funcionamiento

```bash
docker ps
docker run --rm hello-world
```

---

## 5. Instalación de Lazydocker (Interfaz Gráfica TUI)

Instalar la herramienta visual para la terminal:

```bash
curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
sudo mv ~/.local/bin/lazydocker /usr/local/bin/
```

Ejecutar:

```bash
lazydocker
```

---

## 6. Atajos Rápidos de Lazydocker

| Tecla | Acción |
|---|---|
| `h, j, k, l` o Flechas | Navegación entre paneles y elementos |
| `Enter` | Ver logs/detalles del contenedor seleccionado |
| `x` | Menú de acciones rápidas (iniciar, pausar, reiniciar, matar) |
| `d` | Eliminar recurso seleccionado |
| `m` | Ver métricas de CPU y memoria en tiempo real |
| `q` | Salir de Lazydocker |

---

## 7. Notas y Seguridad

- **WSL vs. Warp**: todo se instala y corre en WSL (Ubuntu); Warp es solo el emulador de terminal usado para escribir los comandos, no instala nada por su cuenta. Su capa de autocompletado a veces no refresca bien grupos de usuario o sesiones recientes, así que si `docker ps` o los permisos se comportan raro, prueba primero desde la consola nativa de WSL para descartar interferencias de Warp.
- **Riesgo del puerto TCP**: `127.0.0.1:2375` no tiene autenticación ni TLS. Solo es alcanzable desde procesos locales de esta máquina, pero cualquiera de ellos tendría control total de Docker (y por tanto, acceso root de facto). No exponer este puerto a la red.
