## 🌐 Rol: `nginx_proxy_manager`

Este rol despliega **Nginx Proxy Manager (NPM)** utilizando Docker, creando una red dedicada para servicios expuestos mediante proxy y conectando Portainer a dicha red. El rol gestiona la infraestructura necesaria para tener un proxy inverso funcional y preparado para certificados SSL.

### ✔️ Funcionalidades

- Crea una red Docker de tipo `bridge`.
- Asigna una configuración IP específica mediante `ipam_config`.
- Garantiza que la red esté presente antes de conectar contenedores.
- Conecta Portainer tanto a la red `bridge` como a `proxy_network`.
- Inicia el contenedor `npm` desde la imagen `jc21/nginx-proxy-manager:latest`.
- Conecta NPM a la red `proxy_network`.

### 📝 Notas importantes

- Este rol requiere de Docker previamente instalado y funcionando.

- Si no quieres utilizar Portainer puede eliminar la segunda tarea del fichero `tasks/main.yml`.