# Jellyfin

[Jellyfin](https://jellyfin.org/docs/) es un servidor multimedia que nos permite ver nuestras películas, series y música en cualquier dispositivo de nuestra red local. Es una alternativa a Plex, pero de código abierto y gratuita. En este documento se explicará cómo instalar y configurar Jellyfin en una máquina virtual con Debian 12.

Este proyecto comenzó el 8 de diciembre de 2018, cuando los cofundadores Andrew Rabert y Joshua Boniface, entre otros usuarios, acordaron bifurcar Emby como una reacción directa al cierre del desarrollo de código abierto en ese proyecto. El nombre de Jellyfin fue concebido por Rabert al día siguiente, como una referencia al streaming. El lanzamiento inicial estuvo disponible el 30 de diciembre de 2018.

## Instalación de Jellyfin

Para instalar Jellyfin en Debian 12, podemos utilizar este comando:

```bash
curl https://repo.jellyfin.org/install-debuntu.sh | sudo bash
```

Este comando descargará el script de instalación de Jellyfin y lo ejecutará con permisos de superusuario. Una vez que se complete la instalación, podremos acceder a Jellyfin desde un navegador web en la dirección `http://localhost:8096`. Pero como estamos accediendo a Jellyfin desde una máquina virtual, necesitamos acceder a la dirección IP de la máquina virtual en lugar de `localhost`. 

## Configuración de Jellyfin

Para configurar Jellyfin por primera vez tendremos que acceder a ```http://IP_MAQUINA:8096/web/index.html#!/wizardstart.html```. En esta página se nos pedirá que creemos una cuenta de administrador y que configuremos las carpetas donde Jellyfin buscará los archivos multimedia. Una vez que hayamos completado la configuración inicial, podremos comenzar a disfrutar

## Asegurando Jellyfin

Llegados a este punto, si abrimos el servicio de Jellyfin a la red pública, es importante asegurarnos de que no nos reconfiguren el servidor. Para ello, vamos a crear una regla en NGINX que proteja ese endpoint de configuración. Esto lo podemos hacer el fichero de configuración de NGINX, que se encuentra en `/etc/nginx/sites-available/default`. Añadimos la siguiente regla:

```nginx
server {
    ##
    # Resto de la configuración
    ##

    location /web/index.html#!/wizardstart.html {
        return 301;
    }
}
```

Recuerda refrescar NGINX con: 

```bash
sudo systemctl reload nginx
```

Con esta regla, si alguien intenta acceder a la página de configuración de Jellyfin, no cargarán las cosas correctamente y no podrán modificar la configuración.

## Acceso a Jellyfin desde cualquier dispositivo

Si exportamos este proyecto a una máquina real y tenemos nuestro propio dominio, podemos configurar un proxy inverso en NGINX para acceder a Jellyfin desde cualquier dispositivo de nuestra red local. Para ello, es recomendable tener un certificado SSL para proteger la conexión. Lo primero que tendremos que hacer será crear un archivo de configuración en `/etc/nginx/sites-available/jellyfin` en el que estableceremos la configuración del proxy inverso.

Este apartado es el plus de la formación, en el que se reta al lector a configurar el proxy inverso de NGINX y a aprender más sobre NGINX y SSL.

Con esto finalizamos la instalación y configuración de Jellyfin en una máquina virtual con Debian 12. Ahora podremos disfrutar de nuestras películas, series y música en cualquier dispositivo de nuestra red local.