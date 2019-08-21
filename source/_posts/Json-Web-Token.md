---
title: Json Web Token
date: 2019-06-17 16:34:05
categories:
  - JWT
tags:
  - JWT
  - Node Js
---

## Json Web Token

```javascript
var jwt = require('jsonwebtoken');
var token = jwt.sign({ data: 'mydata' }, 'mysecret');
console.log(`Token : ${token}`);

var decode = jwt.verify(token, 'mysecret');
console.log(`Data : ${decode.data}`);
```

![jwt](./2019-06-17-16-40-23.png)

## Reference

- [JWT](https://jwt.io/)
- [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken)
