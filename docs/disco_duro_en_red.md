# Montando un disco duro en red

## Introducción

En esta sección vamos a ver cómo montar un disco duro en la red. Lo ideal sería conectar un disco duro externo que no usemos a nuestra Raspberry Pi y compartirlo en la red local. De esta forma, podremos acceder a él desde cualquier dispositivo que esté conectado a nuestra red.

Lo primero que vamos a hacer es formatear el disco duro en NTFS, EXFAT o EXT4. En este caso, lo haremos en NTFS.

El disco duro que vamos a montar es un disco duro virtual.

## Creando el disco duro virtual - Linux y Windows (VirtualBox)

Para crear un disco duro virtual, vamos a seguir los siguientes pasos:

1. Abrimos VirtualBox y nos dirigimos a la pestaña de *Archivo*.
2. Seleccionamos la opción de *Gestor de discos duros virtuales*.
3. Se nos abrirá una ventana nueva. Le daremos clic al botón de *Nuevo*.
4. Se nos abrirá una ventana nueva con distintas opciones. Le daremos clic a *Siguiente*.
5. En la siguiente ventana, seleccionamos el tipo de disco duro que queremos crear. En este caso, seleccionaremos *VDI (VirtualBox Disk Image)*.
6. Le daremos clic a *Siguiente*.
7. En la siguiente ventana, seleccionamos el tipo de almacenamiento que queremos. En este caso, seleccionaremos *Tamaño fijo*.
8. Le daremos clic a *Siguiente*.
9. En la siguiente ventana, seleccionamos el tamaño del disco duro. En este caso, seleccionaremos 20 GB.
10. Le daremos clic a *Siguiente*.
11. En la siguiente ventana, seleccionamos la ubicación y el nombre del disco duro. Le daremos clic a *Crear*.
12. Una vez creado el disco duro, le daremos clic a *Aceptar*.

Tras seguir estos pasos, ya tendremos creado nuestro disco duro virtual.

## Particionado y rutas

Suponiendo que hemos conectado el disco duro, ejecutamos el comando ```sudo blkid``` para ver la información de las particiones y nos anotamos el UUID de la partición del disco duro que vamos a usar en la red. En mi caso es SDA1.

En función del tipo de partición necesitaremos un software u otro:

```bash
### NTFS
sudo apt install ntfs-3g -y

### ExFAT
sudo apt install exfat-utils -y
```

Tras las instalaciones y anotaciones pertinentes, podemos comprobar las particiones mediante el comando ```sudo fdisk -l```.

Un paso importante va a ser el siguiente. Tenemos que crear la carpeta donde montaremos el disco duro y procederemos a montarlo:

```bash
sudo mkdir /media/HDDRED
sudo mount /dev/sda1 /media/HDDRED
```

Tras el montaje nos movemos al directorio en cuestión con un comando ```cd /media/HDDRED``` y listamos el disco duro, que si lo acabamos de formatear, evidentemente, no habrá nada:

```bash
ls -lrth
```

(Puede que imprima algunos directorios de configuración que crea Windows por defecto)

Ahora nos toca darle los permisos adecuados:

```bash
sudo chmod 755 /media/HDDRED
```

### Automontaje

El automontaje de un disco duro es un paso interesante. Mientras que Windows lo hace él solo, Linux necesita que le digas que quieres montar ese disco. Vamos a ello:

```bash
sudo nano /etc/fstab
```

¿Recuerdas que habías copiado el UUID del disco duro en los pasos anteriores? Pues añade esta línea al final del archivo:

```bash
UUID=EL_UUID_DE_TU_HDD /media/HDDRED ntfs defaults 0 0
```

Eso sí, si tu formato de disco es distinto a NTFS, tendrás que cambiarlo por el que sea: ExFAT (exfat), EXT4 (ext4), etc.

Tras esto, comprobamos que el fichero está bien con el comando ```sudo mount -a```. En caso de no dar ningún error, es que todo está correcto y puedes reiniciar.

Este disco duro se montará automáticamente siempre que permanezca inalterado. Es decir, siempre que no lo formateemos o que borremos particiones o cualquier cosa relacionada.

## Instalación y configuración de SAMBA

Lo primero que haremos será instalar SAMBA:

```bash
sudo apt install samba samba-common -y
```

Tras la instalación de SAMBA tendremos que añadir la configuración pertinente para el disco duro. Para ello abrimos el archivo ```/etc/samba/smb.conf``` y añadimos lo siguiente al final del mismo:

```bash
[hddred]
  comment = Disco duro multimedia en red
  path = /media/HDDRED
  browseable = Yes
  writeable = Yes
  only guest = no
  create mask = 0750
  directory mask = 0750
  public = Yes
```

Tras configurar el directorio a compartir, tendremos que cambiar la contraseña de SAMBA: ```sudo smbpasswd -a jamesbond```

Tras final la configuración de SAMBA en nuestra máquina, reiniciamos el servicio:

```bash
sudo systemctl restart smbd
```

## Acceso al disco duro en red

Para acceder al disco duro en red, abrimos el explorador de archivos de nuestra máquina host y escribimos en la barra de direcciones ```\\IP_VM``` y nos pedirá las credenciales de acceso. Introducimos el usuario y la contraseña que hemos configurado en el paso anterior y ya podremos acceder al disco duro en red.
