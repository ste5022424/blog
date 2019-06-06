---
title: SonarQube 程式碼品質分析工具
date: 2018-11-20 10:03:25
categories:
- SonarQube
tags:
- SonarQube
---

## 建立 SonarQube Server

### 下載 [SonarQube](https://www.sonarqube.org/downloads/)
![](https://i.imgur.com/VYxvKTz.png)

### 下載最新的 [Java jre](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
![](https://i.imgur.com/m4f7K2k.png)


### 執行 StartSonar.bat
![](https://i.imgur.com/l9Qe4Tx.png)

![](https://i.imgur.com/OnvhdDR.png)


### 進入 http://localhost:9000 就可以看到啟動成功

![](https://i.imgur.com/0nZCYF9.png)


### 新增一個專案

![](https://i.imgur.com/h7qM0QX.png)
![](https://i.imgur.com/yiT3Ca5.png)
![](https://i.imgur.com/Pw3ekAH.png)
![](https://i.imgur.com/IrHmCyG.png)
![](https://i.imgur.com/3DsIYqs.png)
> 這時候就會產生一個專案的key 給掃描驗證使用 4e4602940368f811feba160cc8797ac455ca65d8

## 掃描自己的程式(Analyzing with SonarScanner for MSBuild)

### 下載 [Analyzing with SonarScanner for MSBuild](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild)
![](https://i.imgur.com/OMWi3KS.png)

### 先設定環境變數

```
D:\sonarqube-7.4\bin\sonar-scanner-msbuild-4.4.2.1543-net46
```
![](https://i.imgur.com/qvTXqjF.png)

![](https://i.imgur.com/MRfmYMW.png)

![](https://i.imgur.com/icY2raU.png)

![](https://i.imgur.com/HFT14QA.png)

### 建立 SonaQube 專案，它會在專案目錄底下建立 .sonarqube 資料夾

>k:"{Project Index}" 在 sonarquble 上面建立的 key
> n:"{Project Name}" 要掃描的專案名稱
```
SonarQube.Scanner.MSBuild.exe begin /k:"4e4602940368f811feba160cc8797ac455ca65d8" /n:"MyConsolTest" /v:"1.0"
```
![](https://i.imgur.com/bTou3P8.png)

### 執行 Msbuild
```
"C:\Program Files (x86)\MSBuild\14.0\bin\amd64\msbuild.exe" MyConsolTest.sln /t:Rebuild
```
![](https://i.imgur.com/yLj7IAj.png)

### 執行掃描
```
SonarQube.Scanner.MSBuild.exe end
```
![](https://i.imgur.com/wZsXqhA.png)

![](https://i.imgur.com/yCmU7y8.png)


# 參考

* [SonarQube](https://zh.wikipedia.org/wiki/SonarQube)
* [https://www.sonarqube.org/](https://www.sonarqube.org/)