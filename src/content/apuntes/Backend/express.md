---
title: 'Express.js'
description: ''
pubDate: '15/07/2023'
updatedDate: '15/07/2023'
tags:
  - JavaScript
  - Web Development
categories:
    - Backend
---

Express es un framework de node-js que nos permite levantar un servidor web.

Index

[Librerías](#librerías)
[Instalación](#script-de-instalación)
[Estructura de Fichero](#estructura-de-fichero)

## Librerías

Estas són las librerías que  considero básicas

### Ayudas

1. Morgan
2. dotenv
3. nodemon
4. eslint

### Funcionalidad

1. bcrypt
2. cors
3. jsonwebtoken
4. pg-promise | mongoose ( Depende de la BD a gestionar )

## Script de instalación

Por lo tanto te dejo el script para generar el proyecto fácilmente

```bash
npm install morgan dotenv nodemon bcrypt cors jsonwebtoken cors eslint
```

## Estructura de fichero

- bd
- src
  - app
  - auth
  - controller
  - database
  - jwt
  - routers
  - main
- .env

