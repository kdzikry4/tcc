# Docker

## Courses 1
1. docker search redis
NAME                             DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
redis                            Redis is an open source key-value store that…   7412                [OK]
bitnami/redis                    Bitnami Redis Docker Image                      129                                     [OK]
sameersbn/redis                                                                  77                                      [OK]
grokzen/redis-cluster            Redis cluster 3.0, 3.2, 4.0 & 5.0               61
rediscommander/redis-commander   Alpine image for redis-commander - Redis man…   31                                      [OK] . . . . 

    docker run -d redis
33a00ea6fbc950e4e8f7769e990be499e904bd9fb3a96b3abb463b016afc5882
2. docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
33a00ea6fbc9        redis               "docker-entrypoint.s…"   5 minutes ago       Up 5 minutes        6379/tcp            happy_torvalds
3.  
    ```
    $ docker run -d --name redisHostPort -p 6379:6379 redis:latest
    f28428a309a3577103454f0e57637ada1fcfae8ed164d6131493ded13db21707
    ``` 

4. Accesing Redis
```
docker run -d --name redisDynamic -p 6379 redis:latest
f5abe2d44c43878da51e8774dd4823a80da84ca504d394a029ecf6802f58ed8b
$ docker port redisDynamic 6379
0.0.0.0:32768
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS      NAMES
f5abe2d44c43        redis:latest        "docker-entrypoint.s…"   11 seconds ago       Up 10 seconds       0.0.0.0:32768->6379/tcp   redisDynamic
f28428a309a3        redis:latest        "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:6379->6379/tcp    redisHostPort
33a00ea6fbc9        redis               "docker-entrypoint.s…"   7 minutes ago        Up 7 minutes        6379/tcp      happy_torvalds
```

5. Persisting Saved Data
```
docker run -d --name redisMapped -v /opt/docker/data/redis:/data redis
8ce299ce8136cc071d9b023c796796012426d981c4a99ff8c617fc91b7a7bcd9
```
6. Running Ubuntu Container
```
$ docker run ubuntu ps
  PID TTY          TIME CMD
    1 ?        00:00:00 ps
$ docker run -it ubuntu bash
root@7d2052563e1b:/#
``` 
## Deploy Static HTML Website as Container

1. Create Dockerfile (Copying)
```
FROM nginx:alpine
COPY . /usr/share/nginx/html
```
2. Build Docker Image
```
$ docker build -t webserver-image:v1 .
Sending build context to Docker daemon  3.072kB
Step 1/2 : FROM nginx:alpine
 ---> 4d3c246dfef2
Step 2/2 : COPY . /usr/share/nginx/html
 ---> c756a2855dcf
Successfully built c756a2855dcf
Successfully tagged webserver-image:v1
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
webserver-image     v1                  c756a2855dcf        5 seconds ago       21.2MB
nginx               alpine              4d3c246dfef2        2 weeks ago         21.2MB
ubuntu              latest              16508e5c265d        13 months ago       84.1MB
redis               latest              4e8db158f18d        14 months ago       83.4MB
weaveworks/scope    1.9.1               4b07159e407b        14 months ago       68MB
alpine              latest              11cd0b38bc3c        15 months ago       4.41MB
```
3. Running Static Web
```
$ docker run -d -p 80:80 webserver-image:v1
a160680d1d20291bb1f9e71cec2f8a680f71719728c1ad407c84d6c7f3c30307
$ curl docker
<h1>Dzikry kusu</h1>
```

## Building Container image
```
Your Interactive Bash Terminal. A safe place to learn and execute commands.
$
$ docker build -t dzikry
"docker build" requires exactly 1 argument.
See 'docker build --help'.

Usage:  docker build [OPTIONS] PATH | URL | - [flags]

Build an image from a Dockerfile
$ docker build -t dzikry:v1 .
Sending build context to Docker daemon  3.072kB
Error response from daemon: Dockerfile parse error line 4: COPY requires at least two arguments, but only one was provided. Destination could not be determined.
$ docker build -t dzikry-image:latest .
Sending build context to Docker daemon  3.072kB
Error response from daemon: Dockerfile parse error line 4: COPY requires at least two arguments, but only one was provided. Destination could not be determined.
$ docker build -t dzikry-image:latest .
Sending build context to Docker daemon  3.072kB
Step 1/4 : FROM nginx:1.11-alpine
 ---> bedece1f06cc
Step 2/4 : COPY index.html /usr/share/nginx/html/index.html
 ---> 9a135af016b3
Step 3/4 : EXPOSE 80
 ---> Running in 4ed61fbb9e7a
Removing intermediate container 4ed61fbb9e7a
 ---> da0e24b1326f
Step 4/4 : CMD ["nginx", "-g", "daemon off;"]
 ---> Running in 04f4cda5049e
Removing intermediate container 04f4cda5049e
 ---> 5c50962ec965
Successfully built 5c50962ec965
Successfully tagged dzikry-image:latest
$ docker run -d -p 80:80 dzikry-image
f6b4baf337eba3f2d8e4712b0e2ada0d207ae3f15e5021700cb990dc6cd4db94
$ curl -i http://docker
HTTP/1.1 200 OK
Server: nginx/1.11.13
Date: Tue, 15 Oct 2019 14:04:04 GMT
Content-Type: text/html
Content-Length: 21
Last-Modified: Tue, 15 Oct 2019 13:57:13 GMT
Connection: keep-alive
ETag: "5da5d039-15"
Accept-Ranges: bytes

<h1>Hello World</h1>
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS         NAMES
f6b4baf337eb        dzikry-image        "nginx -g 'daemon of…"   14 seconds ago      Up 14 seconds       0.0.0.0:80->80/tcp, 443/tcp   boring_elbakyan
```