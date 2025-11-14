## 🐳 Rol: `portainer`

Este rol despliega Portainer CE usando Docker, creando el volumen necesario y lanzando el contenedor con la configuración recomendada.

### ✔️ Funcionalidades

- Crea (si no existe) el volumen `portainer_data` para almacenar la configuración persistente de Portainer.
- Despliega el contenedor `portainer` con:
  - Imagen: `portainer/portainer-ce:latest`
  - Política de reinicio: `always`
  - Puertos expuestos:
    - `9443` (interfaz web segura)
    - `8000` (agente/edge)
  - Volúmenes:
    - `/var/run/docker.sock` para gestionar Docker desde Portainer.
    - `portainer_data:/data` para persistencia.
- Garantiza que el contenedor esté siempre en estado `started`.

### 📝 Notas

- Este rol requiere que Docker esté previamente instalado y funcionando en el host.

- Portainer quedará accesible en `https://IP-PÚBLICA:9443`.

- El volumen `portainer_data` asegura que la configuración se mantenga incluso si el contenedor se recrea.