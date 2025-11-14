## 🌐 Rol: `ddns`

Este rol despliega y gestiona un contenedor Docker encargado de actualizar dinámicamente un registro DNS en Cloudflare. Utiliza la imagen `oznu/cloudflare-ddns` para mantener sincronizada la IP pública del servidor con un dominio o subdominio específico.

### ✔️ Funcionalidades

- Crea o actualiza el contenedor `cloudflare-ddns`.
- Configurable mediante variables definidas en `vars/main.yml`:
  - **cloudflare_api_key** → clave de acceso a Cloudflare.
  - **cloudflare_zone** → dominio gestionado en Cloudflare.
  - **cloudflare_subdomain** → subdominio que será actualizado dinámicamente.
  - **cloudflare_proxied** → define si el registro debe pasar por el proxy de Cloudflare.

### 📝 Notas importantes

- Aunque la clave se almacena como variable en el rol, **no debe compartirse ni subirse a repositorios públicos**.
- Este rol requiere:
  - Docker funcionando en el host.
  - Una cuenta de Cloudflare con permisos API adecuados.
  - El dominio y subdominio configurados en Cloudflare.
- La imagen `oznu/cloudflare-ddns` se encargará de detectar cambios en la IP pública y actualizar automáticamente el DNS.
- Para cambiar la configuración, solo es necesario editar las variables en `vars/main.yml`.
