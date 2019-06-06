---
title: Express Web Hello World
date: 2019-05-13 11:45:30
categories:
- Express
tags:
- Express
- Node Js
---

# Express Web Hello World

> Express 是最小又靈活的 Node.js Web 應用程式架構，為 Web 與行動式應用程式提供一組健全的特性。

## 1. 安裝 express 套件

```bash
npm install express --save
```

## 2. 新增 一個 app.js

```bash
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`)
```

## 3. Run node

```bash
node app.js
```

![node](https://i.imgur.com/WqQxqcU.png)

## 4. Hello World!

![Hello](https://i.imgur.com/82nZSdO.png)

# [RestfulAPI](http://expressjs.com/en/starter/basic-routing.html) 實作 Get / Post / Put / Delete

```bash
const express = require('express')
const app = express()
const port = 3000

//// RestfulAPI

// get
app.get('/myget', (req, res) => 
res.send('Hello World myget!')
)

//  post
app.post('/mypost', function (req, res) {
    res.json({ RestfulAPI: 'mypost' })
})

// put
app.put('/myput', function (req, res) {
    res.json({ RestfulAPI: 'myput' })
})

// delete
app.delete('/mydelete', function (req, res) {
    res.json({ RestfulAPI: 'mydelete' })
})

```

### Get

> http://localhost:3000/myget
 
![Get](https://i.imgur.com/KIEL2im.png)

### Post

> http://localhost:3000/mypost

![Post](https://i.imgur.com/NHb3yAh.png)

### Put

> http://localhost:3000/myput

![Put](https://i.imgur.com/PTcWcUh.png)

### Delete

> http://localhost:3000/mydelete

![Delete](https://i.imgur.com/5YN1uGj.png)

# [Static File](http://expressjs.com/en/starter/static-files.html)

```bash
const express = require('express')
const app = express()
const port = 3000

//// static files
app.use(express.static('static'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

![listen](https://i.imgur.com/vKhOU5L.png)

# 參考

* [expressjs](https://expressjs.com/zh-tw/starter/installing.html)