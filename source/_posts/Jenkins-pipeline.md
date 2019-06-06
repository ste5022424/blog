---
layout: pos
title: Jenkins Pipeline
date: 2018-11-23 11:21:54
categories:
- Jenkins
tags: 
- Jenkins
- Pipeline
---
# Jenkins Pipeline

### 可以將部屬流程視覺化來顯示，請看官方的這張[圖](https://jenkins.io/doc/book/pipeline/)

![視覺化](https://i.imgur.com/OXUX6Ca.png)

### 新增作業

![新增作業](https://i.imgur.com/1H6nKrr.png)

### 選擇 Pipeline 專案
![選擇](https://i.imgur.com/Rk6oGvB.png)

### 建立成功之後就可以在 script 的地方撰寫

![建立](https://i.imgur.com/Ms2I0GI.png)

### Pipeline Script 有分兩種方式

 > Pipeline Script 直接寫在 jenkins Script 上面
 > Pipeline script from SCM 可以使用版控來管理 Pipeline script
 * Pipeline Script

![Pipeline Script](https://i.imgur.com/1yz6bPX.png)

```bash
node {
    stage('Clone') {
        echo 'Clone'
    }
    stage('Build') {
        echo 'Build'
    }
    stage('Test') {
        echo 'Teset'
    }
    stage('Deploy') {
        echo 'Deploy'
    }
}
```

#### 馬上建置
![](https://i.imgur.com/RIVUvf9.png)

#### 這時候就可以看到 建置的步驟已經視覺化顯示了
![](https://i.imgur.com/yszPWq1.png)

#### Console Output
![](https://i.imgur.com/rUJMmpo.png)

#### 這裡可以看到剛剛寫的執行log
![](https://i.imgur.com/rgn76nJ.png)

* Pipeline script from SCM

![](https://i.imgur.com/zD7vhP5.png)

![](https://i.imgur.com/QkY1rdW.png)

> Repository URL 在github上面建立一個專案

#### 新增一個檔案叫　Jenkinsfile　
![](https://i.imgur.com/vmYUUY0.png)
> 檔案名稱要不一樣可以再 Script Path 設定

#### 把剛剛寫的code 貼上去，並且 commit
![](https://i.imgur.com/p1e0ECp.png)

#### 第二次建置也成功了
![](https://i.imgur.com/VLtTcJQ.png)

#### 這時候看一下 Console Output，確認就是從 git 上面取下來執行的

![](https://i.imgur.com/u3da9mL.png)

##  Pipeline Syntax 產生語法的小工具
![](https://i.imgur.com/TNiTpxw.png)

![](https://i.imgur.com/AEJ81l7.png)

### 選擇 bat: Windows Batch Script
![](https://i.imgur.com/04A1RjJ.png)

### 按下 Generate Pipeline Script，會產生語法，可以直接在 pipeline 中使用
![](https://i.imgur.com/0AMFpET.png)
> pipeline 是使用 Groovy語言來撰寫，可以參考 [Groovy’s syntax](http://groovy-lang.org/syntax.html)

# 參考
* [Pipeline - Jenkins]https://jenkins.io/doc/book/pipeline/
* [[DevOps自動化-6] Jenkins持續整合、發布](https://dotblogs.com.tw/aken1215/2016/10/11/000455)
* [[持續交付實踐] pipeline：pipeline使用之快速入門](https://testerhome.com/topics/10003)
