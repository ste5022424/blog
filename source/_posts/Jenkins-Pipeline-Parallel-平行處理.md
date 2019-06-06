---
title: Jenkins Pipeline Parallel 平行處理
date: 2018-12-21 15:32:46
categories:
- Jenkins
tags:
- Jenkins
- Pipeline Parallel
---

## Jenkins Pipeline Parallel 平行處理


### 將 parallel 語法設定在專案上
![](https://i.imgur.com/BYD3cvl.png)

> parallel  範例如下
```
node {

   stage('Git Clone') {
       echo "Git Clone OK"
   }
   stage('Nuget Restore') {
       echo "Nuget Restore OK"
   }
   stage('Msbuild') {
       echo "Msbuild OK"
   }

 parallel (
  "Push": {
    stage("Push Server") {
       echo "Push OK"
    }
  },
  "Scan Code": {
    stage("Scan Code") {
        echo " Scan Code OK"
    }
  }
 )
}
```

### Jenkins 上可以看到建置過程
![](https://i.imgur.com/e67Wju4.png)

### Blue Ocean 就可以看到 建置過程是有水平執行
![](https://i.imgur.com/WmTbRhY.png)

> 要看到Blue Ocean圖形可以參考這篇安裝 [Jenkins Pipeline Blue Ocean](https://ste5022424.github.io/2018/12/20/Jenkins-Pipeline-Blue-Ocean/)

## 參考

* [What's New in Declarative Pipeline 1.3: Sequential Stages](https://jenkins.io/blog/2018/07/02/whats-new-declarative-piepline-13x-sequential-stages/)