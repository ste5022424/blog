---
title: Docker compose Run Redis
date: 2018-12-12 16:32:46
categories:
- Redis
tags:
- Docker
- Redis
- Docker compose
- Visual Studio Code
---
# Docker compose Run Redis

## 建立資料夾 及 Dockerfile

```bash
 mkdir composeredis
 cd composeredis
 vi docker-compose.yml
```

## docker-compose.yml

```bash
version: "3"
services:
  redis:
    image: redis
    ports:
     - "1233:6379"
    volumes:
     - "./tmp/redis:/data"
```

## docker-compse run redis

```bash
docker-compose up -d
```

![docker-compose](https://i.imgur.com/fzhLCey.png)

## docekr ps -a

![docekr ps -a](https://i.imgur.com/oCA5fVw.png)

## 連線測試

```bash
telnet 127.0.0.1 1233
set mykey 999
get mykey
```

![telnet](https://i.imgur.com/zz3UsVZ.png)