
# My Own Media Server

Este repositorio surge de la petición de la [RITSI](https://ritsi.org/) sobre la realización de una formación sobre servidores y su gestión. A lo largo de este repositorio se verá cómo conectar un disco duro en red a nuestro servidor y cómo crear un servidor multimedia con Jellyfin.

Esta formación se enfoca a que el usuario tenga un primer contacto con la gestión de servidores y la creación de servicios en los mismos. Además, se podrá poner en práctica mediante una Raspberry Pi, aunque no es necesario para la realización de la formación. Para la realización de la formación se utilizará una máquina virtual con Debian 12 (en la Raspberry Pi se usaría Raspberry Pi OS, que se basa en este mismo sistema), aunque se puede utilizar cualquier otra distribución de Linux teniendo en cuenta los cambios que pueda haber.

Pero antes que nada, un poquito de historia:

Debian es un sistema operativo libre desarrollado por miles de voluntarios de todo el mundo que colaboran a través de Internet. Debian se caracteriza por no tener las últimas novedades en GNU/Linux, pero sí tener el sistema operativo más estable posible.

Debian nace en el 1993 de la mano del proyecto Debian, con la intención de crear un sistema GNU con Linux como núcleo. A día de hoy, hay muchos sistemas operativos basados en Debian, como podrían ser Ubuntu, Mint DE o Raspberry Pi OS.

El fundador del proyecto Debian fue Ian Murdock, quien escribió el manifiesto de Debian. En este documento, los puntos más destacables son: mantener la distribución de manera abierta, coherente a la filosofía del núcleo Linux y de GNU.

¿Y de donde viene el nombre? Pues su nombre viene de la combinación del nombre de quien era su pareja y futura esposa, Deborah, con el suyo, Ian, formando el acrónimo Debian.
Finalmente, la primera versión 1.x de Debian fue lanzada en 1996.

Una vez ya conocemos las curiosidades del sistema operativo que tenemos entre manos, ¡vamos al lío!

## Índice

PDTE.

## Creando la máquina virtual

### Descarga de Debian 12

Para la realización de la formación se utilizará una máquina virtual con Debian 12. Para ello, se puede descargar la imagen de la [página oficial de Debian](https://www.debian.org/distrib/netinst). Se recomienda descargar la versión de 64 bits **sin** entorno gráfico.

### Características de la máquina virtual

Para la realización de la formación se recomienda tener una máquina virtual con las siguientes características:
- 4 GB de RAM
- 2 núcleos de CPU
- 20 GB de almacenamiento
- Un disco duro adicional de 20 GB

### Creación de la máquina virtual - Linux y Windows (VirtualBox)

Es muy importante que una vez tengamos instalado VirtualBox, instalemos las Guest Additions. Las podemos encontrar en la página oficial de VirtualBox, en la sección de descargas con el nombre de "VirtualBox Guest Additions" o "VirtualBox Extension Pack".

Una vez tenemos todo instalado, vamos al lío con la creación de la máquina virtual. 

