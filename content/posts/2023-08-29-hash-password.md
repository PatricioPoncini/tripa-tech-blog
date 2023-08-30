---
title: "Funciones hash y sus usos en software"
date: 2023-08-28
author:
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["Hash", "Criptografía", "Seguridad"]
tags: ["Writing"]
description: "Vamos a hablar de que es un hash, entender como funciona, que tipos existen, como hashear una contraseña, y otros usos de las funciones hash en el mundo de la informática"
thumbnail: "https://supertokens.com/covers/password_hashing_and_salting.png"
image: "https://mojoauth.com/blog/password-hashing-101-all-about-password-hashing-and-how-it-works/password-hashing.png"
---

## ¿Qué es un hash?

Una función hash es un algoritmo matemático que transforma cualquier bloque de datos, en una nueva serie de caracteres y con una longitud fija. No importa el tamaño de la entrada, la salida siempre va a ser la misma (en el mismo tipo de hash).

Una característica de las características de este tipo de algoritmos es que son unidireccionales, osea que no se puede revertir (o al menos es muy difícil) al texto original.

Ejemplo de hashear texto:

```js
TripaTech
    ↓
(algoritmo hash SHA-1)
    ↓
449c8d850255ab5d06b9ee372d2f6c0feb382606
```

Ahora, veamos si el mismo texto pero todo en minúsucula tiene algún cambio:

```js
tripatech
    ↓
(algoritmo hash SHA-1)
    ↓
3d2a5bc126cbc6eddd11b589e10963c66338c4f1
```

Podemos ver que el hash cambió totalmente, pero por qué? Si el texto es parecido, no tiene letras diferentes, solo 2 cambiaron y fueron pasadas a minúsculas. Esto ocurre porque no importa que tan pequeño sea el cambio, el hash cambia completamente. Y además, podrás observar que el hash tiene la misma longitud en los 2 casos, pero eso no es porque las 2 palabras sean igual de largas, si utilizaramos algunas palabras del texto de ejemplo más famoso en el mundo del desarrollo obtendríamos esto

```js
Lorem ipsum dolor sit amet, consectetur adipiscing
    ↓
(algoritmo hash SHA-1)
    ↓
86205dc394f7f9d0d8e1d34d119efcf5028044d7
```

Cambió la longitud, palabras, hay mayúsculas y encima espacios. Y así y todo, la longitud del hash es la misma que los otros 2 ejemplos.

Este ejemplo está hecho con uno de los tipos más famosos de hash, el SHA-1. La familia de algoritmos hash SHA fue publicada por el Insituto Nacional de Estándares y Tecnología (NIST) como un estándar federal de procesamiento de información de EEUU. Hoy en día no se recomienda utilizar SHA-1 ya que no es tan seguro, se recomiendan tipos superiores como SHA-2(SHA-256 y SHA-512) y SHA-3.

## ¿Pero para qué se utiliza el hash?

Todo este "misterio" debe tener un porqué, un uso, un objetivo, cierto? Y la verdad es que sí, pero no solo para un solo uso, sino que tiene múltiples.

### Hashear contraseñas para persistencia en la base de datos

El uso que primero podemos ver cuando entramos a desarrollar (sobre todo backend) es para hashear contraseñas. Sería **muy** mala práctica que las contraseñas se guarden en una base de datos tal como las escribe el usuario. Esto sería comprometedor porque cualquier persona que tenga acceso a la base de datos podría verlas, tanto un desarrollador como alguien que haya comprometido el sistema. Lo que se hace es que la contraseña que ingresa el usuario, se pasa por un algoritmo de hash y se guarda ese hash en la base de datos.

_Ahora, ¿cómo podría el backend saber que el usuario "Tripa" es él?_

Porque lo que se hace es que una vez que tenemos un usuario guardado con su contraseña hasheada en la base de datos, y él quiere ingresar, el backend va a tener que validar que es él comparando las contraseñas. ¿Te acordás que dijimos que el hash es único? Bueno, ahora vas a ver un caso práctico:

Para saber si el usuario "Tripa" es él, se hashea la contraseña que escribió en el front y se compara con la contraseña guardada en la base de datos. Si estos 2 hash coinciden, es la misma persona ya que escribió lo mismo (osea los hash son iguales), si no coincidieran entonces significa que recibimos desde el front algo que no es lo mismo que el hash que se guardó en la base de datos, por lo tanto no podemos validar que es la misma persona y debemos negar el acceso a este usuario.

Ejemplo con la librería _bcrypt_ de npm:

**Hashear una contraseña:**

```js
const saltRounds = 10;

const plainPassword = "miContraseñaSecreta";

bcrypt.hash(plainPassword, saltRounds, (err, hash) => {
  if (err) {
    console.error("Error al hashear la contraseña:", err);
    return;
  }
  console.log("Contraseña hasheada:", hash);
});
```

**Comparar 2 contraseñas:**

```js
const storedHashedPassword = "$2a$10$W9I7SK4ULkLgh5llbgGk/eRpsChGC0gKDizWeDzz6F55ys.sErakm";
const userInputPassword = "miContraseñaSecreta";

bcrypt.compare(userInputPassword, storedHashedPassword, (err, result) => {
  if (err) {
    console.error("Error al comparar las contraseñas:", err);
    return;
  }

  if (result) {
    console.log("¡Contraseña correcta!");
  } else {
    console.log("Contraseña incorrecta");
  }
});
```

## Antivirus y hash
Los antivirus para poder reconocer los virus lo que hacen es obtener el hash de virus que ya existen, o de partes pequeñas y reconocibles de estos. Con estas firmas (o cadenas de hash) se arman listas de hash de malware. A estas listas se las llama Blocklist (HBL).

Entonces los antivirus al detectar un hash en una PC que coincida con uno de los que tienen en su lista, saben que se puede tratar de un virus que ya conocen o al menos es un virus que comparte pedazos de código con un virus ya existente y detectado anteriormente.

*Ejemplo de hash con diferentes frases:*
![Ejemplo hash](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Hash_function2-es.svg/1200px-Hash_function2-es.svg.png)

## Hash de archivos
También se pueden hashear archivos. Lo que se hace por ejemplo es que se crea el hash de un pdf, y guardamos ese hash en nuestra PC en un bloc de notas. Luego lo que hacemos es abrir ese archivo, modificarle algo, cualquier cosa, y lo volvemos a hashear.

Si tomaramos ese hash y lo compararamos contra el que tenemos guardado en nuestra PC vamos a ver que son diferentes, porque hubo un cambio, y por más mínimo que sea el cambio fue hecho. Esto nos permite verificar que un documento no fue alterado, ya que si lo hasheamos, lo enviamos y cuando vuelve volvemos a realizar el hash y son iguales podemos concluir que no fue alterado. Ahora, si vuelve y el hash es diferente, significa que algo cambió en el documento.
![Hash de un archivo](https://web.uanataca.com/uploads/images/1/v/o/ocp-unicidad-del-hash-diferente-documento-nuevo-hash.png)

Hay muchos otros casos de uso, como discográficas para hashear canciones, hashear datos de tarjetas en bases de datos, hashear y guardar información sensible de usuarios, firmas digitales, hasheo de tokens de usuarios, etc.

Como podes ver, hay muchos casos donde se hashean datos o bloques de información para que alguien no pueda obtenerlos ni llegar a ellos, y resulta muy útil para poder proteger estos datos ya que la única forma de violar este algoritmo matemático es con fuerza bruta o ataques de tabla arcoíris(intentan adivinar o precalcular hashes para encontrar coincidencias con la entrada original), pero así y todo hay maneras para aún asegurar más nuestros datos, aumentando el número de saltos del hash.


### Fuentes que ayudaron a escribir el artículo
- https://latam.kaspersky.com/blog/que-es-un-hash-y-como-funciona/2806/
- https://academy.bit2me.com/sha256-algoritmo-bitcoin/
- https://es.wikipedia.org/wiki/Secure_Hash_Algorithm
- https://www.redeszone.net/tutoriales/seguridad/comprobar-integridad-archivos-hash/
- https://academy.bit2me.com/que-es-hash/