---
title: Sequelize-sequelize-auto
date: 2019-06-14 12:00:55
categories:
- Sequelize
tags:
- Sequelize
- Node js
---

## Sequelize-sequelize-auto

### 1. install sequelize-auto

``` bash
npm install -g sequelize-auto
```
### 2. install mysql

``` bash
npm install -g mysql
```

### 3. Run sequelize-auto

```bash
sequelize-auto -o "./models" -d sequelize_auto_test -h localhost -u my_username -p 5432 -x my_password -e postgres
```

> 這時候就會產生一個跟資料庫對應的模型

![model](./2019-06-14-15-43-05.png)

```javascript

/* jshint indent: 2 */

module.exports = function (sequelize, DataTypes) {
  return sequelize.define('User', {
    ID: {
      type: DataTypes.INTEGER(11),
      allowNull: false,
      primaryKey: true
    },
    Name: {
      type: DataTypes.STRING(50),
      allowNull: false
    },
    Telephone: {
      type: DataTypes.STRING(20),
      allowNull: true
    },
    Age: {
      type: DataTypes.INTEGER(11),
      allowNull: true
    }
  }, {
      tableName: 'User',
      timestamps: false
    });
};

```

### 4. import model

```javascript

const Sequelize = require('sequelize');
const sequelize = require('../database/sequelize/sequelize');
const User = require('../models/User')(sequelize, Sequelize);

// Find all users
User.findAll().then(users => {
    console.log("All users:", JSON.stringify(users, null, 4));
});

```

![shoe](./2019-06-14-15-46-33.png)

## Reference

* [sequelizejs](http://docs.sequelizejs.com/manual/getting-started.html)
* [sequelize-auto](https://github.com/sequelize/sequelize-auto)
