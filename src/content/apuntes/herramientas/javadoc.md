---
title: 'JavaDoc - Documentación de código'
description: ''
pubDate: 'August 10 2023'
updatedDate: 'August 10 2023'
tags:
  - Java
  - Development
categories:
    - Herramientas
---

## ¿Qué es JavaDoc?

JavaDoc es una herramienta que nos permite generar documentación de nuestro código Java.
En resultado es un conjunto de páginas HTML que contienen la documentación de las clases y métodos de nuestro código, similar a la documentación de la API de Java.
Se genera a partir de comentarios que se escriben en el código fuente.

## Beneficios

Documentar nuestro código es importante para que otras personas puedan entenderlo y utilizarlo, y para que nosotros mismos podamos recordar cómo funciona.
JavaDoc nos permite generar documentación de nuestro código de forma automática, y mostrarla en un formato HTML que es fácil de leer y navegar, de forma similar a la documentación de la API de Java, lo que facilita su comprensión y uso.

## Convenciones

Para que JavaDoc pueda generar la documentación de nuestro código, debemos seguir las siguientes convenciones:

Los comentarios deberían estar escritos en inglés. ya que es el idioma más utilizado en el desarrollo de software y sea entendible por la mayoría de las personas.
Es importante que los comentarios estén escritos en la línea anterior al elemento que documentan, ya que si están escritos en la misma línea, el elemento no se documentará.
Los comentarios de documentación deben comenzar con `/**` y terminar con `*/`, dentro de estos debería haber una descripción del elemento que documentan, y etiquetas que describan el elemento,
cómo `@param` para los parámetros, `@return` para el valor de retorno, `@throws` para las excepciones, también debería haber una etiqueta `@version` que indique la versión del elemento que documentan y una etiqueta `@author`.

Para escribir

## ¿Cómo se utiliza?

Para generar la documentación de nuestro código Java, una vez tenemos los comentarios de documentación, depende del IDE que estemos utilizando, pero en general se puede hacer de la siguiente forma:

### NetBeans

En NetBeans, para generar la documentación de nuestro código, debemos ir a la pestaña `Run` y seleccionar la opción `Generate Javadoc...`, se abrirá una ventana donde podemos configurar la generación de la documentación, y luego de hacer clic en el botón `OK`, se generará la documentación en el directorio especificado.

### IntelliJ IDEA

En IntelliJ IDEA, para generar la documentación de nuestro código, debemos ir a la pestaña `Tools` y seleccionar la opción `Generate JavaDoc...`, se abrirá una ventana donde podemos configurar la generación de la documentación, y luego de hacer clic en el botón `OK`, se generará la documentación en el directorio especificado.

Cómo alternativa, podemos utilizar el comando `javadoc` desde la terminal, usando la siguiente sintaxis:

```bash
javadoc -d <directorio> <paquete>
```

Al final del documento te dejo un ejemplo de código comentado para que puedas ver y probar cómo funciona JavaDoc.

```bash
javadoc -d <directorio> <paquete>
```

Donde:

- `-d <directorio>`: Especifica el directorio donde se generará la documentación.
- `<paquete>`: Especifica el paquete donde se encuentra el código fuente.
- `<directorio>` Especifica el directorio donde se generará la documentación.

## Etiquetas

Las etiquetas son palabras que comienzan con `@` y se utilizan para describir los elementos que documentan te dejo una lista de las etiquetas más utilizadas:
esta lista las ha sacado Copilot pero puedes ver más en la [documentación de JavaDoc](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html).

- `/** ... */`: Comentario de documentación.
- `/* ... */`: Comentario de bloque.
- `// ...`: Comentario de línea.
- `@param`: Descripción de un parámetro.
- `@return`: Descripción del valor de retorno.
- `@throws`: Descripción de una excepción.
- `@deprecated`: Indica que el elemento está obsoleto.
- `@see`: Referencia a otro elemento.
- `@author`: Autor.
- `@version`: Versión.
- `@inheritDoc`: Hereda la documentación de la clase padre.
- `@link`: Enlace a otro elemento.s

## Ejemplo

```java
/**
 * Clase que representa un punto en el plano.
 * @version 1.0
 * @altaskur
 */

public class Punto {

    /**
     * Coordenada X del punto.
     */
    private double x;

    /**
     * Coordenada Y del punto.
     */
    private double y;

    /**
     * Constructor de la clase.
     * @param x Coordenada X del punto.
     * @param y Coordenada Y del punto.
     */
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    /**
     * Obtiene la coordenada X del punto.
     * @return Coordenada X del punto.
     */
    public double getX() {
        return x;
    }

    /**
     * Obtiene la coordenada Y del punto.
     * @return Coordenada Y del punto.
     */
    public double getY() {
        return y;
    }

    /**
     * Calcula la distancia entre dos puntos.
     * @param p Punto con el que se calcula la distancia.
     * @return Distancia entre los dos puntos.
     */
    public double distancia(Punto p) {
        return Math.sqrt(Math.pow(x - p.x, 2) + Math.pow(y - p.y, 2));
    }

    /**
     * Calcula el punto medio entre dos puntos.
     * @param p Punto con el que se calcula el punto medio.
     * @return Punto medio entre los dos puntos.
     */
    public Punto puntoMedio(Punto p) {
        return new Punto((x + p.x) / 2, (y + p.y) / 2);
    }

    /**
     * Comprueba si dos puntos son iguales.
     * @param p Punto con el que se compara.
     * @return True si los puntos son iguales, false en caso contrario.
     */
    public boolean equals(Punto p) {
        return x == p.x && y == p.y;
    }

    /**
     * Obtiene una representación en cadena del punto.
     * @return Representación en cadena del punto.
     */
    @Override
    public String toString() {
        return "(" + x + ", " + y + ")";
    }
}
```

## Referencias

- [Documentación de JavaDoc](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html)
