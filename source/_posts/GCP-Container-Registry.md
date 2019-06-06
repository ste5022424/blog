---
title: GCP Container Registry
date: 2018-12-26 14:48:55
categories:
- GCP Container Registry
tags:
- GCP Registry
- GCP
- Docker
- Gcloud
---

## GCP Container Registry

### 1. 確認帳號已經啟用付費功能
### 2. [開啟API服務](https://console.cloud.google.com/flows/enableapi?apiid=containerregistry.googleapis.com&redirect=https://cloud.google.com/container-registry/docs/quickstart&_ga=2.224013522.-850793838.1545806748)

![](https://i.imgur.com/jHv4PGH.png)


### 3. 安裝 [Cloud SDK](https://cloud.google.com/sdk/docs/)

#### 3.1 下載 SDK
```
mkdir gcloud
cd gcloud
wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-218.0.0-linux-x86_64.tar.gz
```
#### 3.2 解壓縮
```
gunzip google-cloud-sdk-218.0.0-linux-x86_64.tar.gz
tar xvf google-cloud-sdk-218.0.0-linux-x86_64.tar
```
> 這時候就可以看到 google-cloud-sdk/ 這個資料夾
![](https://i.imgur.com/Mh6PsOr.png)

#### 3.3 執行指令

```
cd google-cloud-sdk/
./install.sh
```
![](https://i.imgur.com/2iG0Dp3.png)

#### 3.4 init SDK

```
cd bin
./gcloud init
```
> 把網址貼到網頁上面 取得 verification code
 
![](https://i.imgur.com/rQRHit0.png)

![](https://i.imgur.com/zz1RyRD.png)

### 4. Build image

#### 4.1.1 建立 Dockerfile
```
mkdir gcpimagetest
cd gcpimagetest/
vi Dockerfile
```
#### 4.1.2 將官方的範例貼上去
```
# The Dockerfile defines the image's environment
# Import Python runtime and set up working directory
FROM python:2.7-alpine
WORKDIR /app
ADD . /app

# Install any necessary dependencies
RUN pip install -r ./requirements.txt

# Open port 80 for serving the webpage
EXPOSE 80

# Run app.py when the container launches
CMD ["python", "app.py"]
```

#### 4.1.3 建立 requirements.txt

```
# This file defines the image's dependencies
Flask
```


#### 4.1.4 建立 app.py
```
# The Docker image contains the following code
from flask import Flask
import os
import socket

app = Flask(__name__)

@app.route("/")
def hello():
    html = "<h3>Hello, World!</h3>"
    return html

if __name__ == "__main__":
  app.run(host='0.0.0.0', port=80)
```

#### 4.2 建立 image

```
docker build -t quickstart-image .
```
![](https://i.imgur.com/QzIpb2r.png)


> gcloud auth 設定(只要設定一次就可以了)

```
./gcloud auth configure-docker
```
![](https://i.imgur.com/4vnE8VL.png)

#### 4.3 tag image

```
docker tag quickstart-image gcr.io/[PROJECT-ID]/quickstart-image:tag1
```
### 5. Push Image

#### 5.1 push 前要安裝[憑證](https://cloud.google.com/container-registry/docs/advanced-authentication)
![](https://i.imgur.com/U8eL3Hp.png)


#### 5.2 建立 docker-credential-gcr
```
vi docker-credential-gcr
```

####  5.3 輸入以下憑證
```
VERSION=1.5.0
OS=linux  # or "darwin" for OSX, "windows" for Windows.
ARCH=amd64  # or "386" for 32-bit OSs

curl -fsSL "https://github.com/GoogleCloudPlatform/docker-credential-gcr/releases/download/v${VERSION}/docker-credential-gcr_${OS}_${ARCH}-${VERSION}.tar.gz" \
  | tar xz --to-stdout ./docker-credential-gcr \
  > /usr/bin/docker-credential-gcr && chmod +x /usr/bin/docker-credential-gcr
```

####  5.4 設定憑證

> 記得要回到目錄的最上層才可以設定

```
./gcloud/google-cloud-sdk/bin/gcloud  components install docker-credential-gcr
```
> 成功畫面

![](https://i.imgur.com/TtZkdtE.png)

#### 5.5 提升 docker-credential-gcr 文件權限 並執行 docker-credential-gcr設定
```
chmod 777 docker-credential-gcr
docker-credential-gcr configure-docker
```
#### 5.6 設定完成之後就可以 推送到 gcp 上面了

```
docker push gcr.io/[PROJECT-ID]/quickstart-imag:tag1
```
![](https://i.imgur.com/NZnYOf0.png)

![](https://i.imgur.com/SpO0EuV.png)

### 6. Pull Image

```
docker pull gcr.io/[PROJECT-ID]/quickstart-image:tag1
```
## 參考
* [官方說明文件](https://cloud.google.com/container-registry/docs/)
* [Authentication](https://cloud.google.com/container-registry/docs/advanced-authentication)