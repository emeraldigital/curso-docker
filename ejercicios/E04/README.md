# Ejercicio 4. Docker compose

## Objetivo

Retomar el ejercicio para agilizar la generación de los servicios usando docker compose.

## Instrucciones

En el ejercicio anterior levantamos los contenedores de manera manual, cuando manejamos pocos servicios es relativamente sencillo manejar los comandos pero si la arquitectura de nuestra aplicación crece el mantener los comandos puede ser algo complicado.

Docker nos facilita esa tarea con la herramienta docker compose.

Crearemos un achivo llamado `docker-compose.yml` con el siguiente contenido.

```docker
version: '3.1'

services:

  wordpress:
    container_name: wordpress
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_USER: ${MYSQL_USER}
      WORDPRESS_DB_PASSWORD: ${MYSQL_PASSWORD}
      WORDPRESS_DB_NAME: ${MYSQL_DATABASE}
    volumes:
      - ./html:/var/www/html

  mysql:
    container_name: mysql
    image: mysql
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

Y simplificaremos nuestro archivo con variables de ambiente para administrarlas mejor:

```bash
MYSQL_ROOT_PASSWORD=123abc
MYSQL_DATABASE=wordpress-blog
MYSQL_USER=test
MYSQL_PASSWORD=123abc
```

Ejecutaremos el comando:

```bash
$ docker compose up
```

## Conclusion

Docker compose nos permite administrar de mejor manera la ejecución de los servicios contenerizados de nuestra apliación.