---
title: 'Conventional commits'
description: ''
pubDate: 'July 27 2023'
updatedDate: 'July 27 2023'
tags:
  - Git
  - Development
categories:
    - Herramientas
---

- [¿Qué son y para que se utiliza?](#qué-son-y-para-que-se-utiliza)
- [¿Cómo se utiliza?](#cómo-se-utiliza)
  - [Tipos](#tipos)
- [Alcance](#alcance)
- [Descripción](#descripción)
- [Body](#body)
- [!break change](#break-change)
- [Footer](#footer)
- [Extensiones para Vscode](#extensiones-para-vscode)
  - [Agradecimientos](#agradecimientos)

---

## ¿Qué son y para que se utiliza?

Conventional Commits es una convención para establecer una forma de escritura común para nuestros commits.

Gracias a esto podemos automatizar los proyectos y trabajar en equipo de una forma más eficiente.

## ¿Cómo se utiliza?

Los commits se estructuran de la siguiente forma:

```bash
<tipo>[alcance opcional]: <descripción>

[texto opcional]

[footer opcional]

```

### Tipos

Los tipos permitidos son:

- **initial commit**: El primer commit de un proyecto
- **build**: Cambios que afectan al sistema de construcción o dependencias externas (ej: gulp, broccoli, npm)
- **ci**: Cambios en nuestro sistema de integración continua (ej: Travis, Circle, BrowserStack, SauceLabs)
- **docs**: Cambios en la documentación
- **feat**: Añadir una nueva funcionalidad
- **fix**: Corregir un bug
- **perf**: Cambios que mejoran el rendimiento
- **refactor**: Cambios en el código que no corrigen un bug ni añaden una funcionalidad
- **style**: Cambios que no afectan al significado del código (espacios en blanco, formato, punto y coma, etc)
- **test**: Añadir tests faltantes o corregir los existentes

## Alcance

debe de ser un sustantivo, encerrado entre paréntesis. Por ejemplo: fix(parser):.

```bash
fix(Parser): Corregir un bug en el parser
```

## Descripción

Debe de tener cómo máximo 50 caracteres, debe de comenzar con una letra en minúscula y no debe de terminar con un punto.

## Body

Pueden ser multilínea pero cada párrafo debe de estar separados por un salto de línea.

```bash
    fix: correct minor typos in code

    see the issue for details

    on typos fixed.
```

## !break change

Si el commit contiene un cambio que rompe la compatibilidad con versiones anteriores, el tipo ha de finalizar con un ! y el footer debe de establecerse con el texto `BREAKING CHANGE:` seguido de una descripción de los cambios.

```bash
    refactor!: drop support for Node 6

    BREAKING CHANGE: refactor to use JavaScript features not available in Node 6.
```

## Footer

El footer debe de contener información adicional sobre el commit, por ejemplo:

- **Closes**: Para indicar que el commit cierra una issue
- **Refs**: Para indicar que el commit hace referencia a una issue
- **Reviewed** o **Tested**: Para indicar que el commit ha sido revisado o testado y especificamos por quién.
- **BREAKING CHANGE**: Para indicar que el commit contiene un cambio que rompe la compatibilidad con versiones anteriores

```bash
    closes #123

    refs #123

    reviewed-by: @username

    BREAKING CHANGE: drop support for Node 6
```

## Extensiones para Vscode

- [Conventional Commits](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits)

### Agradecimientos

- [vamoacodear](https://github.com/nsdonato)
