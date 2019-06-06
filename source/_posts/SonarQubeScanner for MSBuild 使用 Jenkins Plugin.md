---
title: 'SonarQubeScanner for MSBuild 使用 Jenkins Plugin'
date: 2018-11-21 10:09:37
categories:
- SonarQube
tags:
- SonarQube
- Jenkins
---

### 在 Jenkins 外掛中心 找到 SonarQube Scanner 把它安裝起來

![Jenkins](https://i.imgur.com/MGOpSwT.png)

### 檢查是否安裝完成

![檢查是否安裝完成](https://i.imgur.com/VOpA38L.png)

### 管理 Jenkins > 設定系統 > SonarQube servers

![Jenkins](https://i.imgur.com/W69D8aY.png)

![Jenkins](https://i.imgur.com/djQB5ye.png)

### 啟用並且設定Sonarqube server

![Sonarqube server](https://i.imgur.com/j0Gj3jM.png)

### Global Tool Configuration

![Global](https://i.imgur.com/jKyGsJC.png)

![Global](https://i.imgur.com/iOBJvyD.png)

### 建置步驟 >依序加入 樣板

![建置步驟](https://i.imgur.com/pbY24W3.png)

![建置步驟](https://i.imgur.com/CVv8mss.png)

### 將參數設定上去

![忽略掃描](https://i.imgur.com/Uaejl96.png)

> 忽略掃描 sonar.exclusions=obj\\*,bin\\*,packages\\**,Properties\\* 

### 建置專案就會開始掃描

![建置專案就會開始掃描](https://i.imgur.com/uNnnE9D.png)

### 掃描成功

![掃描成功](https://i.imgur.com/h15iB8R.png)

![掃描成功](https://i.imgur.com/TTqBhsQ.png)

# 參考

* [如何使用 SonarQube 檢查 PHP 專案？](https://oomusou.io/sonarqube/php/)