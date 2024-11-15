# Jellyfin

[Jellyfin](https://jellyfin.org/docs/) es un servidor multimedia que nos permite ver nuestras películas, series y música en cualquier dispositivo de nuestra red local. Es una alternativa a Plex, pero de código abierto y gratuita. En este documento se explicará cómo instalar y configurar Jellyfin en una máquina virtual con Debian 12.

Este proyecto comenzó el 8 de diciembre de 2018, cuando los cofundadores Andrew Rabert y Joshua Boniface, entre otros usuarios, acordaron bifurcar Emby como una reacción directa al cierre del desarrollo de código abierto en ese proyecto. El nombre de Jellyfin fue concebido por Rabert al día siguiente, como una referencia al streaming. El lanzamiento inicial estuvo disponible el 30 de diciembre de 2018.

## Instalación de Jellyfin

Para instalar Jellyfin en Debian 12, podemos utilizar este comando:

```bash
curl https://repo.jellyfin.org/install-debuntu.sh | sudo bash
```


