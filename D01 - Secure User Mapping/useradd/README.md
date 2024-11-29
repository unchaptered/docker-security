# basic container

80 포트에서 실행되는 epxress 서버를 빌드 후 일반 설정으로 실행 후 접속

```shell
# Basic
docker build -t secure-user-mapping .
docker run -d --name secure-user-mapping -p 8080:80 secure-user-mapping

docker exec -it secure-user-mapping /bin/sh
```

`ps auxwf`을 통해서 실행 환경을 확인

```shell
/app # ps auxwf
PID   USER     TIME  COMMAND
    1 expressj  0:00 node server.js
   13 expressj  0:00 /bin/sh
   19 expressj  0:00 ps auxwf
/app # exit
```

`whoami` 및 `id` 명령어를 이용해서 user, group 관계 확인

```shell
/app $ whoami
# expressjs

/app $ id
# uid=1001(expressjs) gid=1001(nodejs) groups=1001(nodejs)
```

외부 호스트에서 docker top을 이용해서 환경 확인

```shell
docker top secure-user-mapping
# UID       PID       PPID       C      STIME      TTY    TIME       CMD
# 1001      16381     16364      0      07:45      ?      00:00:00   node server.js --privileged
# 1001      16431     16364      0      07:45      ?      00:00:00   /bin/sh
```

아래 호스트에서 docker inspect를 이용해서 환경 확인

```shell
docker inspect secure-user-mapping --format='{{.Config.User}}'
# expressjs
```

최종적으로 도커 컨테이너 종료

```shell
docker stop secure-user-mapping
docker rm secure-user-mapping
```