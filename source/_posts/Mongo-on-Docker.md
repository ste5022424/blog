---
title: Mongo on Docker
date: 2019-06-26 17:31:44
categories:
tags:
---

```bash

# Use root/example as user/password credentials
version: '3.5'

networks:
  consumer:
    name: consumer

services:
  mongo:
    container_name: 'mongo'
    image: mongo
    restart: always
    volumes:
      - '/tmp/docker/data/mongo:/data/db'
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: root
    networks:
      - consumer

  mongo-express:
    container_name: 'mongo_express'
    image: mongo-express
    restart: always
    ports:
      - 8082:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: root
    networks:
      - consumer


```

## Reference

- [mongo docker](https://hub.docker.com/_/mongo)
- [mongo](https://www.mongodb.com/)
