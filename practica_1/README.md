# Caso práctico 1

**Objetivo:** Descargar imagen de dockerhub y correr múltiples contenedores.

```bash
$ docker run hello-world
```

```bash
# Docker pull permite descargar imagenes desde docker hub las cuales podemos buscar con **docker search**
$ **docker search postgres**
$ docker pull postgres

# Copiar de la documentación de docker hub
$ docker run -d --name postgres-test -e POSTGRES_PASSWORD=mysecretpassword postgres

# El comando run se puede complementar para personalizar nuestros contenedores
$ docker run -d --name postgres-5430 -v ./data:/var/lib/postgresql/data -p 5430:5432 -e POSTGRES_PASSWORD=123abc -e POSTGRES_DB=base_1 postgres

# Una de las ventajas de usar contenedores es que podemos correr diferentes versiones en múltipes contenedores
$ docker run -d --name postgres-5431 -v postgres:/var/lib/postgresql/data -p 5431:5432 -e POSTGRES_PASSWORD=123abc -e POSTGRES_DB=base_2 postgres
```