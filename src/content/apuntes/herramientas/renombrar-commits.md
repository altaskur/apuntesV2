---
title: 'Renombrar Commits'
description: ''
pubDate: 'July 31 2023'
updatedDate: 'July 31 2023'
tags:
  - Git
  - Development
categories:
    - Herramientas
---
## ¿Cómo renombrar los commits?

Si queremos renombrar el último commit podemos utilizar el comando `git commit --amend`,
una vez ejecutado el comando, se nos abrirá el editor de texto que tengamos configurado en git.

Si queremos renombrar un commit anterior, tenemos que usar rebase para reescribir la historia de nuestro repositorio.

## ¿Cómo se utiliza rebase?

> Para utilizar el rebase, tenemos que situarnos en el commit anterior al que queremos modificar.

### ¿Cómo navegamos por los commits?

para indicarle a rebase cual es el commit anterior al que queremos modificar, primero listaremos todos los commits existentes, con el comando `git log`. Nos encontraremos algo parecido a:

```bash
    commit 06706d1054asdfsc773c9262f76d9aeba5596e6d
    Author: Altaskur <@users.noreply.github.com>
    Date:   Sun Jul 30 11:41:27 2023 +0200

    feat: :sparkles: Add password encrypt logic
```

El hash nos sale a partir de la palabra `commit`, seria lo que tenemos que indicarle a rebase.

```bash
    git rebase -i 06706d1054asdfsc773c9262f76d9aeba5596e6d
```

### ¿Cómo renombramos el commit?

Una vez ejecutado el comando, se nos abrirá el editor de texto que tengamos configurado en git, y nos mostrará algo parecido a:

```bash
    pick 06706d1 feat: :sparkles: Add password encrypt logic
```

Para poder modificar el nombre del commit, cambiaremos la palabra `pick` por `edit`

```bash
    edit 06706d1 feat: :sparkles: Add password encrypt logic
```

Ahora si todo va bien, el propio Git nos indicará que ya podemos realizar el cambio del nombre del commit.

```bash
    git commit --amend
```

Comprobamos que se ha realizado el cambio correctamente con el comando `git log`.
y salimos del rebase con el comando `git rebase --continue`.

```bash
    git rebase --continue
```

## ¿Cómo subimos los cambios al repositorio remoto?

Para subir los cambios al repositorio, tan sólo tenemos que ejecutar el comando `git push --force`.

```bash
    git push --force
```
