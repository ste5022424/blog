---
title: Docker compose
date: 2018-12-12 14:33:21
categories:
- Docker compose
tags:
- Docker
- Docker compose
---
# Docker compose

> 安裝 [Docker Compose](https://docs.docker.com/compose/install/)

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```

## 安裝完成就可以看版本資訊

![安裝](https://i.imgur.com/mwTzUhO.png)

## Step 1: Setup

### 1.建立 composetest 資料夾

```bash
mkdir composetest
cd composetest
```

### 2.建立 app.py

```bash
touch app.py
```

#### 2.1.編輯 app.py

```bash
vi app.py
```

Vi指令
> i 編輯
> ESC 結束編輯
> :wq 存檔並離開

#### 2.2輸入以下內容

```bash
import time

import redis
from flask import Flask


app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)


def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)


@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True)
```

### 3. 建立 requirements.txt

```bash
touch requirements.txt
```

#### 3.1. 編輯 requirements.txt

```bash
vi requirements.txt
```

#### 3.2. 輸入文字

```bash
flask
redis
```

## Step 2: Create a Dockerfile

### 1. 建立 touch Dockerfile

```bash
touch Dockerfile
```
#### 1.1. 輸入內容

```
FROM python:3.4-alpine
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```
## Step 3: Define services in a Compose file

### 1. 建立 docker-compose.yml
```
touch docker-compose.yml
```
#### 1.1. 輸入內容
```
version: '3'
services:
  web:
    build: .
    ports:
     - "5000:5000"
  redis:
    image: "redis"
    ports:
     - "6379:6379"
```

> 這時候 檔案結構會是這樣
> 
![](https://i.imgur.com/mgKu7Wa.png)

## Step 4: Build and run your app with Compose

```
docker-compose up -d
```

>這時後就可以看到剛剛 Run 的 python 網站

![](https://i.imgur.com/ftdICEH.png)


## Step 5: Edit the Compose file to add a bind mount

```
version: '3.1'
services:
  web:
    build: .
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: "redis"
    ports:
     - "6379:6379"
```
### 5.1. 再重新 build 一次就可以看到剛剛修改的內容

```
docker-compose up -d
```

![](https://i.imgur.com/YT90O9u.png)


## docker-compose 其他指令
> 背景執行 docker-compose
```
 docker-compose up -d
```
> 檢查 docker-compose 容器狀態
 
```
docker-compose ps
```


# 參考

* [Docker Compose](https://docs.docker.com/compose/)
* [Get started with Docker Compose](https://docs.docker.com/compose/gettingstarted/)