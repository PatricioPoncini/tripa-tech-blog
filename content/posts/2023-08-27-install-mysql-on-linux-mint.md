---
title: "Instalar MySQL en Linux Mint"
date: 2023-08-27
author: 
  name: "Patricio Poncini"
  image: images/author/author_img.jpg
categories: ["MySQL", "Linux", "Bases de datos"]
tags: ["Writing"]
description: Aprenderas a instalar MySQL en Linux Mint utilizando la bash. Además, crearás tu primera base de datos mediante comandos
thumbnail: "/images/mysql_install_banner.jpg"
image: "https://blog.trescomatres.com/wp-content/uploads/2017/03/banner-mysql.jpg"
---

En este primer post vamos a aprender a instalar MySQL en Linux Mint utilizando la bash. ¡Comencemos!
## Primeros pasos

Primero debemos saber que es la bash.

La bash en Linux Mint es la terminal, la "cmd" de windows, donde podemos escribir y ejectuar comandos. Pero si nos remitimos a la teoría pura, es:
> GNU Bash o simplemente Bash es una interfaz de usuario de línea de comandos popular, específicamente un shell de Unix; así como un lenguaje de scripting

![bash](https://i.insider.com/542451726da811d27b0a4127?width=1000&format=jpeg&auto=webp)

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

Cabe aclarar que apenas se instala MySQL el servicio está corriendo por defecto, por lo que ya estará iniciado y no tendrás que hacer ningún proceso adicional para levantarlo.

¡Si pudiste ver la versión, la instalación fue exitosa!

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
| sys                |
+--------------------+
4 rows in set (0,00 sec)
```

Si quisieramos crear una base de datos nueva, tendríamos que usar el comando
```bash
CREATE DATABASE nombre_base_de_datos;
```
Y una vez hecho esto, si volvieramos a usar el comando para ver las bases de datos, observaríamos esto
```bash
mysql> CREATE DATABASE tripa_tech;
Query OK, 1 row affected (0,02 sec)
```
```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| tripa_tech         |
+--------------------+
5 rows in set (0,00 sec)
```
Y listo, así tendríamos MySQL instalado en nuestro Linux Mint con nuestra primer base de datos creada y lista para poder trabajar con ella.

Te recomiendo leer la documentación acerca de las queries de MySQL para que sepas como poder manejar registros en la base de datos, para poder leer, actualizar, borrar o insertar datos. 

[Documentación "Reference Manual " MySQL 8.0 ➜](https://dev.mysql.com/doc/refman/8.0/en/select.html)

[Documentación "MySQL Shell 8.0" ➜](https://dev.mysql.com/doc/mysql-shell/8.0/en/)