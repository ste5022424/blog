---
title: Node js Hello world!
date: 2019-05-20 16:47:59
categories:
- Node js
tags:
- Node js
- VsCode
---

# Node js Hello world!

> 記得先安裝 [node js](https://nodejs.org/en/)

## 1. Init

``` bash
npm init
```

![init](https://i.imgur.com/KyI1SLv.png)

![init](https://i.imgur.com/1iq6IQb.png)

## 2. 新增 HelloNode.js

```javascript=
console.log('Hello Node JS');
```

![HelloNode](https://i.imgur.com/InyTfST.png)

## 3. 執行

### 執行有三種方式

### (1) node XXX.js

```bash=
node .\HelloNode.js
```

![bash](https://i.imgur.com/KbIncMz.png)

### (2) node run

#### package.json 加入以下片段

```bash=
"HelloNode": "node HelloNode.js
```

![package](https://i.imgur.com/BIkArgS.png)

#### Run

```bash=
npm run HelloNode
```

![run](https://i.imgur.com/IDxDVIJ.png)

### (3) Vs Code 偵錯

#### 選擇偵錯(Crtl + Shift + D) > 設定

![選擇偵錯](https://i.imgur.com/0l3LrJ4.png)

#### 選 node js

![node](https://i.imgur.com/a7FWok1.png)

#### 調整設定檔

![調整設定檔](https://i.imgur.com/UNj8b4R.png)

#### F5 啟動偵錯

![啟動偵錯](https://i.imgur.com/TLkfqJb.png)

# 參考

* [建立 第一個Node.js 專案](https://ithelp.ithome.com.tw/articles/10199745)