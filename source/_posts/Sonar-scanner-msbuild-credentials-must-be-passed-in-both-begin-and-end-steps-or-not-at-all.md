---
title: >-
  Sonar-scanner-msbuild : credentials must be passed in both begin and end steps
  or not at all
date: 2019-04-23 11:54:14
categories:
- SonarQube
tags:
- SonarQube
---

# Sonar-scanner-msbuild : credentials must be passed in both begin and end steps

#### 再跑 SonarScanner 的時候跳出了錯誤([credentials must be passed in both begin and end steps]((https://github.com/SonarSource/sonar-scanner-msbuild/releases/tag/4.1.0.1148)))，如果再 SonarScanner.MSBuild.exe中要使用 /d:sonar.login，必須在 begin 和 end 都要加入 /d:sonar.login，才會生效。

![error](https://i.imgur.com/4i5JLOM.png)

``` bash
SonarScanner.MSBuild.exe begin /k:"project-key" /d:sonar.login="YourToken"
MSBuild.exe <path to solution.sln> /t:Rebuild
SonarScanner.MSBuild.exe end /d:sonar.login="YourToken"
```

> Token 的部分可以去帳號設定產出來
![Token](https://i.imgur.com/qcSnpi2.png)

![Token](https://i.imgur.com/xHttBYN.png)

# 參考

* [sonar-scanner-msbuild : 4.1.0.1148](https://github.com/SonarSource/sonar-scanner-msbuild/releases/tag/4.1.0.1148)

* [SonarQube+Scanner+for+MSBuild](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild)
