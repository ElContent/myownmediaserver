# Creación y configuración de la máquina virtual

## Descarga de Debian 12

Para la realización de la formación se utilizará una máquina virtual con Debian 12. Para ello, se puede descargar la imagen de la [página oficial de Debian](https://www.debian.org/distrib/netinst). Se recomienda descargar la versión de 64 bits **sin** entorno gráfico.

## Características de la máquina virtual

Para la realización de la formación se recomienda tener una máquina virtual con las siguientes características:
- 4 GB de RAM
- 2 núcleos de CPU
- 20 GB de almacenamiento
- Un disco duro adicional de 20 GB

## Creación máquina virtual - Linux y Windows (VirtualBox)

Es muy importante que una vez tengamos instalado VirtualBox, instalemos las Guest Additions. Las podemos encontrar en la página oficial de VirtualBox, en la sección de descargas con el nombre de "VirtualBox Guest Additions" o "VirtualBox Extension Pack".

Una vez tenemos todo instalado, vamos al lío con la creación de la máquina virtual:

![Nueva máquina virtual](vbx_01.png)

Se nos abrirá una ventana nueva con distintas secciones y opciones. En las capturas de pantalla que siguen en el documento se muestran las secciones que sufren cambios, así como los cambios en sí. **Es muy importante no seleccionar la imagen ISO en estos pasos iniciales hasta que se indique**:

![Selección del tipo de sistema operativo](vbx_02.png)

![Selección de la memoria RAM](vbx_03.png)

![Creación de un disco duro virtual](vbx_04.png)

Una vez llegados a este punto, le daremos clic al botón *terminar*.

Ahora veremos nuestra máquina virtual creada en la pantalla inicial de la aplicación, pero no está terminada, ahora nos toca configurarla. Para ello le daremos clic al botón de configuración.

Veremos una pantalla como esta:

![Configuración de la máquina virtual](vbx_05.png)

¿Qué vamos a hacer en esta configuración? Pues bien, vamos a realizar cambios que permitan que la máquina virtual esté al mismo nivel de red que nuestra máquina host, por lo tanto, tendrá una IP en nuestra red local y será accesible desde cualquier dispositivo que esté conectado a nuestra red local. Por otra parte, vamos a revisar la configuración del portapapeles entre host e invitado y la memoria de vídeo.

![Configuración del portapapeles](vbx_06.png)

![Configuración del arranque](vbx_07.png)

![Configuración de la memoria de vídeo](vbx_08.png)

![Configuración de la red](vbx_09.png)

Una vez llegados a este punto, podemos dar clic sobre el botón aceptar para que se guarden nuestros cambios.

## Insertando el ISO de Debian 12

Ahora que ya hemos configurado nuestra máquina virtual, vamos a insertar la imagen ISO de Debian 12. Para ello, le daremos clic derecho a nuestra máquina virtual y seleccionaremos la opción de *Configuración*.

En la ventana que se nos abre, vamos a la sección de *Almacenamiento* y seleccionamos el icono del disco que está en la parte derecha de la ventana. Se nos abrirá un menú desplegable, en el cual seleccionaremos la opción de *Seleccionar un archivo de disco óptico virtual*. Buscamos la imagen ISO de Debian 12 y le damos clic en *Abrir*.

![Insertar ISO](vbx_10.png)

Una vez hecho esto, le daremos clic en *Aceptar* para que se guarden los cambios. Ahora ya podemos iniciar nuestra máquina virtual y comenzar con la [instalación de Debian 12](instalacion_so.md).

## Instalación de Debian 12

Para empezar con la instalación de Debian 12, arrancaremos la máquina virtual. Lo primero que hará será arrancar el medio de instalación con un menú que nos preguntará el tipo de instalación que queremos hacer. En nuestro caso, vamos a lo más sencillo: **instalación gráfica**.

Como la instalación es prácticamente un *siguiente*, *siguiente*, *siguiente*, sólo voy a mostrar las partes relevantes de la instalación. Y en nuestro caso será la interfaz gráfica del sistema operativo que, como ya sabemos, no hay, puesto que es un servidor:

![Instalación de Debian 12](debian_01.png)

Una vez llegados al final de la instalación y reiniciada la máquina, nos pedirá que introduzcamos el usuario y la contraseña. Una vez introducidos, ya tendremos nuestra máquina virtual con Debian 12 instalada.


### Añadimos nuestro usuario a sudo

Accedemos a la máquina virtual con nuestro usuario y contraseña y configuramos nuestro usuario. Entramos en el root: 

```bash	
su -
```

Y añadimos nuestro usuario al grupo *sudo*:

```bash
usermod -aG sudo julioiglesias
```

Finalmente, instalamos *sudo*:

```bash
apt update
apt install sudo -y
```

A partir de este momento, podremos ejecutar comandos con privilegios de superusuario. Recuerda salir del usuario root con el comando *exit*. También podemos acceder a la máquina virtual desde *PowerShell* o *CMD* con el comando *ssh*. Para ello, necesitamos la IP de la máquina virtual. Para obtenerla, ejecutamos el comando *ip a* y anotamos la IP que aparece en la interfaz de red que estemos utilizando.

```bash
ssh julioiglesias@IP
```

![SSH](debian_02.png)

### Añadimos alias para controlar mejor algunos comandos

Para controlar mejor algunos comandos, vamos a añadir unos alias a nuestro usuario. Para ello, editamos el archivo *.bash\_aliases*:

```bash
echo "alias poweroff='sudo systemctl poweroff'" > echo .bash_aliases
echo "alias reboot='sudo systemctl reboot'" >> echo .bash_aliases
source .bashrc
```

También puedes editarlo con tu editor de texto favorito, como por ejemplo *nano* o *vim*:

```bash
nano .bash_aliases
```

Y añadimos las siguientes líneas:

```bash
alias poweroff='sudo systemctl poweroff'
alias reboot='sudo systemctl reboot'
```

Con esto, podremos apagar y reiniciar la máquina con los comandos *poweroff* y *reboot* respectivamente.

### Instalación de herramientas necesarias

Para la realización de la formación, vamos a necesitar instalar algunas herramientas o, simplemente, nunca viene mal tenerlas. Para ello, ejecutamos el siguiente comando:

```bash
sudo apt install -y neofetch net-tools zip nginx curl wget git
```

Llegados a este punto ya tenemos nuestra máquina virtual con Debian 12 instalada y configurada: 

![Debian 12](debian_03.png)

Además, tenemos instalado un servidor web *nginx* que nos permitirá acceder a la máquina virtual desde cualquier dispositivo de nuestra red local. Para ello, abrimos un navegador web y escribimos la IP de la máquina virtual. En mi caso, la IP es *192.168.1.174*:

![Nginx](debian_04.png)

El servidor NGINX no lo vamos a utilizar en la formación, pero es interesante tenerlo instalado para futuros proyectos. Aun así, dejaré un reto al final de la formación en el que configuraremos el proxy inverso de NGINX para acceder a Jellyfin desde cualquier dispositivo de nuestra red local.

Con esto finalizamos la creación y configuración de la máquina virtual con Debian 12. 


