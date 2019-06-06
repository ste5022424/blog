---
title: Docker Nginx Reverse Proxy
date: 2018-12-10 14:55:44
categories:
- Nginx
tags:
- Docker
- Nginx
---

# Docker Nginx Reverse Proxy

## 1. 建立 nginx_reverseproxy 資料夾

```bash
mkdir nginx_reverseproxy
cd ngixn_reverseproxy/
```

## 2. 建立 nginx.conf

```bash
touch nginx.conf
```

## 3. 編輯 nginx.conf

```bash
vi nginx.conf
```

> 輸入 i可以進入編輯模式
> 輸入 ESC離開編輯模式，在輸入 ":wq"存檔
> 刪除資料夾可以使用 "rm -r 資料夾名稱"

## 4. 設定 nginx.conf

```bash
events {

}

http {
server {
  listen 80;
  server_name www.google.com;
  location / {
    proxy_pass http://www.google.com;
  }
}
}
```

## 5. Run Docker Nginx

```bash
docker run --name proxy_nginx -v /nginx_reverseproxy/nginx.conf:/etc/nginx/nginx.conf:ro -p 8088:80 -d nginx
```

## 6. 瀏覽 Yourhost:8088

![瀏覽](https://i.imgur.com/imLE42t.png)

## 使用 Dockerfile 建立 image & docker run container

### 1. Dockerfile

```bash
FROM nginx
ADD nginx.conf /etc/nginx/nginx.conf
```

### 2. build

```bash
docker build -t nginx_dockerfile:v1 .
```

### 3. docker run

```bash
docker run --name nginx_dockerfile -p 8089:80 -d nginx_dockerfile:v1
```

# 參考

* [[ DevOps ] Nginx 設定 Proxy Server 及 Load balance](https://oranwind.org/-devops-ubuntu-shang-nginx-an-zhuang-yu-she-ding/)
* [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)