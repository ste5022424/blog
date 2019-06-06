---
title: SonarQube Server pluin StyleCop
date: 2019-01-18 13:56:52
categories:
- SonarQube
tags:
- SonarQube
- SyleCop
---

# SonarQube Server pluin SyleCop Pluin

### 1. 下載外掛

#### [官網下載](http://www.sonarplugins.com/stylecop)

![](https://i.imgur.com/RS5OUM4.png)

#### 指令下載

```
wget http://downloads.sonarsource.com/plugins/org/codehaus/sonar-plugins/stylecop/sonar-stylecop-plugin/1.1/sonar-stylecop-plugin-1.1.jar
```

### 2.下載到 /extensions/plugins 資料夾底下，然後重新啟動

```
docker restart sonarqube
docker logs sonarqube
```
![](https://i.imgur.com/nFq3qfv.png)