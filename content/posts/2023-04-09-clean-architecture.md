---
title: "Diferencias entre Javascript y Typescript"
date: 2023-09-04
author:
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["Lenguajes", "Javascript", "Typescript"]
tags: ["Writing"]
description: "Diferencias y caracteristicas de 2 de los lenguajes más en auge."
thumbnail: "https://www.imaginarycloud.com/blog/content/images/2021/05/type-vs-javascript.png"
image: "https://logica7web.es/wp-content/uploads/2022/05/Texto-mecanografiado-vs-JavaScript-Comprenda-la-diferencia-principal-en-detalle.jpg"
---

## Todos sabemos que es Javascript, pero ¿Qué es Typescript?

Typescript es un superset de JavaScript. Decimos que una tecnología es un superset de un lenguaje de programación, cuando puede ejecutar programas de la tecnología, Typescript en este caso, y del lenguaje del que es el superset, JavaScript en este mismo ejemplo. En resumen, esto significa que los programas de JavaScript son programas válidos de TypeScript, a pesar de que TypeScript sea otro lenguaje de programación.

Es un lenguaje orientado a objetos. Esto quiere decir que tanto el cliente como el servidor tienen acceso a la escritura de código. Además, se trata de un código abierto.

Por si fuera poco, uno de los beneficios adicionales de esta característica del lenguaje, es que pone a disposición el enorme ecosistema de librerías y frameworks que existen para JavaScript. Con Typescript podemos desarrollas aplicaciones con React, Vue, Angular, etc.

¿Pero si es un superset de Javascript, se ejecuta Javascript? Sí, Typescript transpila a Javascript. ¿Qué significa esto? Que cuando se ejecuta el código de TS, se convierte a Javascript (con las caracteristicas de Typescript) y allí recién se ejecuta.

## Principal característica
La principal característica de Typescript es el tipado estático.
```javascript
let edad : number; //Asignamos el tipo number para la variable edad
edad = 20; // La variable ahora sólo puede asignar valores del tipo number
```

El contraste de estos lenguajes son los de tipado dinámico, como JavaScript, estos lenguajes suelen ser mucho más flexibles, lo que nos permite escribir código menos verboso.

Por otro lado, los lenguajes de tipado estático se prestan a la implementación de herramientas de desarrollo más avanzadas, como:

- Autocompletado de código
- Recomendación de qué argumentos recibe una función
- Recomendación de qué tipo retorna una función
- Auto documentación del código
- Mejor análisis para detectar errores

## ¿Qué es el tipado? ¿Y por qué lo usa Typescript?
El tipado se refiere a cómo se declaran los tipos de variables. Estos pueden variar desde tipos simples como number y string hasta estructuras complejas.

Puedes encontrar dos categorías en los lenguajes de programación: Tipado estático y tipado dinámico.

En lenguajes con tipado estático, el tipo de variable se conoce en el tiempo de compilación, mientras que en lenguajes con tipado dinámico, el tipo de variable se conoce solamente cuando se ejecuta el programa.

JavaScript no admite tipado estático. Typescript sí, y ese esa es su ventaja.

## Ventajas de utilizar Typescript

- **Un lenguaje intuitivo**: TypeScript es un lenguaje fácil de aprender, si conoces JavaScript. Además, es un lenguaje fácil de leer y redactar.
- **Detecta errores a tiempo**: La precisión de TypeScript es ideal. Permite detectar errores de compilación antes de su ejecución, por lo que se trata de un código confiable y con un índice de error muy bajo.
- **Facilita el trabajo en equipo**: Al ser multiplataforma, varios desarrolladores pueden trabajar en un mismo proyecto al unísono. 
- **Genera código estándar**: En este sentido, esto también propicia que los posibles problemas sean menores.
- **Escritura estática**: No es un código dinámico, de modo que este tipo de escritura favorece una mejora en la estructura de código y en las técnicas de programación orientadas a objetos.
- **Efectividad**: Se pueden emplear las habilidades de JavaScript de una forma más efectiva. Compilado TypeScript, se convierte en un JavaScript más seguro y limpio.


## Principales diferencias entre JS y TS
Estas son las principales diferencias entre estos 2 lenguajes:

- TypeScript dispone de una escritura estática, mientras que JavaScript es un lenguaje dinámico.
- JavaScript no admite módulos, mientras que TypeScript sí que les da soporte.
- TypeScript dispone de interfaz, mientras que JavaScript no.
- En TypeScript sí que hay que compilar el código, en JavaScript no es necesario.

## Diferencia en código
Si entraramos en un proyecto y tenemos una funcion que trae datos de una api, no sabemos cuales son los datos que trae esa API salvo que ejecutemos esa función:
```js
const response = axios.get(endpoint);
console.log(response);
```

Pero si la cosa cambiara, y lo hicieramos con Typescript, podríamos ver como está tipada la llamada a la API para ver que datos puede traer:
```js
const response: UsuarioInterface = axios.get(endpoint);
console.log(response);
```

Fijate la diferencia entre las 2 lineas, entre la primera que solo sabemos que es una llamada a la API y la segunda, que sabemos que va a traer algo relacionado a un usuario. Y si entraramos en la interface (interfaz) de usuario, podriamos ver los datos que esperamos de la API. 

```js
export interface UsuarioInterface {
  id: number,
  nombre: string,
  apellido: string
}
```

Osea, toda la info que necesitamos sin tener que hacer la llamada a la API, cuando con Javascript tendriamos que haber llevado a cabo otros pasos.

### Fuentes que se usaron para el artículo
- [https://profile.es/blog/que-es-typescript-vs-javascript/](https://profile.es/blog/que-es-typescript-vs-javascript/)
- [https://immune.institute/blog/typescript-que-es-como-se-diferencia-javascript/](https://immune.institute/blog/typescript-que-es-como-se-diferencia-javascript/)