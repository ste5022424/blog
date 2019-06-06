---
title: 'Docker run Jenkins'
date: 2018-10-19 11:50:40
categories: 
- Jenkins
tags: 
- Jenkins
- Docker
---

## Docker run Jenkins

### 安裝 jenkins

```
mkdir -p -m 777 jenkins_home
docker run -d -p 8080:8080 -p 50000:50000 -v /jenkins_home:/var/jenkins_home --name jenkins jenkins

```
### 取得密碼(initialAdminPassword)
```
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

### 進入Jenkins
http://127.0.0.1:8080/


## 參考網址
* [Jenkins On Doker](https://github.com/jenkinsci/docker/blob/master/README.md)
* [Get Started with Jenkins 2.0 with Docker](https://www.cloudbees.com/blog/get-started-jenkins-20-docker)