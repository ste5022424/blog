---
title: 使用 Hexo 建立 Github Blog
date: 2018-10-17 17:23:06
categories:
- Hexo
tags:
- Hexo
---

## 事先安裝

* [Git](https://git-scm.com/)
* [Node js](https://https://nodejs.org/en/) 
* [Visual Studio Code](https://code.visualstudio.com/)

### Github 新增.github.io專案

![Github](https://i.imgur.com/PO7dlOS.png)

## 安裝 Hexo

```bash=
npm install hexo-cli -g
```

![](https://i.imgur.com/5rz5CHP.png)

## 建立專案

```bash=
hexo init D:\\blog
```

![](https://i.imgur.com/59eoBCu.png)

### 使用 vs code 開啟
![](https://i.imgur.com/SeD9liQ.png)

### 更換部落格樣式
#### 挑選自己喜歡的主題
https://hexo.io/themes/index.html
![](https://i.imgur.com/a8KgChZ.png)

#### 取得套件(以 Noise為範例)

![](https://i.imgur.com/WIA4TRG.png)

```bash=
git clone https://github.com/iissnan/hexo-theme-next.git ./themes/Noise
```

#### 設定 _config.yml

![](https://i.imgur.com/sdYrMVo.png)

```bash=
theme: Noise
```

### 啟動server
![](https://i.imgur.com/Y3UI7EA.png)

```
hexo s -p 8080
```
#### 檢視網站
![](https://i.imgur.com/MQAv634.png)

### 發佈到自己的Github

#### 安裝 hexo-deployer-git。
![](https://i.imgur.com/Jd0uVhz.png)
```
npm install hexo-deployer-git --save
```
#### 設定_config.yml
```
deploy:
  type: git
  repo: https://github.com/yourUsername/yourUsername.github.io.git
  branch: master
```
![](https://i.imgur.com/p2eoUwL.png)

#### 部屬至 github

![](https://i.imgur.com/KiO1WNm.png)
```
hexo deploy
```
#### 檢視網站
![](https://i.imgur.com/wAw1gfC.png)

### 建立第一篇文章

#### 建立文章
![](https://i.imgur.com/rkrC6xS.png)
```
hexo new "使用 Hexo 建立 Github Blog"
```
#### 編輯文章

![](https://i.imgur.com/ClTN0Q7.png)

### 建立網站 categories
#### 新增一個 categories 頁面
![](https://i.imgur.com/Alwebxp.png)

```
hexo new page categories
```

#### 編輯 categories/index.md
![](https://i.imgur.com/6MkMNVk.png)
```
---
title: 文章分類
date: 2018-10-17 18:25:40
type: "categories"
---
```
#### 在文章上加入 categories
![](https://i.imgur.com/cMKKYti.png)

````
---
title: 使用 Hexo 建立 Github Blog
date: 2018-10-17 17:23:06
tags: 
categories:
- 學習
---
````

![](https://i.imgur.com/VrItgdZ.png)

### 建立網站 tag
#### 新增一個 tags 頁面

````
hexo new page tags
````
![](https://i.imgur.com/53PecP6.png)


#### 編輯 tags/index.md
![](https://i.imgur.com/WfD3HDq.png)
````
---
title: tags
date: 2018-10-17 18:40:57
type: "tags"
---
````
#### 在文章上加入 tags
![](https://i.imgur.com/vCQUMWW.png)
````
---
title: 使用 Hexo 建立 Github Blog
date: 2018-10-17 17:23:06
tags:
- Hexo
categories:
- 學習
---
````

### 搜尋功能

#### 安裝 hexo-generator-search
[hexo-generator-search](
https://www.npmjs.com/package/hexo-generator-search)

```
npm install hexo-generator-search --save
```
####  在_config.yml 找到 local_search 將 enable 設定為true

![](https://i.imgur.com/pdUPxJC.png)

![](https://i.imgur.com/sid0Bvr.png)

![](https://i.imgur.com/oawpKOu.png)


## 參考網址
Hexo 官方網站 : https://hexo.io/zh-tw/
Hexo 文件 :https://hexo.io/zh-tw/api/
Hexo Them :https://hexo.io/themes/index.html
[Hexo使用攻略-添加分类及标签](https://linlif.github.io/2017/05/27/Hexo%E4%BD%BF%E7%94%A8%E6%94%BB%E7%95%A5-%E6%B7%BB%E5%8A%A0%E5%88%86%E7%B1%BB%E5%8F%8A%E6%A0%87%E7%AD%BE/)
[[Hexo] 快速上手 Hexo 網誌框架](https://oawan.me/2016/easy-hexo-easy-blog/)
[可能是最詳細的 Hexo + GitHub Pages 搭建部落格的教程](http://www.lovebxm.com/2018/06/24/hexo-github-blog/)
[用Hexo + Github Pages搭建個人部落格](https://yogapan.github.io/2017/08/11/%E7%94%A8Hexo-Github-Pages%E6%90%AD%E5%BB%BA%E5%80%8B%E4%BA%BA%E9%83%A8%E8%90%BD%E6%A0%BC/#comments)
[Hexo的NexT主题个性化：添加文章阅读量](http://www.jeyzhang.com/hexo-next-add-post-views.html)
[Sign up to Leancloud and create an app](https://github.com/theme-next/hexo-theme-next/blob/master/docs/LEANCLOUD-COUNTER-SECURITY.md)