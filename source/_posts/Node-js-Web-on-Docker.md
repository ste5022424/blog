---
title: Node.js Web on Docker
date: 2019-05-27 15:59:35
categories:
- Node JS
tags:
- Node JS
- Docker
---

# Node.js Web on Docker

## 1. init Project

```bash=
npm init
npm install
git init
git add .
git -commit -m "git init"
```
![](https://i.imgur.com/6Nw3vNY.png)

## 2. Edit package.json

```bash=
{
  "name": "nodejs_docker",
  "version": "1.0.0",
  "description": "nodejs_docker",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

## 3. Install express.js

```bash=
npm install express --save
```

## 4.Creat index.js

```bash=
'use strict';

const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello world\n');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```

![](https://i.imgur.com/NUWIoL2.png)

## 5. Creat Dockerfile

```bash=
FROM node:8

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "npm", "start" ]
```
![](https://i.imgur.com/Co2Q6g7.png)

## 6. Build Docker Images

```bash=
docker build -t node-web-app .
```

## 7. Docker Run

```bash=
docker run -p 49160:8080 -d --name node-web-app node-web-app
```

## 8. Demo

```bash=
curl 127.0.0.1:49160
```
![](https://i.imgur.com/34rpm5d.png)

> [範例連結](https://github.com/ste5022424/nodejs_docker)

# 參考

* [把一個Node.js web 應用程序給Docker 化](https://nodejs.org/zh-cn/docs/guides/nodejs-docker-webapp/)