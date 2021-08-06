# Ejercicio 3. Docker pull

## Objetivo

Descargar las imagenes para generar los contenedores:

* [Wordpress](https://hub.docker.com/_/wordpress)
* [MySQL](https://hub.docker.com/_/mysql)


## Instrucciones

Ademas del docker hub podremos buscar imagenes directamente con el comando:

```bash
$ docker search wordpress
```

Se recomienda utilizar imagenes oficiales o con buena reputación (stars).

Una vez identificada la imagen que queramos podremos descargar con el comando:

```bash
$ docker pull wordpress
```

O bien ejecutarla directamente, en caso de que no se tenga la imagen local docker la descargará y la ejecutará.

Cada imagen puede tener parametros personalizables atraves de variables de ambiente.

Por ejemplo, si ejecutamos el comando:

```bash
$ docker -d run -e MYSQL_ROOT_PASSWORD=123abc mysql
```

Docker correra un contenedor a partir de una imagen de mysql (latest) y configurara el password del usuario root al valor indicado.

Usando la opción `-d` docker correrá en segundo plano, pero podremos ver la salida del contenedor usando el comando:

```docker
$ docker logs --follow mysql
```

Tambien podemos listar los contenedores que corren actualmente en nuestro equipo usando: 

```docker 
$ docker ps
```

Ejecutemos un contenedor de wordpress con la imagen que descargamos con las variables de ambiente requeridas.

Adicionalmente crearemos una red (`network`) y volumen (`volume`).

La red nos permitirá virtualizar una red en la cual nuestros contenedores convivan, lo que nos permitira pasarle al contenedor de wordpress el nombre del contenedor de mysql como nombre de host de la base de datos.

```docker
$ docker network create wordpress-blog
```

Los contenedores de docker corren en memoria y no tienen persistencia por lo que si queremos conservar los datos generados por nuestro contenedor deberemos usar un volumen. El volumen _espejea_ un directorio entre nuestro host y el contenedor. Se recomienda crear volumenes para evitar errores de permiso de escritura en el host.

```docker
$ docker volume create mysql
```

```docker
$ docker run --rm --name mysql --network wordpress-blog -p 3306:3306 -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123abc -e MYSQL_DATABASE=wordpress-blog -e MYSQL_USER=test -e MYSQL_PASSWORD=123abc mysql
```

```docker
$ docker run --rm --name wordpress --network wordpress-blog -p 8080:80 -v "$PWD/html":/var/www/html -e WORDPRESS_DB_HOST=mysql -e WORDPRESS_DB_USER=test -e WORDPRESS_DB_PASSWORD=123abc -e WORDPRESS_DB_NAME=wordpress-blog wordpress
```

Si usamos un archivo env con el contenido de las variables podemos reducir considerablemente nuestros comandos `docker run`.

Crea un archivo llamado `.env` con el contenido:

```bash
# MYSQL VALUES
MYSQL_ROOT_PASSWORD=123abc
MYSQL_DATABASE=wordpress-blog
MYSQL_USER=test
MYSQL_PASSWORD=123abc
# WORDPRESS VALUES
WORDPRESS_DB_HOST=mysql
WORDPRESS_DB_USER=test
WORDPRESS_DB_PASSWORD=123abc
WORDPRESS_DB_NAME=wordpress-blog
```

Elimina los contenedores anteriores y correlos de nuevo pero usando el archivo de variables de ambiente.

```docker
$ docker run --rm --name mysql --network wordpress-blog -p 3306:3306 -v mysql:/var/lib/mysql --env-file .env mysql
```

```docker
$ docker run --rm --name wordpress --network wordpress-blog -p 8080:80 -v "$PWD/html":/var/www/html --env-file .env wordpress
```

## Conclusion

Descargamos imagenes de docker hub y creamos contenedores a partir de ellas.

Aprendimos los conceptos de: `volume`, `network`, `enviroment`, `port`.

La opcion `--rm` nos permite crear contenedores que se eliminen al terminar su ejecución.

