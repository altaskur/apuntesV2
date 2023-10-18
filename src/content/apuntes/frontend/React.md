---
title: 'React.js'
description: 'Una librería de JavaScript para construir interfaces de usuario'
pubDate: 'September 23 2023'
updatedDate: 'October 18 2023'
tags:
  - JavaScript
  - Web Development
categories:
    - Frontend
principal: false
---

- [¿Qué es React?](#qué-es-react)
- [Roadmap](#roadmap)
- [Inicializar un proyecto](#inicializar-un-proyecto)
- [JSX](#jsx)
  - [Comentarios en JSX](#comentarios-en-jsx)
  - [Diferencias con HTML](#diferencias-con-html)
- [Componentes](#componentes)
  - [Componente vs Elemento](#componente-vs-elemento)
- [Props](#props)
  - [Trabajando con props](#trabajando-con-props)
- [Estados](#estados)
- [Hooks](#hooks)
  - [Estado inicial](#estado-inicial)
  - [Propagación de eventos](#propagación-de-eventos)
- [Recorrer listas](#recorrer-listas)
- [UseEffect](#useeffect)
  - [then vs async/await](#then-vs-asyncawait)
- [Custom Hooks](#custom-hooks)

## ¿Qué es React?

React es una de las librerías más populares de JavaScript para construir interfaces de usuario, es de código abierto y fue desarrollada por Facebook.

## Roadmap

Estos apuntes pretenden ser una guía de consulta rápida de conceptos muy concretos de React, por lo que no se profundizará en cada uno de ellos.

## Inicializar un proyecto

Para inicializar un proyecto debemos usar vite, que nos permite crear un proyecto pre-configurado, junto a Eslint.

```bash
npm init vite@latest
```

Recomiendo el uso de JavaScript + SWC. SWC es un trasnpilador de JavaScript que nos permite usar las últimas características de JavaScript en navegadores antiguo, más rápido que su predeterminado Babel.

## JSX

JSX es una sintaxis que nos permite escribir código HTML dentro de JavaScript, y es una de las características más importantes de React.

### Comentarios en JSX

Los comentarios en JSX se escriben entre llaves, y deben de estar dentro de un elemento.

```jsx
function App() {
    return (
        <main>
            {/* Comentario */}
            <h1>Comentarios</h1>
        </main>
    );
};
```

### Diferencias con HTML

- Los atributos de las etiquetas HTML se escriben en camelCase, en lugar de kebab-case.
- Los atributos booleanos se escriben sin valor, por ejemplo `disabled` o `true` en lugar de `disabled="true"`.
- Las etiquetas deben cerrarse, por ejemplo `<img />` en lugar de `<img>`.
- class se escribe cómo className, ya que class es una palabra reservada en JavaScript.

## Componentes

Los componentes de React deben de estar escritos en PascalCase, esto es así para evitar colisiones con las etiquetas HTML, ya que estas están escritas en kebab-case, y nunca sabremos si en un futuro se añadirá una etiqueta HTML con el mismo nombre que nuestro componente.

```jsx
function PrimerComponente({nombre}) {
    return (
        <section>
            <h1>Componente {nombre}</h1>
            <p>Este es un componente</p>
        </section>
    )
}

export default PrimerComponente
```

Ahora para llamar al componente debemos importarlo y usarlo cómo si fuera una etiqueta HTML.

```jsx
import PrimerComponente from './PrimerComponente'

function App() {
    return (
        <main>
            <PrimerComponente nombre="Primer componente" />
        </main>
    );
};
```

ahora bien, si queremos volver a usar el componente debemos usar React.Fragment o su forma abreviada <></>, ya que un componente solo puede devolver un elemento.

```jsx
import PrimerComponente from './PrimerComponente'

function App() {
    return (
        <>
            <PrimerComponente nombre="Primer componente" />
            <PrimerComponente nombre="Segundo componente" />
        </>
    );
};
```

### Componente vs Elemento

Un componente es una función que devuelve un elemento, y un elemento es una etiqueta HTML.

```jsx
function Componente() {
    return (
        <h1>Elemento</h1>
    )
}

export default Componente
```

## Props

Las props son los atributos que le pasamos a un componente, y se pueden acceder a ellas desde el componente cómo un objeto.

```jsx
function Componente({nombre}) {
    return (
        <h1>{nombre}</h1>
    )
}
```

### Trabajando con props

Las props no deberían modificarse, ya que las props deben ser inmutables, de ese modo perdemos la seguridad  de estar recibiendo el mismo tipo de dato en el componente.
Para solucionarlo podemos envolver el componente en un elemento, y modificar las props de ese elemento.

también podemos usar children, que es una prop que nos permite pasar elementos dentro de un componente, en otros frameworks se conoce cómo slot.

```jsx

function Componente({nombre, children}) {
    return (
        <div>
            <h1>{nombre}</h1>
            {children}
        </div>
    )
}

function App() {
    return (
        <Componente nombre="Componente">
            <p>Esto es un children</p>
        </Componente>
    )
}
```

## Estados

Es un valor que cada vez que cambie, hará que el componente vuelva a pintarse en el DOM, actualizando la información.

`En el estado solo debemos guardar la mínima información necesaria para que el componente cumpla su función.`

## Hooks

Nos permite hacer que los componentes, reaccionen a ciertos eventos, o que se actualicen cuando cambie el estado de la aplicación.

Para usar un hook debemos importar userState de React, este user state nos devuelve un array con dos elementos, el primero es el estado, y el segundo es una función que nos permite modificar el estado.

```jsx

import {useState} from 'react'

function Componente() {
    const [estado, setEstado] = useState(false);
    const handleClick = () => {
        setEstado(!estado);
    }
    return (
        <button onClick={ handleClick }>
            {estado ? 'Activo' : 'Inactivo'}
        </button>
    )
}

export default Componente;
```

### Estado inicial

Podemos definir una prop cómo estado inicial, de esta forma el componente se renderizará con el estado inicial. Como buena práctica se declara con la palabra `initial`"nombreProp". ya que el estado inicial solo se ejecuta la primera vez que se renderiza el componente. Por lo tanto si cambia el estado en el componente padre, el componente hijo no se actualizará.

```jsx
function Componente({estadoInicial}) {
    const [estado, setEstado] = useState(estadoInicial);
    const handleClick = () => {
        setEstado(!estado);
    }
    return (
        <button onClick={ handleClick }>
            {estado ? 'Activo' : 'Inactivo'}
        </button>
    )
}

export default Componente;
```

### Propagación de eventos

Cuando usamos un evento en un componente, este evento se propaga a todos los elementos hijos, de esta forma podemos mandar información actualizada a los componentes hijos.

Eso quiere decir, que si renderiza un componente padre, todos los componentes hijos se renderizarán también, aunque la información que reciban no haya cambiado.

## Recorrer listas

Para recorrer listas debemos indicar un atributo key, que debe ser único, ya que React usa este atributo para identificar los elementos, y así poder actualizarlos, si colocamos la misma key en dos elementos, React seguramente replicará el estado del primer elemento en el segundo.

```jsx
function Discientes() {
    const discientes = [
        {id: 1, nombre: 'Juan'},
        {id: 2, nombre: 'Pedro'},
        {id: 3, nombre: 'María'},
        {id: 4, nombre: 'Ana'},
    ];
    return (
        <ul>
            {discientes.map((disciente) => {
                return <li key={disciente.id}>{disciente.nombre}</li>
            })}
        </ul>
    )
}

export default Discientes;
```

## UseEffect

Nos permite ejecutar código, al renderizar el componente, utilizado para manejar datos fuera de React, cómo peticiones a una API.

Nos permite ejecutar el código de tres maneras distintas:

Se ejecuta con cada renderizado.

```jsx
useEffect(() => {
    // código
})
```

Al modificar el estado y las props.

```jsx
useEffect(() => {
    // código
}, [estado, props])
```

Solo se ejecuta una vez, al renderizar el componente por primera vez, suele ser la más común,
para manejar API's.

```jsx
useEffect(() => {
    // código
}, [])
```

### then vs async/await

Aunque then es más antiguo y su lectura es más complicada, a la hora de interactuar con useEffect, es más rápido que async/await.

Async/await genera una promesa y useEffect debe ser síncrono, por lo que debemos envolver en código en una función autoejecutable.

```jsx
useEffect(() => {
    (async () => {
        try(){
            const response = await fetch('https://jsonplaceholder.typicode.com/users/1');
            if (!response.ok) throw Error('Error');
            const data = await response.json();
            console.log(data);
        } catch (error) {
            console.log(error);
        }
    })()
}, [])
```

ahora bien si usamos .then el código queda más reducido:

```jsx
useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users/1')
        .then(response => {
            if(!response.ok) throw Error('Error');
            response.json()
        })
        .then(data => console.log(data))
        .catch(error => console.log(error))
}, [])
```

En React suele ser más común usar .then, o directamente Axios.

## Custom Hooks
