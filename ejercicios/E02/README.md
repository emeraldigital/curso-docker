# Ejercicio 2. Dockerfile

## Objetivo

Crear un archivo Dockerfile para un contenedor que al ejecutar imprima en pantalla `Hello world`.

## Instrucciones

Crear un archivo Dockerfile con el siguiente contenido.

```dockerfile
FROM ubuntu:16.04
CMD echo Hello world!
```

Ejecuta en la terminal el comando para generar la imagen a partir del Dockerfile. Asegurate de indicarle a docker el contexto (ubicación) del Dockerfile.

```bash
$ docker build .
```

 Revisa las imagenes locales con el comando

 ```bash
$ docker images
```

Nuestra imagen se generó, pero sin un nombre, por lo que para crear un contenedor tendremos que especificar el ID de la imagen, copialo y reemplazalo en el siguiente comando.

 ```bash
$ docker run <IMAGE_ID>
```

Para facilitar la identificación de nuestras imagenes es conveniente _etiquetarlas_ con la opción: `-t TAG:VERSION`.

Si seguiste las instrucciones en pantalla se imprimirá el mensaje `Hello world!`.

Ahora, creemos otro Dockerfile (`Dockerfile2`), con el siguiente contenido:

```dockerfile
FROM ubuntu:16.04

WORKDIR /src
COPY . .
RUN chmod 777 hello.sh

CMD /src/hello.sh
```

Y un archivo bash `hello.sh` con el contenido:

```bash
#!/bin/bash
echo Hello world!
ls -la
```

Asegurate de tener ambos archivos en el mismo directorio (contexto) y construye la imagen asignando un tag y utilizando el Dockerfile recien creado.

```bash
$ docker build -t hello:2.0 -f Dockerfile2 .
```

La imagen que creemos contendra un directorio de trabajo `/src` en el cual copiaremos el contenido de nuestro directorio actual (contexto), modificaremos los permisos de ejecución del archivo bash y finalmente, cuando creemos el contenedor será ejecutado imprimiendo en pantalla:

```bash
$ docker run hello:2.0 
Hello world!
total 32
drwxr-xr-x 1 root root 4096 Aug  6 16:35 .
drwxr-xr-x 1 root root 4096 Aug  6 16:35 ..
-rw-r--r-- 1 root root   22 Aug  6 16:35 .docker-ignore
-rw-r--r-- 1 root root   39 Aug  6 16:21 Dockerfile
-rw-r--r-- 1 root root   82 Aug  6 16:35 Dockerfile2
-rw-r--r-- 1 root root 2637 Aug  6 16:17 README.md
-rwxrwxrwx 1 root root   36 Aug  6 16:33 hello.sh
```

En caso de que queramos limitar los archivos copiados podemos excluirlos creando un archivo `.dockerignore` con el contenido:

```
.dockerignore
Dockerfile*
README.md
```

Si volvemos a generar la imagen y corremos el contenedor..

```bash
$ docker build -t hello:3.0 -f Dockerfile2 . 
```

```bash
$ docker run hello:3.0 
```
la salida habra cambiado algo similar a:

```bash
[+] Building 0.5s (9/9) FINISHED                                                                              
# Docker build output
Hello world!
total 16
drwxr-xr-x 1 root root 4096 Aug  6 16:47 .
drwxr-xr-x 1 root root 4096 Aug  6 16:48 ..
-rwxrwxrwx 1 root root   36 Aug  6 16:33 hello.sh
 ```

## Conclusion

Generamos una imagen _custom_ y aprendimos que podemos tener distintos archivos de Dockerfile dentro del mismo proyecto.

Podemos asignar un tag y versionar nuestras imagenes con la opcion `-t IMAGE_TAG:VERSION` para identificarla facilmente.

Por default docker considerará el archivo Dockerfile para generar una imagen pero podremos indicar otro Dockerfile en caso de que lo requiramos con `-f DOCKER_FILE_NAME`.

Finalmente aprendimos como copiar, excluir y asignar permisos a archivos en nuestras imagenes usando `COPY` y el archivo `.dockerignore`.