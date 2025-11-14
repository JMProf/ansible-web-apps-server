## 📦 Rol: `volumen_npm`

Este rol restaura el contenido del volumen de **Nginx Proxy Manager (NPM)** a partir de un archivo comprimido ubicado en la carpeta `files` del rol.  
Automatiza todo el proceso: detección del archivo, copia, parada del contenedor, restauración del volumen y arranque del servicio.

En el archivo comprimido debe encontrarse la carpeta `_data` con los ficheros del volumen de NPM que deseas reemplazar.

### ✔️ Funcionalidades

- Busca en `roles/<rol>/files/` un fichero con extensión `.tar.gz`, `.zip`, `.tar`, `.tgz`. Selecciona el primero que encuentre y obtiene su nombre, por lo que no requiere especificar manualmente el archivo.
- Transfiere el archivo comprimido al directorio donde se encuentra el volumen (`ruta_volumen`). Esta variable puede editarse en el fichero `/vars/main.yml`, aunque no debería ser necesario.
- Detiene el contenedor `npm` para evitar corrupción de datos durante la restauración.
- Borra el volumen de NPM.
- Descomprime el archivo copiado restaurando así toda la estructura del volumen.
- Elimina el archivo comprimido una vez restaurado.
- Vuelve a iniciar el contenedor `npm`.

### 📝 Notas importantes

- El archivo comprimido debe estar dentro del directorio `files` del rol.

- El contenedor debe llamarse npm; si usas otro nombre, deberás parametrizarlo.

- Si el volumen contiene configuraciones SSL, estas se restaurarán junto al resto de datos.