---
title: 'Backend'
description: ''
pubDate: 'July 16 2023'
updatedDate: 'July 16 2023'
---

Express es un framework de node-js que nos permite levantar un servidor web.

Index

- [Librerías](#librerías)
  - [Ayudas](#ayudas)
  - [Funcionalidad](#funcionalidad)
- [Script de instalación](#script-de-instalación)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Aplicación simple en express.js](#aplicación-simple-en-expressjs)
- [Ejemplos de rutas](#ejemplos-de-rutas)
  - [Parámetros](#parámetros)
  - [Query](#query)
  - [Body](#body)
- [Referencias](#referencias)

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

Definimos las variables de entorno

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

Creamos el punto de llamada

```js
// /main.js
const app = require('./app/app');

require('dotenv').config();

const { env } = process;

app.listen(env.APP_PORT, () => {
  console.log(`Web server listening on port ${env.APP_PORT}`);
});
```

Montamos la aplicación

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

const loggingRouter = require('../routers/login');
const profile = require('../routers/profile');

app.use('/api/logging', loggingRouter);
app.use('/api/profile', profile);


module.exports = app;
```

Ahora necesitamos montar el token de la sesión

```js
// /jwt -> jwt.js

const jws = require('jsonwebtoken');
require('dotenv').config();

function generateToken( user ) {
  const payload = {
    id: user.id,
    email: user.email,
    name: user.name,
  };

  const option = {
    expiresIn: '6d',
  };

  return jws.sign(payload, process.env.JWT_SECRET, option);
}

function verifyToken(req, res, next) {

  const token = req.headers.authorization;
  if (!token) return res.status(401).send({ error: 'No token provided' });

  try {
    const decoded = jws.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    return next();
  } catch (err) {
    return res.status(401).send({ error: 'Invalid token' });
  }
}

module.exports = {
  generateToken,
  verifyToken,
};

```

Preparamos la contraseña y lo pasamos cómo middleware

```js
// /auth -> auth.js

const bcrypt = require('bcrypt');

function encriptPassword(req, res,next){
  const { password } = req.body;
  if(!password) return res.status(400).send({ error: 'Password is required' });

  bcrypt.hash(password, 10, (err, hash) => {
    if (err) return res.status(500).send({ error: 'Internal server error' });
    req.body.password = hash;
    return next();
  });
}

async function checkPassword(password, userPassword) {
  return bcrypt.compareSync(password, userPassword);
}

module.exports = {
  encriptPassword,
  checkPassword,
};

```

Una vez tenemos el token pasamos a crear la ruta de login

```js
// /routers -> login.js
const express = require('express');
const { db } = require('../database/connection');
const { generateToken } = require('../jwt/jwt');
const { checkPassword } = require('../auth/auth');

const router = express.Router();

router.post('/', async (req, res) => {
  const { email, password } = req.body;
  try {
    const user = await db.oneOrNone('SELECT * FROM users WHERE email = $1', [email]);
    if (!user) return res.status(400).send({ error: 'User not found' });
    const isPasswordValid = await checkPassword(password, user.password);
    if (!isPasswordValid) return res.status(400).send({ error: 'Invalid password' });
    const token = generateToken(user);
    return res.status(200).send({ token });
  } catch (err) {
    return res.status(500).send({ error: 'Internal server error' });
  }
});

module.exports = router;
```

Ahora creamos la ruta de profile

```js
// /routers -> profile.js

const express = require('express');
const { db } = require('../database/connection');
const { verifyToken } = require('../jwt/jwt');

const router = express.Router();

router.get('/', verifyToken, async (req, res) => {
  const { id } = req.body;
  try {
    const user = await db.oneOrNone('SELECT * FROM users WHERE id = $1', [id]);
    if (!user) return res.status(400).send({ error: 'User not found' });
    return res.status(200).send({ user });
  } catch (err) {
    return res.status(500).send({ error: 'Internal server error' });
  }
});

module.exports = router;

```

Por último creamos la conexión a la base de datos

```js
// /database -> connection.js

const pgp = require('pg-promise')();

require('dotenv').config();

const { env } = process;

const config = {
  host: env.DB_HOST,
  port: env.DB_PORT,
  database: env.DB_DATABASE,
  user: env.DB_USER,
  password: env.DB_PASSWORD,
};

const db = pgp(config);

module.exports = {
  db,
};

```

Con esto ya tenemos una aplicación básica de express.js

## Ejemplos de rutas

### Parámetros

```js
// /routers -> profile.js

router.get('/:id', verifyToken, async (req, res) => {
  const { id } = req.params;
  try {
    const user = await db.oneOrNone('SELECT * FROM users WHERE id = $1', [id]);
    if (!user) return res.status(400).send({ error: 'User not found' });
    return res.status(200).send({ user });
  } catch (err) {
    return res.status(500).send({ error: 'Internal server error' });
  }
});

```

### Query

```js
// /routers -> profile.js

router.get('/', verifyToken, async (req, res) => {
  const { id } = req.query;
  try {
    const user = await db.oneOrNone('SELECT * FROM users WHERE id = $1', [id]);
    if (!user) return res.status(400).send({ error: 'User not found' });
    return res.status(200).send({ user });
  } catch (err) {
    return res.status(500).send({ error: 'Internal server error' });
  }
});

```

### Body

```js
// /routers -> profile.js

router.post('/', verifyToken, async (req, res) => {
  const { id } = req.body;
  try {
    const user = await db.oneOrNone('SELECT * FROM users WHERE id = $1', [id]);
    if (!user) return res.status(400).send({ error: 'User not found' });
    return res.status(200).send({ user });
  } catch (err) {
    return res.status(500).send({ error: 'Internal server error' });
  }
});

```

## Referencias

- [Express.js](https://expressjs.com/)
- [JWT](https://jwt.io/)
- [Bcrypt](https://www.npmjs.com/package/bcrypt)
- [pg-promise](https://www.npmjs.com/package/pg-promise)
- [Mongoose](https://mongoosejs.com/)
- [Cors](https://www.npmjs.com/package/cors)
- [Morgan](https://www.npmjs.com/package/morgan)
- [Dotenv](https://www.npmjs.com/package/dotenv)
- [Nodemon](https://www.npmjs.com/package/nodemon)
- [Eslint](https://www.npmjs.com/package/eslint)
