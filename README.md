# CreacionDBDocker

En este ejercicio vamos a crear una base de datos en MySQL corriendo sobre Docker

## Requisitos: 

1. Ya tener instalado y corriendo una VM con Docker y tener contenedores de MySQL arriba. 

2. Haber realizado la configuración pertinente descrita en el _Flow 4_. Si aún no ha hecho esto, [pulse aquí para ver el tutorial](https://github.com/Vanadiox/NodeRed-Flow4G12)



Para ello, primero hay que listar los contenedores disponibles. Abra una ventana de comandos e introduzca lo siguiente: 

~~~
docker container ls -a
~~~

Céntrese en las columnas de _CONTAINER ID_ e _IMAGE_. Debe estar una imágen llamada _mysql:latest:_. A la izquierda, en la columna _CONTAINER ID_ debe estar el id del contenedor. Cópielo y péguelo en el siguiente comando: 

~~~
docker exec -it [id] mysql -u root -p
~~~

Donde [id] es el id de su contenedor mysql. En mi caso, el comando se ve así:

~~~
docker exec -it ec6961923fec mysql -u root -p
~~~

Le pedirá una contraseña. Esta se encuentra en el archivo 

~~~
compose.yaml
~~~

visto con anterioridad. Una vez introducida la contraseña de manera correcta, la consola entrará en el servidor mysql y se verá así:

~~~
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.33 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
~~~

Aquí empezará a teclear. 

Si escribe el comando

~~~
show databases;
~~~

la consola mostrará las bases de datos disponibles, como es el siguiente ejemplo:

~~~
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.02 sec)
~~~

Vamos a crear una base de datos llamada "cursoIoT". Para ello, teclee:

~~~
create database cursoIoT;
~~~

Para mostrar la BD, teclee

~~~
show databases;
~~~

y ya aparecerá nuestra BD

~~~
+--------------------+
| Database           |
+--------------------+
| cursoIoT           |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.02 sec)
~~~

Ahora seleccionemos nuestra recién creada BD. Para ello, teclee:

~~~
use cursoIoT
~~~

Y ya estamoslistos para agregar las tablas. En este caso, agregaremos una tabla con las siguientes columnas: id, fecha, nombre, temperatura, humedad. Para ello, tecleamos la siguiente sentencia: 

~~~
create table clima(id int(6) unsigned auto_increment primary key, fecha timestamp default current_timestamp, nombre char(248) not null, temperatura float(4,2) not null, humedad int(6) not null);
~~~
y mostramos la tabla con

~~~
show tables;
~~~

y aparecerá

~~~
mysql> show tables;
+--------------------+
| Tables_in_cursoIoT |
+--------------------+
| clima              |
+--------------------+
1 row in set (0.00 sec)
~~~

Ahora, es tiempo de introducir los datos. Para este ejemplo solo completaremos 3 columnas: Nombre, temperatura y humedad: 

~~~
insert into clima (nombre, temperatura, humedad) values ("Tu nombre", t, h);
~~~~

Donde 
- "Tu nombre": pondrá usted su nombre
- t: la temperatura (en números enteros o con punto decimal)
- h: la humedad (de 0 a 100)

Ahora, para mostrar los resultados, teclee

~~~
select * from clima;
~~~

Y aparecerá algo como esto:

~~~
mysql> select * from clima;
+----+---------------------+-----------------+-------------+---------+
| id | fecha               | nombre          | temperatura | humedad |
+----+---------------------+-----------------+-------------+---------+
|  1 | 2023-05-26 03:44:42 | Pepe Pecas      |       22.00 |      50 |
|  2 | 2023-05-26 03:48:39 | Aquiles Bailo   |       29.00 |      70 |
|  3 | 2023-05-26 03:48:45 | Laura Sad       |       10.00 |      50 |
|  4 | 2023-05-28 00:46:27 | Pepe Grillo     |       10.00 |      50 |
+----+---------------------+-----------------+-------------+---------+
4 rows in set (0.00 sec)
~~~

En este caso, hemos metido más datos a la tabla. 

Para salir de mysql, solo teclee

~~~
exit
~~~

y la consola respondará con un "Bye". 

# ¡Y LISTO!

## Referencias:

[Flow 4: Configuración de mysql](https://github.com/Vanadiox/NodeRed-Flow4G12)

## Créditos

[Manual creado por Vanadiox (Kevin H)](https://github.com/Vanadiox)