---
title: 'Express.js'
description: ''
pubDate: 'July 16 2023'
updatedDate: 'July 16 2023'
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

## Estructura del proyecto

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

## Aplicación simple en express.js

```js

// /app -> app.js

const express = require('express');
const cors = require('cors');

const app = express();
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

// !ATENCIÓN!
// esto sólo lo recomiendo para desarrollo
// en producción sustituir por la ruta de despliegue

const corsOptions = {
  origin: '*', // tu dirección.com o 64.255.225.2
  optionsSuccessStatus: 200,
};

app.use(cors(corsOptions));

const loggingRouter = require('../routers/iniciarSession');
const profile = require('../routers/profile');

app.use('/api/logging', loggingRouter);
app.use('/api/profile', profile);


module.exports = app;
```

```js
// /main.js
const app = require('./app/app');

require('dotenv').config();

const { env } = process;

app.listen(env.APP_PORT, () => {
  console.log(`Web server listening on port ${env.APP_PORT}`);
});
```

```env
// .env
APP_PORT=8084
JWT_SECRET= // aquí rellenar con la clave de encriptación que deses

// En el caso de tener BD incluye los datos
DB_USER
DB_HOST
DB_DATABASE
DB_PASSWORD
DB_PORT
```
