# basic container

```shell
# Basic
docker build -f basic.Dockerfile -t secure-user-mapping .
docker run --name secure-user-mapping -p 8080:80 secure-user-mapping
docker exec -it secure-user-mapping /bin/sh

docker stop secure-user-mapping
docker rm secure-user-mapping

# Privileged
docker build -f basic.Dockerfile -t secure-user-mapping .
docker run --name secure-user-mapping -p 8080:80 secure-user-mapping --privileged
```