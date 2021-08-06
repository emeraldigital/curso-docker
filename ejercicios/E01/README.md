# Ejercicio 1. Hello world!!

## Objetivo

Correr un contenedor que imprime en pantalla el típico: `Hello world!`.

> En informática, **Hola mundo** es un programa que imprime el texto «¡Hola, mundo!» en un dispositivo de visualización, en la mayoría de los casos la pantalla de un monitor. Este programa suele ser usado como introducción al estudio de un lenguaje de programación, siendo un primer ejercicio típico, y se considera fundamental desde el punto de vista didáctico.

## Instrucciones

Ejecuta en la terminal el comando

```bash
$ docker run hello-world
```

```bash
# OUTPUT:
docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete 
Digest: sha256:df5f5184104426b65967e016ff2ac0bfcd44ad7899ca3bbcf8e44e4461491a9e
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## Conclusion

Cuando no existe una imagen en nuestro equipo docker la busca en docker hub, si la encuentra la descarga (pull).

Al ejecutar `docker run IMAGE:TAG` creamos un contenedor a partir de la `IMAGE:TAG`, si no especificamos un TAG docker por default considerará la imagen con la etiqueta `latest`.