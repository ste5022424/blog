---
title: GCP K8s Quickstart
date: 2018-12-28 15:19:04
categories:
- k8s
tags:
- k8s
- GCP
- Docker
---

## GCP K8s Quickstart

### 1. 安裝 gcloud

>[GCP Container Registry image安裝](https://ste5022424.github.io/2018/12/26/GCP-Container-Registry/)
>[Cloud SDK(Linux)快速入門](https://cloud.google.com/sdk/docs/quickstart-linux)

### 2. Creating a GKE cluster

```
./gcloud/google-cloud-sdk/bin/gcloud container clusters create [CLUSTER_NAME]
```
![](https://i.imgur.com/fcpVqKY.png)

### 3. 安裝 kubectl

```
./gcloud/google-cloud-sdk/bin/gcloud components install kubectl
```
![](https://i.imgur.com/2gtxj6u.png)

### 4. kubectl run Container Registry

#### 4.1 Build Docker image 

> .net core webapi 建立可以參考這篇[.net core webapi](https://ste5022424.github.io/2018/12/28/Net-Core-CLI/)

```
docker build -t gcr.io/[your-projectid]/netcorewebapi:v1
```
#### 4.2 Push image to GCR

```
docker push gcr.io/[your-projectid]/netcorewebapi:v1
```
#### 4.3 執行服務

```
kubectl run netcorewebapi --image gcr.io/[your-projectid]/netcorewebapi:v1 --port 80
```
![](https://i.imgur.com/vWp9gWH.png)

#### 4.4. 公開 k8s 容器
```
kubectl expose deployment netcorewebapi  --type LoadBalancer --port 80 --target-port 80
```
#### 4.5. 取得服務的資訊
```
kubectl get service netcorewebapi 
```
![](https://i.imgur.com/IX5PCxJ.png)

####  4.6 預覽

![](https://i.imgur.com/3DX0Tcb.png)


## 參考

* [K8S Quickstart](https://cloud.google.com/kubernetes-engine/docs/quickstart)