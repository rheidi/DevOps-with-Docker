# Exercises

## 1.1 Getting started 
Three containers, two stopped and one running
```console
➜  ~ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS                     PORTS     NAMES
d157a6bde8af   nginx     "/docker-entrypoint.…"   About a minute ago   Exited (0) 2 seconds ago             tender_shamir
8e3c8ee9f96a   nginx     "/docker-entrypoint.…"   2 minutes ago        Up 2 minutes               80/tcp    vigorous_kepler
d0e331824394   nginx     "/docker-entrypoint.…"   4 minutes ago        Exited (0) 2 seconds ago             modest_kirch
```

## 1.2 Cleanup
```console
➜  ~ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
➜  ~ docker image ls
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
➜  ~
```

## 1.3 Secret message
```console
➜  ~ docker run -d -it --name secret devopsdockeruh/simple-web-service:ubuntu
➜  ~ docker exec -it secret bash
root@17075545e8ab:/usr/src/app# tail -f ./text.log
2024-05-07 09:07:04 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

## 1.4 Missing dependencies
```console
➜  ~ docker run -d --rm -it --name fourth ubuntu
➜  ~ docker exec -it fourth bash
root@01ddf21422c8:/# apt-get update
root@01ddf21422c8:/# apt-get -y install curl
root@01ddf21422c8:/# sh -c 'while true; do echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website; done'
Input website:
helsinki.fi
Searching..
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.22.1</center>
</body>
</html>
Input website:

```

## 1.5 Sizes of images
```console
➜  ~ docker pull devopsdockeruh/simple-web-service:alpine

➜  ~ docker images
REPOSITORY                          TAG       IMAGE ID       CREATED       SIZE
devopsdockeruh/simple-web-service   ubuntu    4e3362e907d5   3 years ago   83MB
devopsdockeruh/simple-web-service   alpine    fd312adc88e0   3 years ago   15.7MB

➜  ~ docker run -dit devopsdockeruh/simple-web-service:alpine
6931956832b62c45eb1e400691183d150b08a82597cfddd1e10f957a8a5deb40
➜  ~ docker exec -it 69 sh
/usr/src/app # tail -f ./text.log
2024-05-07 10:56:13 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'

```

## 1.6 Hello Docker Hub
```console
➜  ~ docker run -it devopsdockeruh/pull_exercise
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete
5e2195587d10: Pull complete
6f595b2fc66d: Pull complete
165f32bf4e94: Pull complete
67c4f504c224: Pull complete
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"

```

## 1.7 Image for Script
```Dockerfile
FROM ubuntu:22.04

RUN <<EOF
apt-get update
apt-get install -y curl
EOF

WORKDIR /usr/src/app

COPY script.sh .

RUN chmod +x script.sh

# When running Docker run the command will be ./script.sh
CMD ./script.sh
```

## 1.8 Two line dockerfile
```Dockerfile
FROM devopsdockeruh/simple-web-service:alpine
CMD ["server"]
```

```console
docker build . -t two-line
➜  part_1 git:(main) ✗ docker run two-line
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:	export GIN_MODE=release
 - using code:	gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
```

## 1.9 
```console
docker run -v "/Users/heidi/koodausta/DevOps-with-Docker/part_1:/usr/src/app/text.log" devopsdockeruh/simple-web-service:alpine
```
