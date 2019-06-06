---
title: SonarLint - Sonqrqube Server Custom Rules
date: 2019-05-14 13:39:45
categories:
- SonarLint
tags:
- SonarLint
- Sonqrqube
---

# SonarLint - Sonqrqube Server Custom Rules

## 1. 安裝 [SonarLint](https://ste5022424.github.io/2019/04/15/Sonarqube-in-visual-studio-SonarLint/)

## 2. 檢視 > Team Explore

![Team Explore](https://i.imgur.com/RdWw9Sl.png)

## 3. 連到 Sonqrqube Server

![Sonqrqube Server](https://i.imgur.com/wkKFdfO.png)

## 4. Connet

![Connet](https://i.imgur.com/F4qQEfm.png)

![Connet](https://i.imgur.com/9csx0Jh.png)

## 5. 連線之後，選擇自己的專案下載規則

![下載規則](https://i.imgur.com/0zN7Xbb.png)

## 6. 專案會出現 .sonarlint 跟 .ruleset 檔案

> 可以將檔案加入版控，組員就可以直接連線

![sonarlint](https://i.imgur.com/ICCj1t2.png)

![ruleset](https://i.imgur.com/l62ve75.png)

## 7. 建置 > 針對方案程式碼進行分析 (Alt + F11 )

![針對方案程式碼進行分析](https://i.imgur.com/BO6jdqq.png)

## 8. 回到 sonarqube server > 選擇 > 代碼規則 > 質量配置 > 選擇一個自己做的樣板

![質量配置](https://i.imgur.com/CtywggV.png)

## 9. 隱藏某條規則 (使用S1118 當範例)

![隱藏某條規則](https://i.imgur.com/bQwCsQH.png)

## 10. 回 Team Explore 再去下載一次 profile

![profile](https://i.imgur.com/0zN7Xbb.png)

## 11. 就可以看到 S1118 這條規則已經被隱藏了

![隱藏](https://i.imgur.com/gZYOT9V.png)