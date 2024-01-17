# DOCKER Construcción de la imágen

```
export CR_PAT=<ACCESS TOKEN>
```

```
echo $CR_PAT | docker login ghcr.io -u ignalog --password-stdin
```

Para hacer la build con tag 0.0.1

```
docker build -t ghcr.io/ignalog/nginx-demo-arm:0.0.1 docker/nginx
```

Para hacer la build con tag 0.0.1

```
docker build --build-arg FROM_IMG="nginx" --build-arg FROM_VER="1.22.1" --build-arg VERSION="0.0.1" -t ghcr.io/ignalog/nginx-demo-arm:0.0.1 docker/nginx
```

Para lanzar un contenedor mapeando el puerto local 8081 al 80 del contenedor

```
docker run -d --name nginx-demo-arm -p 8081:80 ghcr.io/ignalog/nginx-demo-arm:0.0.1
```

Para subir la imagen a nuestro registry

```
docker push ghcr.io/ignalog/nginx-demo-arm:0.0.1
```

Para parar el contenedor

```
docker stop nginx-demo-arm
```

Para eliminar el contenedor

```
docker rm nginx-demo-arm
```

Ahora vamos a generar una nueva version 0.1.1 y siguientes versiones

```
    VERSION=0.1.0 && \
        docker build --build-arg FROM_IMG="nginx" --build-arg FROM_VER="1.22.1" --build-arg VERSION="$VERSION" -t ghcr.io/ignalog/nginx-demo-arm:$VERSION docker/nginx && \
        docker push ghcr.io/ignalog/nginx-demo-arm:$VERSION
```

    VERSION=0.1.0 && \
    docker build --build-arg FROM_IMG="nginx" --build-arg FROM_VER="1.22.1" --build-arg VERSION="$VERSION" -t ignalog/nginx-demo-arm:$VERSION docker/nginx && \
    docker push ignalog/nginx-demo-arm:$VERSION

    VERSION=0.0.1 && \
    docker build --build-arg FROM_IMG="nginx" --build-arg FROM_VER="1.22.1" --build-arg VERSION="$VERSION" -t ghcr.io/ignalog/nginx-demo-arm:$VERSION docker/nginx && \
    docker tag ghcr.io/ignalog/nginx-demo-arm:$VERSION ghcr.io/ignalog/nginx-demo-arm:latest && \
    docker push ghcr.io/ignalog/nginx-demo-arm:$VERSION && \
    docker push ghcr.io/ignalog/nginx-demo-arm:latest

    VERSION=0.1.0 && \
    docker build --build-arg FROM_IMG="nginx" --build-arg FROM_VER="1.22.1" --build-arg VERSION="$VERSION" -t ignalog/nginx-demo-arm:$VERSION docker/nginx && \
    docker tag ignalog/nginx-demo-arm:$VERSION ignalog/nginx-demo-arm:$VERSION && \
    docker tag ignalog/nginx-demo-arm:$VERSION ignalog/nginx-demo-arm:latest && \
    docker push ignalog/nginx-demo-arm:$VERSION && \
    docker push ignalog/nginx-demo-arm:latest

    Cuando el repositorio nginx-demo-arm en github es privado no consigue cargar el pod aún utilizando bien el token de acceso ni aun dandole todos los permisos posibles. Alguien sabe por qué?
