---
title: SQL-Server-2017-安裝-登入
date: 2018-10-17 17:27:29
categories:
- SQL Server
tags:
- SQL-Server
---
# SQL Server 2017 安裝 & 登入

## 1. 下載sql server express
https://www.microsoft.com/zh-tw/sql-server/sql-server-downloads

![](https://i.imgur.com/DSjWrRS.png)

## 2. 安裝 

![](https://i.imgur.com/9CU5pZG.png)

![](https://i.imgur.com/PIVQE5B.png)

![](https://i.imgur.com/BX2qXDA.png)


## 3. 設定允許用帳號登入

![](https://i.imgur.com/PlWgPoh.png)

**右鍵 > 屬性**

![](https://i.imgur.com/AARhZ9K.png)

## 4. 設定 127.0.0.1 可以連線

(1)**開啟 > SQL Server 2017 組態管理員**

![](https://i.imgur.com/hnHGAwg.png)

(2)**啟動 TCP/IP**
(3)**IPAll > TCP通訊埠輸入 : 1433**

![](https://i.imgur.com/rtitoTG.png)

(3)重新啟動 SQL Server 

![](https://i.imgur.com/GCoZYqe.png)


## 5. 使用帳號登入

![](https://i.imgur.com/SFuHqtZ.png)


## 參考網址

* [sql sa 登入失敗(18456)](https://dotblogs.com.tw/messboy000/archive/2014/05/31/145324.aspx)
* [最近sql server 炸了,重新安装后出现登录出现 连接SQL Server:无法连接到127.0.0.1也就是.](https://blog.csdn.net/QQ459932400/article/details/78002633)