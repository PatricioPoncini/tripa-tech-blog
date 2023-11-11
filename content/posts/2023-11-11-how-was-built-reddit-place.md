---
title: "Como fue construido el muro de Reddit"
date: 2023-11-11
author:
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["Reddit", "Bases de datos"]
tags: ["Writing"]
description: "Traducción de un artículo donde el equipo de Reddit cuenta como fue que llevaron a cabo el r/place de su página, contando desde los requerimientos hasta las partes más técnicas"
thumbnail: "/images/reddit_place_banner.jpg"
image: "https://theartofgaming.es/wp-content/uploads/2022/04/Reddit-mural-2022-rplace-1536x864.jpg"
---

# Introducción
Este artículo va sobre la construcción del muro de Reddit, algo que me llamó muchísimo la atención a nivel de funcionalidad. A mi parecer fue un gran proyecto ya que se necesitaban alcanzar una serie de grandes requerimientos. 

Antes de seguir, **una breve aclaración**. Seguramente leas el término *"baldosa"*. Esta palabra hace referencia a cada pequeño pedazo que un usuario podía pintar en el muro de Reddit. Más adelante la veras más seguido

Comencemos...

# Como surgió la idea
Según cuenta el artículo, el equipo cada año en el día de los inocentes quiere hacer un proyecto que explore la manera en la que los humanos interactuan a gran escala. En 2017 (año donde nace el muro de Reddit) eligieron un gran canva colaboratio, donde cada uno podia "pintar una baldosa" cada unos pocos minutos, y que todos puedan ver el progreso en tiempo real.

## Requerimientos
- El muro debia ser de 1000 baldosas por 1000 baldosas
- Los usuarios deberian estar viendo todos lo mismo, osea el muro en tiempo real. De otra manera esto generaria problemas para colaborar entre ellos
- Deberían soportar como mínimo 100,000 usuarios en simultáneo
- Cada usuario solo podría cambiar una baldosa cada 5 minutos, por lo que deberían soportar un promedio de actualizacion de 100,000 baldosas cada 5 minutos
- El proyecto debe ser diseñado para no alterar o afectar el resto de funcionalidades normales del sitio, incluso si hubiera un alto tráfico en r/place
- La configuración del sitio debe ser flexible. Esto significa que el tamaño del muro y el tiempo de espera para colocar baldosas debería ser ajustable sobre la marcha del proyecto
- La API debe ser generalmente abierta y transparente para que la comunidad de Reddit pueda construir sobre ella (bots, extensiones, recolectar data, etc) si ellos desean

# Backend
### Decisiones de implementación
En cuanto a backend, comienzan a contar que el desafío principal fue mantener a todos los usuarios (clientes) sincronizados junto con el muro. Osea, que todos estén viendo lo mismo, al mismo tiempo.

Su solución fue inicia el estado del cliente escuchando la colocación de baldosas en tiempo real, e inmediatamente luego hacer la request para el tablero completo. La response del muro completo podía estar desactualiada unos pocos segundos, siempre y cuandotuvieramos la colocación de baldosas en tiempo real. Cuando el usuario recibe el tablero completo, se traen tambien las baldosas en tiempo real que recibió meintras esperaba. Una vez cargado el muro completo, las baldosas que siguieran se actualizaban al momento de ser recibidas.

Para este esquema de trabajo, necesitaron hacer la request del estado completo del muro lo más rápido posible. Su propuesta inicial fue guardar el muro completo en una sola fila en Cassandra y cada request del muro leería la columna entera. El formato que tenían planeado para cada columna en la fila era el siguiente:
```
(x, y): {‘timestamp’: epochms, ‘author’: user_name, ‘color’: color}
```
Basicamente se guardaban las cordenadas en el eje *x* y en el eje *y*, para luego guardar el tiempo, el autor y el color de la baldosa.

Esta propuesta viene porque el tablero contiene 1 millón de baldosas, lo que significa que debería leer 1 millón de columnas. En su cluster de producción eso les tomaría un tiempo de 30 segundos, un tiempo totalmente inaceptablemente lento y que podría ejercer una presión excesiva sobre Cassandra.

El siguiente enfoque fue guardar el muro completo en Redis. Guardaron en formato **[bitfield](https://redis.io/commands/bitfield/)** (campo de bits usado en Redis) de 1 millón de enteros de 4 bits. Cada entero de 4 bits puede codificar un color de 4 bits, y las cordenadas *x* e *y* se determinaban mediante el desplazamiento (offset = x + 1000y) dentro del campo de bits. Con esto podrían leer el estado del muro leyendo el campo de bits completo. Esto ademas permite actualizar individualmente baldosas actualizando el valor del campo de bits en un offset específico.

Igualmente todavía necesitaban guardar todos los detalles en Cassandra para que los usuarios puedan inspeccionar las baldosas individuales para ver quien las colocó y cuando. Tenían planeado utilizar Cassandra para restaurar el muro en caso de que Redis falle. Leer el muro entero desde Redis tomaba menos de 100 milisgundos, lo cual era suficientemente rápido.

![How colores were stored in Redis](https://www.redditinc.com/assets/images/blog/_720xAUTO_crop_center-center_none/drawio-1.png)
*Ilustración de como los colores son guardados en Redis usando un muro de 2x2*

Estaban conscientes de exceder la capacidad máxima de bandaancha en Redis. Si muchos clientes se conectaban o frescaban al mismo tiempo el estado del muro solicitarían muchas lecturas en simultáneo a Redis. La solución fue cachearlo en el CDN porque es simple de implementar y significaba que el cache estaba lo más cerca posible del cliente, lo que ayuda a mejorar la velocidad de respuesta.

Peticiones para el estado completo del muro eran cacheadas por Fastly con expiración de 1 segundo. También comentan que añadieron un control de caché "stale-while-revalidate" para evitar que se generaran más solicitudes de las deseadas cuando la caché del tablero caducaba. Fastly mantiene alrededor de 33 puntos de presencia (POP) que realizan almacenamiento en caché de manera independiente, por lo que esperábamos recibimo como máximo 33 peticiones por segundo para el muro completo.

Para devolver las actualizaciones al cliente utilizaron websockets. Tuvieron éxito usandolo en producción para *reddit live* para más de 100,000 clientes simultáneos con todo lo que ello conlleva.

# API

## Escribiendo...