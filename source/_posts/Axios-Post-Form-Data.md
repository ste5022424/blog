---
title: Axios Post Form Data
date: 2019-05-31 10:26:33
categories:
- Axios
tags:
- Axios
- Node JS
---

# Axios Post Form Data

## 安裝套件

```base
npm init
npm install axios
npm i qs
```

## Code

```javascript
const axios = require('axios');
const qs = require('qs');

let formdata = qs.stringify({
    Name: 'Andy',
    Age : 18
});

axios({
    method: 'post',
    url: 'Your Url',
    data: formdata,
    config: { headers: { 'Content-Type': 'application/x-www-form-urlencoded' } }
})
    .then(function (response) {
        //handle success
        console.log(response.data);
    })
    .catch(function (response) {
        //handle error
        console.log(response);
    });

```

# 參考
* [axios](https://github.com/axios/axios)
* [qs](https://www.npmjs.com/package/qs)