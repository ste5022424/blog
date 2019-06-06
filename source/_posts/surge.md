---
title: Surge 免費靜態網頁空間
date: 2018-11-02 14:39:54
categories:
- surge
tags:
- Surge
---

# Surge
免費靜態網頁空間

### 安裝 

```
npm install --global surge
```
>請先安裝 Node.js

### 新增一個網頁

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <P>Hello! world</P>
</body>
</html>
```
![](https://i.imgur.com/C2AqlfU.png)

### 輸入 surge 指令

```
surge
```
![](https://i.imgur.com/nalP9TX.png)

> 請自行輸入email 跟 密碼，還可以自訂Domain
 

### 上傳成功就可以看到網頁

![](https://i.imgur.com/DLoh5KV.png)

[http://ste5022424.surge.sh/index.html](http://ste5022424.surge.sh/index.html)


### 部屬到自己定義的網址

```
surge --domain ste5022424.surge.sh
```

![](https://i.imgur.com/OFKTSrX.png)

### 設定 https

```
surge --domain https://ste5022424.surge.sh
```
![](https://i.imgur.com/SxhyGA7.png)



# 參考網址
* [Surge](https://www.minwt.com/website/server/17359.html)