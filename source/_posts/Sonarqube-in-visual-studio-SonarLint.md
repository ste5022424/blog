---
title: Sonarqube in visual studio SonarLint
date: 2019-04-15 15:42:39
categories:
- sonarlint
tags:
- sonarlint
- sonarqube
- Visual Studio
---

# SonarLint 安裝

## 1. 工具 > 擴充功能和更新

![擴充功能和更新](https://i.imgur.com/oNK4QfK.png)

## 2. 搜尋 >  SonarLint > 下載 > 重新啟動 Visual Studio

![搜尋](https://i.imgur.com/CG2E0Ov.png)

![搜尋](https://i.imgur.com/Qa542je.png)

## 3. 建置 > 針對方案執行程式碼分析 (Alt+ F11)

![建置](https://i.imgur.com/qsu1tEZ.png)

## 4. 錯誤清單 > 組件 + IntelliSense

> 這邊就可以看到要修改的項目(S開頭的為sonrquebe的規則)

![IntelliSense](https://i.imgur.com/No8kYss.png)

## 5. 修改程式碼

> 程式碼就會顯示 綠色的蚯蚓 alt+. 就會出現建議
![綠色的蚯蚓](https://i.imgur.com/VFtLN7i.png)

![alt+.](https://i.imgur.com/9LVPM3t.png)

# 參考

* [www.sonarlint.org](https://www.sonarlint.org/)
* [如何在 Visual Studio 使用 SonarLint ?](https://oomusou.io/sonarqube/sonarlint-vs/) 