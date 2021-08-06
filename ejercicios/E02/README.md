9. Caso práctico 2

**Objetivo:** Generar un contenedor de una imagen generada a partir de un Dockerfile

```docker
# Dockerfile 
FROM ubuntu:16.04
# MAINTAINER someuser@somedomain.com 
# Esto es un comentario
RUN apt-get update && apt-get install –y mysql
CMD echo "Hello docker!"
```

```bash
# Crear imagen
$ docker build .
# Correr contenedor
$ docker run -it hello-docker
```

**Objetivo:** Generar un archivo bash, copiarlo a nuestra imagen y ejecutarlo en nuestro contenedor.

```bash
#!/bin/bash
echo Hello world!!
```

```docker
# Dockerfile 
FROM ubuntu:16.04
# MAINTAINER someuser@somedomain.com
RUN apt-get update && apt-get install –y mysql

WORKDIR /app
COPY . .

CMD ./app/hello.sh
```

```bash
# Crear imagen
docker build -t hello-bash .
# Correr contenedor
docker run -it hello-bash
```