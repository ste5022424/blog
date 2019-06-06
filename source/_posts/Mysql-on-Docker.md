---
title: Mysql on Docker
date: 2019-05-28 09:52:26
categories:
- Mysql
tags:
- Mysql
- Docker
---

# Mysql on Docker

> docker-compose.yml

```bash=
version: "3.1"
services:
  db:
    container_name: "mysql"
    image: "mysql"
    volumes:
    - "/data/mysql:/var/lib/mysql"
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: "root"

  adminer:
    container_name: "adminer"
    image: "adminer"
    restart: always
    ports:
      - 8081:8080
```

# 參考
* [dockerhub mysql](https://hub.docker.com/_/mysql)
* [mysql](https://www.mysql.com/)
* [adminer](https://www.adminer.org/)