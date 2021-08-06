# Ejercicio 5. Docker swarm

## Objetivo

Orquestar un servicio utilizando docker swarm.

## Instrucciones

Usaremos el comando `docker stats` para obtener estadisticas en tiempo real de los contenedores en ejecución

```docker
docker stats
```

Ahora arrancaremos el servicio de docker swarm para orquestar el servicio de wordpress que creamos anteriormente.

```docker
docker swarm init
```

Cuando creamos el servicio podemos definir el numero de replicas que generara el servicio y podremos limitar los recursos que utilizará cada replica.

```docker
docker service create --limit-cpu 0.5 --limit-memory 400M --replicas 2 -p 8000:80 --name wordpress wordpress
```

Si eliminamos una replica docker swarm en automatico la restaurará para cumplir con la cuota que definimos al crear el servicio.

Podemos analizar el servicio con el comando `docker ps`.

```docker
docker service ps wordpress
```

## Conclusion

Docker swarm es una herramienta de orquestación de contenedores muy simple de usar a diferencia de otros servicios como Kubernetes.