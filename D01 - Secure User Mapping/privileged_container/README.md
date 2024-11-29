# basic container

80 포트에서 실행되는 epxress 서버를 빌드 후 일반 설정으로 실행 후 접속

```shell
# Basic
docker build -t secure-user-mapping .
docker run -d --name secure-user-mapping -p 8080:80 secure-user-mapping --privileged

docker exec -it secure-user-mapping /bin/sh
```

`ps auxwf`을 통해서 실행 환경을 확인

```shell
/app # ps auxwf
PID   USER     TIME  COMMAND
    1 root      0:00 node server.js --privileged
   13 root      0:00 /bin/sh
   19 root      0:00 ps auxwf
/app # exit
```

외부 호스트에서 docker top을 이용해서 환경 확인

```shell
docker top secure-user-mapping
# UID       PID       PPID       C      STIME      TTY    TIME       CMD
# root      16381     16364      0      07:45      ?      00:00:00   node server.js --privileged
# root      16431     16364      0      07:45      ?      00:00:00   /bin/sh
```

아래 호스트에서 docker inspect를 이용해서 환경 확인

```shell
docker inspect secure-user-mapping --format='{{.Config.User}}'
# 
```

최종적으로 도커 컨테이너 종료

```shell
docker stop secure-user-mapping
docker rm secure-user-mapping
```

## 차이점

```shell
docker exec -it secure-user-mapping ls /dev
# core     full     null     pts      shm      stdin    tty      zero
# fd       mqueue   ptmx     random   stderr   stdout   urandom
```

```shell
core     full     null     pts      shm      stdin    tty      zero
fd       mqueue   ptmx     random   stderr   stdout   urandom
```