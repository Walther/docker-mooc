# Part 1

## 1. Getting started

Starting three detached containers

```
docker run -d nginx:latest
d2aaa32e5610b6d3ba3959f476698711c4a32cdc7b11226d2e0159ae9fc7ad10
docker run -d nginx:latest
77088054cc06f81bfb0bbfe0a6b3ad49acd2fda77a35238d3c53eb24787c5b59
docker run -d nginx:latest
8619d49da40f4d66e5b990cf425c5f88f8c741af45d3eb47fa2cfbddca4a3042
```

Confirming they're running

```
docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
8619d49da40f   nginx:latest   "/docker-entrypoint.…"   28 seconds ago       Up 27 seconds       80/tcp    beautiful_dhawan
77088054cc06   nginx:latest   "/docker-entrypoint.…"   29 seconds ago       Up 29 seconds       80/tcp    amazing_robinson
d2aaa32e5610   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    objective_bell
```

Stopping two containers

```
docker container stop d2a 770
d2a
770
```

Listing all containers

```
docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS                     PORTS     NAMES
8619d49da40f   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute          80/tcp    beautiful_dhawan
77088054cc06   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Exited (0) 3 seconds ago             amazing_robinson
d2aaa32e5610   nginx:latest   "/docker-entrypoint.…"   2 minutes ago        Exited (0) 3 seconds ago             objective_bell
```

## 2. Cleanup

Stop the remaining container

```
docker container stop 861
861
```

Remove all containers

```
docker container rm 861 770 d2a
861
770
d2a
```

List all containers to verify

```
docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## 3. Secret message

Start the mystery container

```
docker run -d --rm -it devopsdockeruh/simple-web-service:ubuntu
cd228f8c59620f7dcb5e165e43dcfbab1cc17f4c3832eeaff59c1dd2d2b99a7d
```

Run an interactive shell attached to the container

```
docker exec -it cd22 bash
root@cd228f8c5962:/usr/src/app# ls
server  text.log
root@cd228f8c5962:/usr/src/app# tail -F text.log
2021-11-22 11:26:02 +0000 UTC
2021-11-22 11:26:04 +0000 UTC
2021-11-22 11:26:06 +0000 UTC
2021-11-22 11:26:08 +0000 UTC
2021-11-22 11:26:10 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
2021-11-22 11:26:12 +0000 UTC
2021-11-22 11:26:14 +0000 UTC
2021-11-22 11:26:16 +0000 UTC
2021-11-22 11:26:18 +0000 UTC
2021-11-22 11:26:20 +0000 UTC
```

## 4. Missing dependencies

Initial state:

```
docker run --rm -it ubuntu:latest sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
Input website:
helsinki.fi
Searching..
sh: 1: curl: not found
```

Solution 1: install `curl` within the image:

```
docker run --rm -it ubuntu:latest sh -c 'apt update && apt install -y curl; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
Get:1 http://ports.ubuntu.com/ubuntu-ports focal InRelease [265 kB]
Get:2 http://ports.ubuntu.com/ubuntu-ports focal-updates InRelease [114 kB]
Get:3 http://ports.ubuntu.com/ubuntu-ports focal-backports InRelease [101 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease [114 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports focal/universe arm64 Packages [11.1 MB]
Get:6 http://ports.ubuntu.com/ubuntu-ports focal/multiverse arm64 Packages [139 kB]
Get:7 http://ports.ubuntu.com/ubuntu-ports focal/restricted arm64 Packages [1317 B]
Get:8 http://ports.ubuntu.com/ubuntu-ports focal/main arm64 Packages [1234 kB]
Get:9 http://ports.ubuntu.com/ubuntu-ports focal-updates/main arm64 Packages [1217 kB]
Get:10 http://ports.ubuntu.com/ubuntu-ports focal-updates/multiverse arm64 Packages [8777 B]
Get:11 http://ports.ubuntu.com/ubuntu-ports focal-updates/restricted arm64 Packages [3530 B]
Get:12 http://ports.ubuntu.com/ubuntu-ports focal-updates/universe arm64 Packages [1034 kB]
Get:13 http://ports.ubuntu.com/ubuntu-ports focal-backports/universe arm64 Packages [7186 B]
Get:14 http://ports.ubuntu.com/ubuntu-ports focal-backports/main arm64 Packages [2680 B]
Get:15 http://ports.ubuntu.com/ubuntu-ports focal-security/restricted arm64 Packages [3286 B]
Get:16 http://ports.ubuntu.com/ubuntu-ports focal-security/universe arm64 Packages [745 kB]
Get:17 http://ports.ubuntu.com/ubuntu-ports focal-security/main arm64 Packages [800 kB]
Get:18 http://ports.ubuntu.com/ubuntu-ports focal-security/multiverse arm64 Packages [3242 B]
Fetched 16.9 MB in 1s (13.8 MB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
All packages are up to date.
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  ca-certificates krb5-locales libasn1-8-heimdal libbrotli1 libcurl4 libgssapi-krb5-2 libgssapi3-heimdal libhcrypto4-heimdal libheimbase1-heimdal libheimntlm0-heimdal libhx509-5-heimdal
  libk5crypto3 libkeyutils1 libkrb5-26-heimdal libkrb5-3 libkrb5support0 libldap-2.4-2 libldap-com

 SNIP lots of logs here

Setting up curl (7.68.0-1ubuntu2.7) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
Processing triggers for ca-certificates (20210119~20.04.2) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
</body></html>
```

Solution 2: use an official curl image instead

```
docker run --rm -it curlimages/curl:latest sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
</body></html>
```

## 5. Size of images

Start both containers

```
docker run -d devopsdockeruh/simple-web-service:ubuntu
0af1376d2eaf804790cfb8dd0e5ef7dbe923f3e3348924173a78120c9e7cf904

docker run -d devopsdockeruh/simple-web-service:alpine
a993bda33a0dadb85d58813de68a9e1412c0c7cca63c5b4394f07da549afb949

docker ps
CONTAINER ID   IMAGE                                      COMMAND                 CREATED         STATUS         PORTS     NAMES
a993bda33a0d   devopsdockeruh/simple-web-service:alpine   "/usr/src/app/server"   2 minutes ago   Up 2 minutes             jolly_colden
0af1376d2eaf   devopsdockeruh/simple-web-service:ubuntu   "/usr/src/app/server"   2 minutes ago   Up 2 minutes             recursing_panini
```

_Sidenote: `recursing_panini` feels like a funny & appropriate name for a container here, due to the common habit of CS students getting paninis from the nearby cafeteria._

Verify the `alpine`-based image has equivalent functionality

```
docker exec -it a99 sh
/usr/src/app # ls
server    text.log
/usr/src/app # tail -F text.log
2021-11-22 11:42:27 +0000 UTC
2021-11-22 11:42:29 +0000 UTC
2021-11-22 11:42:31 +0000 UTC
2021-11-22 11:42:33 +0000 UTC
2021-11-22 11:42:35 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
2021-11-22 11:42:37 +0000 UTC
2021-11-22 11:42:39 +0000 UTC
2021-11-22 11:42:41 +0000 UTC
2021-11-22 11:42:43 +0000 UTC
^C
```

Compare the image sizes

```
docker image ls | rg devops
devopsdockeruh/simple-web-service   ubuntu    4e3362e907d5   8 months ago   83MB
devopsdockeruh/simple-web-service   alpine    fd312adc88e0   8 months ago   15.7MB
```

## 6. Hello Docker Hub

Run the command to start the mystery container

```
docker run -it devopsdockeruh/pull_exercise
```

Check the documentation on the Docker Hub page of the container <https://hub.docker.com/r/devopsdockeruh/pull_exercise>

```
This is the readme, use input "basics" to complete this exercise.
```

Give the password to the container prompt

```
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

For fun, check what happens if you give an incorrect answer

```
docker run -it devopsdockeruh/pull_exercise
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
Give me the password: hunter2
hunter2 is not the correct password, please try again
```

## 7. Two line Dockerfile

Create a simple Dockerfile

```Dockerfile
FROM devopsdockeruh/simple-web-service:alpine
CMD server
```

Build an image and tag it

```
docker build --tag web-server .
```

Run it

```
docker run web-server
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
```

## 8. Image for script

Save a small script into a file `curl.sh`, and remember to run `chmod +x curl.sh`

```sh
/bin/sh
echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;
```

Write a Dockerfile

```Dockerfile
FROM ubuntu:18.04
RUN apt update && apt install -y curl
COPY curl.sh .
CMD ./curl.sh
```

Build and tag, and run

```
docker build --tag curler .
```

```
docker run --rm -it curler
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
</body></html>
```

## 9. Volumes

Create a local file and use a bind mount.

```
touch text.log;
docker run --rm -it --mount type=bind,source=$(pwd)/text.log,target=/usr/src/app/text.log devopsdockeruh/simple-web-service
```

## 10. Ports open

Run an ephemeral container with a port forward

```
docker run --rm -it -p 8080:8080 devopsdockeruh/simple-web-service server

[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
[GIN] 2021/11/22 - 14:07:27 | 200 |       5.179ms |      172.17.0.1 | GET      "/"
^C%
```

## 11. Spring

Clone the repo from 

Create a Dockerfile

```Dockerfile
FROM openjdk:8
COPY ./spring-example-project /usr/src/myapp
WORKDIR /usr/src/myapp
RUN ./mvnw package
CMD java -jar ./target/docker-example-1.1.3.jar
```

Build and tag the image

```
docker build --tag spring-example-project .
```

Run the container

```
docker run --rm -it -p 8080:8080 spring-example-project
```

The website is available at <localhost:8080>.

## 12. Hello, Frontend!

## 13. Hello, Backend!

## 14. Environment

## 15. Homework

## 16. Heroku
