
12. Caso práctico 5

**Objetivo:** Orquestar un servicio utilizando docker swarm

```docker
# Inicializar docker swarm
docker swarm init
```

```docker
docker service create --limit-cpu 0.5 --limit-memory 400M --replicas 2 -p 8000:80 --name educafin-api educafin-backend
```

```docker
docker ps
```

```docker
docker service ps educafin-api
```
