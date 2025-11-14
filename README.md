# Despliegue automático de un servidor de aplicaciones web con Ansible

Ansible es una herramienta de automatización de código abierto que permite la gestión y configuración de sistemas, aplicaciones y redes de manera sencilla y eficiente. Utiliza un enfoque basado en infraestructura como código (IaC), lo que permite definir configuraciones y despliegues y este se encargará de realizar las operaciones necesarias para lograr dicha configuración.

Ansible utiliza **playbooks** para definir y ejecutar tareas de automatización de forma ordenada y reproducible. Además, organiza estas tareas en **roles**, que permiten agrupar playbooks, variables, plantillas y archivos relacionados, facilitando la reutilización y el mantenimiento de la infraestructura.

### Roles

Este repositorio incluye los roles necesarios para el despliegue básico de uno o varios servidores de aplicaciones web mediante docker. Los roles permiten mantener una separación entre los diferentes niveles de configuración, por lo que es posible ejecutar únicamente los roles deseados para nuestro servidor. Cada rol situado en la carpeta "roles" contiene un archivo `README.md` con la información necesaria para utilizarlo, por lo que se aconseja leerlos antes de ejecutar el rol.

Los roles realizan las siguientes tareas:

- Rol `docker`: instala docker, docker-compose y python3-docker. Necesarios para ejecutar el resto de roles.
- Rol `ddns`: instala un contenedor que actualiza registros DNS en Cloudflare con la IP pública que tenga el servidor.
- Rol `portainer`: instala Portainer CE, un contenedor para administrar docker mediante un interfaz web.
- Rol `nginx_proxy_manager`: instala Nginx Proxy Manager (NPM), un proxy reversible para administrar conexiones seguras a las aplicaciones del servidor. También crea una red nueva para conectar Portainer y NPM.
- Rol `volumen_npm`: sobreescribe el volumen "npm_data" de NPM con una copia que tengamos en un fichero comprimido.

### Instalación y uso

1. Instala Ansible:

```Shell
sudo apt update
sudo apt install ansible
```
2. Descarga el repositorio:

```Shell
git clone https://github.com/JMProf/app-server-con-ansible
cd app-server-con-ansible
```

3. Edita el fichero `hosts.ini` con el servidor o servidores sobre los que quieras ejecutar los roles.

4. Si vas a utilizar el rol `ddns` debes editar el fichero `roles/ddns/vars/main.yml` para ajustar las variables de tu dominio de Cloudflare. Descomenta el rol en `despliegue.yml`.

5. Si vas a utilizar el rol `volumen_npm`debes incluir en la carpeta `roles/volumen_npmn/files/` el archivo comprimido con la `_data` correspondiente al volumen que quieras utilizar de NPM. Descomenta el rol en `despliegue.yml`.

6. Edita el fichero `despliegue.yml` para añadir o eliminar los roles deseados y lanza el *playbook*:

```Shell
ansible-playbook -i hosts.ini despliegue.yml
```