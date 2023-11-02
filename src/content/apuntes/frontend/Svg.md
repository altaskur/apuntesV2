---
title: 'SVG - Charla Carmen Ansio - Nuclio'
description: 'Tutorial y mejores prácticas sobre SVGator y Figma'
pubDate: 'November 1 2023'
updatedDate: 'November 2 2023'
tags:
  - SVG
  - Figma
  - SVGator
  - Design
  - Web Development
categories:
    - Frontend
    - Animación
    - Diseño
principal: false
---

- [Notas Generales](#notas-generales)
- [SVG](#svg)
  - [¿Porque su auge hoy en día?](#porque-su-auge-hoy-en-día)
  - [Agrupación de elementos](#agrupación-de-elementos)
  - [Nodos](#nodos)
  - [ViewBox y posicionamiento](#viewbox-y-posicionamiento)
  - [Fill vs Stroke](#fill-vs-stroke)
  - [Por documentar](#por-documentar)
- [Figma](#figma)
  - [Control versión](#control-versión)
  - [Regiones](#regiones)
  - [Copy to ClipBoard](#copy-to-clipboard)
- [SVGator](#svgator)
- [Recursos](#recursos)
  - [Creadores de contenido](#creadores-de-contenido)
  - [Enlaces](#enlaces)
  - [Libros](#libros)
  - [Herramientas](#herramientas)

## Notas Generales

- Existe una alternativa a GreenSock GSAP con CSS, puedes ver el perfil de [@bramus](https://twitter.com/bramus) Google DevRel.
- Otro perfil interesante es el de Amelia "water?preguntar"
- Se recomienda "guiar al usuario" a través de la web, de forma sutil ayudándolo a seguir los pasos o "historia" a través del sitio o aplicación.

    `Lo comparo al tutorial de inicio de un videojuego, dónde sin apenas indicaciones el usuario a través de pequeñas pruebas (destellos, retos etc) de forma completamente "intuitiva" va a prendiendo las mecánicas de este.`

- Existe una versión de estudiantes de Figma.
- Tenemos una herramienta de exportación para SVG creada por AirBnb llamada Lottie y también la librería correspondiente además de un repositorio de imágenes.
- Samsung ofrece su propio navegador web, seria interesante echar un ojo al motor y los estándares que sigue.

## SVG

### ¿Porque su auge hoy en día?

Debido a la estandarización de los navegadores, nos permite trabajar casi exacta desde cualquier navegador, además de la mejora sustancial en rendimiento y su redimension.

### Agrupación de elementos

A la hora de animar conjunto de elementos podemos agruparlos, de tal manera que respondan cómo úno solo, te pongo el ejemplo del card de Mario, dónde podemos agrupar las manos/volante/ruedas, y con la misma orden estamos moviendo a la vez simulando el control de Mario sobre el Kart.

### Nodos

Contra menos nodos, menos puntos de cálculo, por lo que mantendremos un mejor rendimiento a la hora de carga, quizás en diseños simples no llegues a notar la diferencia, pero, cuando la cosa se complica, la carga es significativa, Best-Practices ✨

### ViewBox y posicionamiento

Debido al calculo relativo de los elementos dentro de
"viewBox", si los sacas fuera de este elemento jamás se calculará de la misma manera, quedándose descompasado, al tener puntos de referencia distintos, es preferible ocultar el elemento y hacerlo aparecer antes que eliminarlo del grupo.

### Fill vs Stroke

Ahora vas a recordar las películas de Disney cómo las primeras versiones de Mickey o el videojuego de CupHead, en concreto, Piernas y brazos, si te fijas están formadas por una línea gruesa, de esta manera podemos usarlos cómo un sistema de "huesos" similar al de Blender, simplemente moviendo los nodos de control tenemos un sistema simple y muy concreto de realizar animaciones, ahora imagínate la cantidad de elementos nodos al tener en cuenta si estos mismos brazos fueran relleno.

### Por documentar

``Easing duration properties +``

## Figma

### Control versión

¿Sabías que hay un control de versiones?, échale un vistazo en el apartado de inicio.

### Regiones

Puedes rellenar distintas regiones dentro del mismo vector, tan solo haz clic al vector en cuestión o apóyate en las opciones del apartado superior.

### Copy to ClipBoard

No es necesario hacer una exportación directa del svg
también puedes copiarlo en las opciones de inicio o haciendo click derecho sobre el vector, es más rápido a la hora de trasladarlo a herramientas cómo Lottie o SVGator.

## SVGator

Apoyándonos en la función de Figma para copiar directamente el SVG, SVGator nos permite pegar el contenido del block de notas.

Para crear animaciones que requieran seguir de una ruta,
podemos pintar un "path" y decirle al elemento que se mueva teniendo a este path cómo referencia. Cómo si se tratase de un sigue lineas electrónico.

## Recursos

### Creadores de contenido

 [@bramus](https://twitter.com/bramus) Google DevRel.

- Amelia Water

### Enlaces

[slides.com](https://slides.com/carmenansio)

### Libros

The Animator's survival kit
**mas libros en slides**

### Herramientas

- Lottie/Lottie files
- StorySet
- Ux Motion
