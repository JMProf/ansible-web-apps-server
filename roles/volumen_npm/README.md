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

### 🧰 Obtener archivo comprimido

Para obtener el archivo comprimido que utiliza este rol es necesario localizar el volumen de datos de NPM. La ruta predeterminada para los volúmenes es `/var/lib/docker/volumes`, y es posible acceder como `root`, por lo que quizás necesites ejecutar previamente `sudo su`para poder moverte al directorio. 
Una vez dentro, accede al volumen de datos de NPM y verás la carpeta `_data`. Esta es la carpeta a comprimir. Puedes hacerlo con el siguiente comando:

```Shell
tar -czvf volumen_npm.tar.gz _data
```

Para descargarlo posteriormente, muévelo a la `home` del usuario con el que realices la conexión SSH:

```Shell
mv volumen_npm.tar.gz ~
```

Una vez hecho, es el momento de descargar el fichero al ordenador local con SCP. Para ello ejecuta el siguiente comando desde una terminal:

```Shell
scp -i CLAVE.pem USUARIO@IP:volumen_npm.tar.gz .
```

Con esto ya tendrás la copia del volumen de datos en tu ordenador y podrás guardarlo en la carpeta `files` del rol cuando lo ejecutes.
