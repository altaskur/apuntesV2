---
title: 'Cambiar el usuario de los commits'
description: ''
pubDate: 'July 31 2023'
updatedDate: 'July 31 2023'
tags:
  - Git
  - Development
categories:
    - Herramientas
---

---

- [¿Cómo cambiar el usuario de los commits?](#cómo-cambiar-el-usuario-de-los-commits)
- [Referencias](#referencias)
- [Agradecimientos](#agradecimientos)

---

## ¿Cómo cambiar el usuario de los commits?

En este ejemplo vamos a ver cómo cambiar el usuario y el email de todos los commits, de una rama.
El script es un .sh, asi que asegúrate de tener un entrono Unix apropiado.

> Asegúrate de cambiar los campos de OLD_EMAIL, CORRECT_NAME y CORRECT_EMAIL.

Lo que hace el script, ejecutar git filter-branch, y para cada commit, comprueba si el email del autor o del commiter es el que queremos cambiar, y si es así, lo cambia.

```bash

#!/bin/sh

git filter-branch --env-filter '
OLD_EMAIL="Tu antiguo email"
CORRECT_NAME="Tu nombre"
CORRECT_EMAIL="Tu nuevo email"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags

```

## Referencias

- [StackOverflow](https://stackoverflow.com/questions/750172/how-do-i-change-the-author-and-committer-name-email-for-multiple-commits)

## Agradecimientos

- [xoxefdp](https://github.com/xoxefdp)
