10. Caso práctico 4
**Objetivo:** Revisar estructura de Dockerfile y ejecutar múltiples contenedores usando una archivo `docker-compose.yml`

```docker
FROM tiangolo/uvicorn-gunicorn-fastapi:python3.7
# Allow statements and log messages to immediately appear in the Knative logs

WORKDIR /app
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

ENV PYTHONUNBUFFERED True
ENV DB_HOST=postgres
ENV DB_PORT=5432
ENV DB_NAME=educafin
ENV DB_USER=postgres
ENV DB_PASSWORD=123abc

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

```docker
# Build imagen del backend
docker build -t educafin-backend .
```

```docker
# Ejecutar contenedor del backend
docker build -t educafin-backend --restart=always -p 8000 .
```

```docker
version: '3'
services:
  postgres:
    container_name: educafin-database
    image: postgres
    env_file:
      - ./.env
    volumes:
      - ./data/postgres:/var/lib/postgresql/data
    ports:
      - ${POSTGRES_PORT}:5432
    expose:
      - ${POSTGRES_PORT}
    environment:
      POSTGRES_PASSWORD: ${POSTGRES_PASS}
      POSTGRES_DB: ${POSTGRES_DATABASE}

  educafin:
    container_name: educafin-api
    build: ./
    volumes:
      - ./:/app
    restart: always
    depends_on:
      - postgres
    ports:
    - 8000:8000
```

```docker
docker-compose up
# Podemos definir el archivo yml para correr los servicios con docker-compose 
# docker-compose <-f filename.yml> up
```

```docker
docker-compose down
```
