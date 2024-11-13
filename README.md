# My Own Media Server

[![deploy-docs](https://github.com/Jordilavila/myownmediaserver/actions/workflows/deploy-docs.yml/badge.svg?branch=main)](https://github.com/Jordilavila/myownmediaserver/actions/workflows/deploy-docs.yml)

Este repositorio surge a razón de una petición que me hace la [RITSI](https://ritsi.org/) sobre la realizar una formación sobre servidores y su gestión. A lo largo de este repositorio se verá cómo conectar un disco duro en red a nuestro servidor y cómo crear un servidor multimedia con Jellyfin.

El autor de esta formación soy yo, [Jordi S. Enríquez](https://cv.elcontent.es), y la he realizado en base a mis conocimientos y experiencias. Al momento en el que redacto esta web, soy estudiante del Grado en Ingeniería Informática en la Universitat d'Alacant y el actual Coordinador de Infraestructuras y Comunicaciones de la RITSI.

Esta formación se enfoca a que el usuario tenga un primer contacto con la gestión de servidores y la creación de servicios en los mismos. Además, se podrá poner en práctica mediante una Raspberry Pi, aunque no es necesario para la realización de la formación. Para la realización de la formación se utilizará una máquina virtual con Debian 12 (en la Raspberry Pi se usaría Raspberry Pi OS, que se basa en este mismo sistema), aunque se puede utilizar cualquier otra distribución de Linux teniendo en cuenta los cambios que pueda haber.

![RITSI_logo_grande_horizontal](docs/1710_Imagotipo_Degradado_Horizontal.png)

Pero antes que nada, un poquito de historia:

Debian es un sistema operativo libre desarrollado por miles de voluntarios de todo el mundo que colaboran a través de Internet. Debian se caracteriza por no tener las últimas novedades en GNU/Linux, pero sí tener el sistema operativo más estable posible.

Debian nace en el 1993 de la mano del proyecto Debian, con la intención de crear un sistema GNU con Linux como núcleo. A día de hoy, hay muchos sistemas operativos basados en Debian, como podrían ser Ubuntu, Mint DE o Raspberry Pi OS.

El fundador del proyecto Debian fue Ian Murdock, quien escribió el manifiesto de Debian. En este documento, los puntos más destacables son: mantener la distribución de manera abierta, coherente a la filosofía del núcleo Linux y de GNU.

¿Y de donde viene el nombre? Pues su nombre viene de la combinación del nombre de quien era su pareja y futura esposa, Deborah, con el suyo, Ian, formando el acrónimo Debian.
Finalmente, la primera versión 1.x de Debian fue lanzada en 1996.

## Estructura

La estructura de este repositorio es la siguiente:

```
.
├── .github
│   ├── workflows
│   │   ├── auto-prerelease.yml
│   │   ├── auto-release.yml
│   │   ├── deploy-docs.yml
│   │   └── telegram-notify-issues.yml
│   ├── ISSUE_TEMPLATE
│   │   ├── bug_report.yml
│   │   ├── config.yml
│   │   ├── feature-request.yml
│   │   └── question.yml
│
├── docs
│   ├── _sidebar.md
│   ├── Desarrollo.md
│   ├── .nojekyll
│   └── README.md
│
├── .gitignore
├── LICENSE
├── package-lock.json
├── package.json
├── README.md
```

## Documentación

La documentación de este proyecto se encuentra en la carpeta `docs`. Para su redacción, se ha utilizado [Docsify](https://docsify.js.org/) con un tema personalizado.

Para visualizar la documentación en local, es necesario ejecutar el siguiente comando:

```bash
npm run docs
```

Si no tienes instalado Docsify en tu máquina, puedes hacerlo mediante el siguiente comando:

```bash
npm i docsify-cli -g
```



