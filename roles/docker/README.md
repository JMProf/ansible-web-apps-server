## 📦 Rol: `docker`

Este rol instala y configura Docker en sistemas basados en Debian/Ubuntu. Incluye la instalación de Docker Engine, las dependencias necesarias y la configuración básica del servicio.

### ✔️ Funcionalidades

- Instala los paquetes:
  - `docker.io`
  - `python3-docker`
  - `docker-compose`
- Asegura que el servicio **Docker** esté activo y habilitado al inicio.
- Añade el usuario que ejecuta Ansible (`ansible_user`) al grupo `docker`, permitiendo usar Docker sin privilegios de superusuario.

### 📝 Notas

- Este rol está diseñado para sistemas basados en APT (Debian/Ubuntu).

- Es necesario que el usuario cierre y abra sesión para que se aplique su pertenencia al grupo docker.