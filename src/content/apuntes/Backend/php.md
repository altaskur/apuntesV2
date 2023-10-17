---
title: 'PHP'
description: ''
pubDate: 'October 16 2023'
updatedDate: 'October 16 2023'
tags:
  - PHP
  - Web Development
categories:
    - Backend
---
## POO

Para crear una clase de PHP cómo en Java necesitamos usar class más el nombre de clase y las llaves.

```php

class Soporte{
  // tu código aquí
}
```

## Atributos de clase

Para establecer atributos de la case debemos declarar su ámbito cómo [private, public, protected] y luego el nombre del atributo. Es muy similar a Java.

```php
  class Soporte{
    private const IVA = 21;
    private float $precio;
  }
```

## Constructor

Para inicializar el constructor usaremos la palabra reservada `__construct()` y dentro de los paréntesis los parámetros que queramos inicializar.

Podemos declarar y asignar un valor dentro de los paréntesis del constructor, asignándole un valor predeterminado.

## llamar a un atributo

Para llamar a un atributo podemos hacer uso de la palabra reservada `$this` y luego el nombre del atributo.

En este ejemplo podemos ver cómo actualizar un atributo desde el constructor.

```php
  class Soporte{
    private const IVA = 21;
    private float $precio;

    public function __construct(float $precio = 0){
      $this->precio = $precio;
    }
  }
```

Pero ¿Que ocurre si el atributo es una constante Para llamar a una constante
