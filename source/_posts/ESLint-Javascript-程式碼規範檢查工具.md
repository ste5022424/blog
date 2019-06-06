---
title: ESLint Javascript 程式碼規範檢查工具
date: 2019-05-21 17:42:06
categories:
- ESLint
tags:
- ESLint
- Node JS
- Javascriptd
---

# ESLint Javascript 程式碼規範檢查工具

## 1. 安裝工具

```bash=
npm install eslint --save-dev
```

## 2. 跑規則

> 如果方案沒有 package.json 記得先 npm init

```bash=
./node_modules/.bin/eslint --init
```

![init](https://i.imgur.com/AQOsWew.png)

## 3. 跑完之後會發現 檔案呈現紅色的

![red](https://i.imgur.com/OUZQko3.png)

## 4. 這邊就可以看到要些改的項目

![edit](https://i.imgur.com/sZ9IWa6.png)

## 5. 自動修復

```bash=
./node_modules/.bin/eslint --fix My.js
```

![fix](https://i.imgur.com/1da2Kvm.png)

# VsCode ESLint

[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
![ESLint](https://i.imgur.com/ebWP69Q.png)

# 參考
* [Getting Started with ESLint](https://eslint.org/docs/user-guide/getting-started)
* [在 VSCode 啟用程式碼規範工具 (ESLint)](https://wcc723.github.io/tool/2017/11/09/coding-style/)
* [eslint](https://eslint.org/)
* [ESLint Quickstart - find errors automatically](https://www.youtube.com/watch?v=qhuFviJn-es)