---
title: "Introducción al uso de CRUD e interacción con APIs"
date: 2023-08-28
author: 
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["API", "CRUD"]
tags: ["Writing"]
description: En este post nos introduciremos en el mundo de los CRUD y la interacción con APIs. ¿Qué es un CRUD? ¿Qué operaciones hace? ¿Qué es una API? Contestaremos todas estas preguntas y más
thumbnail: "https://miro.medium.com/v2/resize:fit:1400/1*2eBdh0vLZjUyCDF6x1EqvQ.png"
image: "https://miro.medium.com/v2/resize:fit:1400/1*DI5wwLcQV-b3erfLIbvfFQ.jpeg"
---

## ¿Qué es un CRUD?
CRUD es un término que se usa en informática y es el acrónimo de "**C**reate - **R**ead - **U**pdate - **D**elete". Es una abreviatura y un concepto que se utiliza para englobar las operaciones básicas que se pueden hacer interactuando con una base de datos (generalmente más utilizado en bases de datos SQL).

Se resume en que son las operaciones que puede hacer un usuario para interactuar con el servidor, desde su interfaz de cliente.

## ¿Para qué sirve?
El uso de CRUD lo dice la palabra, es para poder crear, leer, actualizar o eliminar registros de una base de datos.

*Por ejemplo:* Para crear un sistema de gestión de stock para inventariar productos, al construir la API utilizaríamos un CRUD ya que necesitaríamos poder crear productos para tener en stock, leerlos para saber cuantos tenemos, actualizarlos por si surge algún cambio, y eliminarlos cuando decidamos no vender más un producto.

Este se usa generalmente en APIs que sean [REST API](https://www.redhat.com/es/topics/api/what-is-a-rest-api), ya que se comunican por protocolo HTTP.

## ¿Qué es el protocolo HTTP?
Es el protocolo de transmisión de información de la World Wide Web. Osea, se desarrolla código para que la *computadora cliente* pueda comunicarse con la *computadora servidor* y que puedan intercambiar información.

Es una forma básica de que el *cliente-servidor* se comuniquen y puedan intercambiar datos en la web.

![HTTP Protocol](https://blog.makeitreal.camp/assets/images/http-messages.jpg)

Tiene métodos que son para usar junto con CRUD, aquí hay 4 métodos que son de los más habituales de ver:

- Método **GET**: Trae información
- Método **POST**: Envía información
- Método **PUT**: Actualiza información
- Método **DELETE**: Elimina información

[Todos los métodos HTTP ➜](https://developer.mozilla.org/es/docs/Web/HTTP/Methods)

*Por ejemplo:* Al crear una REST API, utilizaríamos CRUD para poder crear un usuario. Para esto utilizaríamos el método POST del protocolo HTTP para poder hacer una solicitud POST desde el cliente al servidor, con la información del usuario que se quiere crear (Create). El servidor procesa esta información, crea el usuario y lo guarda en la base de datos.

En ese caso, hicimos uso del método POST del protocolo HTTP interactuando con una REST API.

Hoy en día hay un stándar que es HTTPS, básicamente es HTTP pero más seguro. Y es algo prácticamente obligatorio en cualquier página hoy en día, ya que brinda confiabilidad a los usuarios al tener un protocolo seguro.

La diferencia que tiene con HTTP es que HTTPS está protegido contra intervención de terceros que quieran ver el intercambio de información. Estos datos en HTTPS van cifrados entre el *cliente-servidor*.

## ¿Qué es una API y como funciona?
Las siglas pertenecen a *"Application Programming Interface"*

Es código que permite que diferentes aplicaciones se comuniquen entre sí. Es un intermediario entre 2 sistemas, permite intercambiar datos del punto A al punto B, tanto para leer o transferir información.

![API](https://www.redhat.com/rhdc/managed-files/styles/wysiwyg_full_width/private/API-page-graphic.png?itok=RRsvST-_)

En el ejemplo que dimos antes de un sistema de control de stock de inventariado, podríamos desarrollar una API para esto.

Definamos 2 roles, un rol es **"Comprador"** y otro es **"Vendedor"**.

Cuando desarrollamos una API disponibilizamos endpoints para que los usuarios puedan acceder a las funcionalidades que le brindamos. Tomando los roles de antes, un comprador tendría acceso a la tienda, donde podría hacer una solicitud *GET* para ver todos los productos que hay en stock, y otra solicitud *POST* para registrar una venta (por ejemplo, le diríamos a la API que registre una venta y baje en 1 el stock de "Notebook Lenovo Thinkpad L15" ya que el comprador adquirió una).

Asímismo, en las APIs no solo hay métodos HTTP entre cliente-servidor en el momento. Podríamos desarrollar una función para que cuando el comprador realice una compra, el backend tome el email con el que la persona se registró y le mande un correo automáticamente al comprador indicandole que su compra fue exitosa.

El vendedor no podría (al menos con su cuenta de rol "Vendedor") realizar una compra, pero sí podría hacer una solicitud *GET* para ver cuales fueron los productos más vendidos del mes, o una solicitud *POST* para agregar un nuevo producto con stock que quiere ofrecer al público.

Osea, cada uno tiene endpoints a los que puede acceder y endpoints a los que no. Esto la API lo maneja "dejando pasar o no" a la persona, dependiendo del rol. 

**Endpoint de ejemplo para ver los productos en stock:**
```js
// GET
https://www.stock-inventory.com/products
```

**Endpoint de ejemplo para ver las ventas del mes:**
```js
// GET
https://www.stock-inventory.com/sales-month
```

Pero cuidado, una API no solo se usa para interactuar con usuarios, sino que tambien hay APIs que son para interactuar con otras APIs, se comunican entre ellas. Si nosotros quisiéramos hacer una REST API como proyecto y quisieramos mostrar el clima, lo que haríamos sería interactuar mediante una petición HTTP a una API de clima, que nos traiga esa información, y una vez la tengamos, nuestra API la muestra al usuario.

Otro ejemplo sería si tuvieramos una API con la que el usuario se puede loggear por usuario y contraseña o mediante una plataforma del gobierno de su país que valide su identidad. Si eligiera la opción de validar su identidad mediante una plataforma de un ente gubernamental, el backend (nuestra API) lo que haría sería consultarle a la API de este organismo si esta persona existe. Si la respuesta es positiva, tomaría los datos que le brinda este organismo acerca de la persona y directamente le crearía el usuario, algo que le facilita a la persona el hecho de estar escribiendo todos sus datos en los campos.

Como adicional y hablando sobre la seguridad, esta depende de la API depende exclusivamente de quien la desarrolla, ya que el developer puede dedicarle tiempo para crear un sistema robusto o hacer lo mínimo, teniendo que atenerse a las consecuencias en caso de que intente ser vulnerada.

Para comenzar con seguridad en APIs, un buen tema a tratar son los [JWT (JsonWebTokens)](https://openwebinars.net/blog/que-es-json-web-token-y-como-funciona/)