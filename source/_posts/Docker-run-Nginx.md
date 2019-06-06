---
title: Docker run Nginx
date: 2018-12-07 15:24:06
categories:
- Nginx
tags:
- Docker
- Nginx
---

## Docker run Nginx

### Run Nginx

```
docker run -d -p 1324:80 --name mynginx nginx
```
![](https://i.imgur.com/q64ALvt.png)

### Using Dockerfile Create Nginx & Run Nginx

#### Creat Docker file

> Dockerfile
```
FROM nginx
COPY ./index.html /usr/share/nginx/html
```

> index.html
```
<!DOCTYPE html>
<html>
    <head>
        <title></title>
    </head>
    <body>
        <p>Hello Nginx</p>
    </body>
</html>

```

#### build docker imgage
```
docker build -t mynginx:1 .
```
#### Run mynginx

```
docker run -d --name mynginx -p 1234:80 mynginx:1
```
![](https://i.imgur.com/yeybXMF.png)


# 參考

* [https://hub.docker.com/_/nginx/](https://hub.docker.com/_/nginx/)