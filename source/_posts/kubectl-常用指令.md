---
title: 'kubectl 常用指令'
date: 2019-03-15 11:15:23
categories:
- Kubernetes
tags:
- Kubernetes
- kubectl
- Docker
---

# kubectl 常用指令

## 以下列舉常用指令

* version :查看 kubectl 版本

```bash=
kubectl version
```

* cluster-info :顯示叢集資訊

```bash
kubectl cluster-info
```

* top :查看CPU、記憶體狀態

```bash
kubectl top pod
kubectl top node
```


* get :取得K8s相關資訊

```bash=
kubectl get pods
kubectl get service
```

* run :執行容器

```bash=
kubectl run [your-name] --image gcr.io/[your-projectid]/netcorewebapi:v1 --port 80
```

* logs :查看容器log

```bash=
kubectl logs [pod-name]
```

* exec :對容器下指令

```bash=
kubectl exec -it [pod-name] bash
```

* apply :使用 yaml 更新 K8s

```bash=
kubectl apply [youtrname].yaml 
```

* config view :查看 kubectl 設定

```bash=
kubectl config view
```

# 參考

* [kubectl-commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
* [K8S指令](https://blog.csdn.net/xingwangc2014/article/details/51204224)