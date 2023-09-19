---
title: "¿Qué es y cómo funciona la blockchain?"
date: 2023-09-18
author:
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["Blockchain", "Criptomonedas", "Seguridad"]
tags: ["Writing"]
description: "Explora a fondo este mundo, como interactuan las criptomonedas y demás. Analizaremos su funcionamiento, su impacto en las finanzas y la seguridad de los datos."
thumbnail: "/images/blockchain.jpg"
image: "/images/blockchain_banner.jpg"
---

## Para comenzar, ¿qué es la blockchain?
Por definición, blockchain es un libro de contabilidad inmodificable y compartido que facilita el proceso de registro de transacciones y seguimiento de activos en una red empresarial. Prácticamente cualquier cosa de valor puede ser rastreada y comercializada en una red blockchain, de modo que se reducen el riesgo y los costes para todos los involucrados.

Una red blockchain puede rastrear pedidos, pagos, cuentas, producción y mucho más. Como los miembros comparten una sola visión de la verdad, puede ver todos los detalles de una transacción de extremo a extremo, lo que aporta una mayor confianza, así como nuevas oportunidades y eficiencia.

## ¿Cómo funciona?
El proceso funciona de esta manera. Si A quiere enviarle dinero a B, ahora ellos no están solos dentro de la blockchain, implicamos a otras personas. Si A quiere enviar un bitcoin de su cuenta personal a B, primero A le avisa a todo el mundo sobre la transacción.  Para ilustrar esta idea, podemos imaginar un libro contable donde se registran todas las transacciones de entrada y salida.

La información está distribuida en múltiples nodos independientes e iguales entre sí que la examinan y la validan sin necesidad de que se conozcan entre ellos. El tema aquí es que una vez que se inserta la información, no puede ser eliminada ni actualizada, ya que al ir toda la información hasheada (y estar todos los blockes relacionados criptográficamente) si algún dato se modificara, se deberian modificar todos los registros ya que están conectados unos con otros.

![Como funciona la blockchain](https://media.geeksforgeeks.org/wp-content/uploads/20220518004235/BlockchainF1.jpg)

**Aclaración:** dentro de la blockchain nadie sabe el nombre de A y B, ya que estos, como todas las transacciones y movimientos dentro de la blockchain están hasheados. Si quieres entender más sobre este tema, puedes leer mi otro artículo sobre [como funcionan los algoritmos hash ➜](https://tripa-tech.vercel.app/blog/2023/08/funciones-hash-y-sus-usos-en-software/)

En caso de que no lo puedas leer en este momento, una explicación rápida es que para el mundo en la blockchain, A es '6dcd4ce23d88e2ee9568ba546c007c63d9131c1b' y B es 'ae4f281df5a5d0ff3cad6371f76d5c29b6d953ec'. ¿Qué se logra con eso? Logramos que nadie sepa quien le pasó criptomonedas a quien, además de que la transferencia también se hashea. Un algoritmo hash es un algoritmo matemático mediante el cual, una cadena string se transforma en otra más larga de tal manera que no se puede revertir, osea que no podemos saber cual es la palabra dentro de un hash.

¡Ahora sí, sigamos!

## Veamos un ejemplo
Pensemos que estamos en una sala llena de personas, y cada vez que una persona le otorga dinero a otra, todos anotan en un papel eso, ej: 'Juan le dió 10 bitcoins a Tripa'. Todos anotarían cada vez que alguna transacción así se hiciera, y nadie podría borrar ni actualizar la información. Por lo que, veamos el papel que veamos, las transacciones siempre serán las mismas. Los datos están distribuidos en una red, este es un ejemplo simple pero que lleva a entender fácilmente como funciona el registro de las transacciones en blockchain.

Pero veamos un ejemplo de una empresa que aplica el blockchain en un caso real: Disney. 

Disney utiliza la tecnología blockchain en las operaciones de la compañía para seguimiento de inventario, así como ventas y envíos en los parques. Además, la empresa presentó una patente para un sistema basado en blockchain que podría permitirle rastrear el uso de contenido con derechos de autor, podría averiguar quien fue el que hizo uso del contenido y además para qué.

## Uso de criptomonedas
Para hacer las transacciones en la blockchain, se utilizan criptomonedas. Pero...

### ¿Qué es una criptomoneda?
Una criptomoneda es un medio digital de intercambio. Cumple la función de una moneda (o dinero) pero en un formato digital. Utiliza métodos criptográficos para asegurar sus transacciones financieras, controlar la creación de nuevas unidades y verificar la transferencia de activos. Una de las más famosas es Bitcoin, y vamos a hablar de ella.

![Bitcoin banner](https://img.freepik.com/free-vector/cryptocurrency-bitcoin-golden-coin-with-digital-circuit-lines-background_1017-33592.jpg?w=826&t=st=1695089032~exp=1695089632~hmac=67c65346a2666ef3001b346bc5d275999f30336d72d115f3ece2852036380c61)

No depende de un ente gubernamental para que funcione, ya que es descentralizada. Por ello es posible comprar, vender, realizar todo tipo de transacciones de forma rápida, sin condiciones ni límites. La importancia de Bitcoin es que todo queda registrado con una huella digital imborrable (hash) como dijimos anteriormente que se maneja en la blockchain.

A pesar de que esto es algo que se suele usar mucho en los comerciones en línea, hoy en día muchos comercios físicos también aceptan criptos. Por lo que esto es una total revolución en como se maneja el dinero dentro del internet, pero también fuera. Cada vez hay más países que aceptan (o al menos evalúan) el uso de Bitcoin.

### Ventajas y desventajas de Bitcoin
A modo explicativo y que sea más fácil de leer, te dejo este cuadro de las ventajas y desventajas de el uso de Bitcoin. Al final del artículo encontrarás la fuente de donde saqué el gráfico.
![Ventajas y desventajas de Bitcoin](https://cdn.shopify.com/s/files/1/2642/0470/files/Ventajas_y_riesgos_de_Bitcoin_-_LISA_Institute._5baf7d28-303c-4778-a2a6-6e46a22839e1.jpg?v=1630670447)

### Fuentes
- https://www.ibm.com/es-es/topics/blockchain
- https://www.xataka.com/especiales/que-es-blockchain-la-explicacion-definitiva-para-la-tecnologia-mas-de-moda
- https://vmark.eu/por-que-es-tan-importante-la-tecnologia-blockchain/