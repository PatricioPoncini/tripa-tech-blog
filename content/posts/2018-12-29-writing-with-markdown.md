---
title: "Instalar MySQL en Linux Mint"
date: 2023-08-27
author: 
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["MySQL", "Linux"]
tags: ["Writing"]
description: Aprender a instalar MySQL utilizando bash en Linux Mint
thumbnail: "https://noviello.it/content/images/2019/03/mysql.jpg"
image: "https://blog.trescomatres.com/wp-content/uploads/2017/03/banner-mysql.jpg"
---

En este primer post vamos a aprender a instalar MySQL en Linux Mint utilizando la bash. ¡Comencemos!

## Primeros pasos

Primero debemos saber que es la bash.

La bash en Linux Mint es la terminal, la "cmd" de windows, donde podemos escribir y ejectuar comandos. Pero si nos remitimos a la teoría pura, es:
> GNU Bash o simplemente Bash es una interfaz de usuario de línea de comandos popular, específicamente un shell de Unix; así como un lenguaje de scripting

![bash](https://i.insider.com/542451726da811d27b0a4127?width=1000&format=jpeg&auto=webp)

> To write using an easy-to-read and easy-to-write plain text format

Teniendo esto en claro, vamos a comenzar a trabajar.

### Instalación de MySQL
Vamos a proceder con el primer comando:

```bash
sudo apt install mysql-server
```
Una vez hecho, se comenzará a ejectuar. Pronto nos aparecerá una advertencia diciendo que despues de la operación "X" espacio en el disco será usado para alojar MySQL. 
> After this operation, 248 MB of additional disk space will be used.
> Do you want to continue? [Y/n]

Tecleamos "y" para que continue con el proceso de instalación.

Una vez esté finalizado, lo que hacemos es ejectuar el comando
```bash
mysql --version
```
Esto nos debería indicar que versión de MySQL tenemos instalada, lo que nos da la pauta de que la instalación fue exitosa. En mi caso, al ejectuar el comando me aparecé lo siguiente:
> mysql  Ver 8.0.34-0ubuntu0.22.04.1 for Linux on x86_64 ((Ubuntu))

¡La instalación fue exitosa!

## Usar MySQL en bash
Una vez tengamos hecho esto, si somos usuarios root podremos usar ya MySQL. Utilizando el siguiente comando vamos a poder acceder:
```bash
sudo mysql
```
AL ejecutarlo, nos pedirá nuestra contraseña de usuario root (admin). Y luego ya podremos tener disponible para usar MySQL.

Por ejemplo, ejecutando el siguiente comando:
```bash
SHOW DATABASES;
```
Podremos saber cuales son las bases de datos que tenemos actualmente (aunque en este momento, solo veremos las que trae MySQL por defecto)
```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| stockmaster        |
| sys                |
+--------------------+
5 rows in set (0,00 sec)
```
