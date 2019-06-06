---
title: Docker 介紹
date: 2018-10-19 13:44:56
categories: 
- Docker
tags:
- Docker
---

![](https://i.imgur.com/XFB46do.png)


> Docker 是一個開源專案，它使用GO語言實作，讓應用程式在容器中工作並且可以自動進行，使用者不需要去關心容器的管理，操作 Docker 的容器就像操作一個快速輕量級的虛擬機。

[https://www.docker.com/](https://www.docker.com/ "https://www.docker.com/")

## Container 容器

> Container技術採取共用Host OS ，不需在每一個Container內執行Guest OS，而是在OS內的核心系統層來打造虛擬執行環境，也被稱為是OS層的虛擬化技術。

![](https://i.imgur.com/XF9AmNd.png)

## Image 映像檔

> 映像檔一個唯讀的板模，裏面包含了容器內的所有應用程式


## Docker 倉庫

> 存放Docker映像檔的倉庫，可以建立公用或者私用的倉庫


[https://hub.docker.com/](https://hub.docker.com/ "hub.docker.com")


# Docker 常用指令

### 安裝Docker
```
curl -fsSL https://get.docker.com/ | sh
```

### 查 Docker 版本
    docker version
    
### 取得 映像檔
    docker pull

### 查看 映像檔
    docker images

    -a 完整資訊
    -q 只列檔名

### 刪除 映像檔
    docker rmi image_id 

### 匯出 映像檔
    docker save -o

#### 載入 映像檔
    docker load 


### 查看 容器
    docker ps -a

### 執行容器
    docker run

    -d 背景執行
    --name 命名container
    -p 指定主機的port 轉到 container 的 port

### 刪除 容器 
    docker stop container_id
    docker rm container_id

### 批次停止跟刪除 容器
    docker stop $(docker ps -a -q)
    docker rm $(docker ps -a -q)