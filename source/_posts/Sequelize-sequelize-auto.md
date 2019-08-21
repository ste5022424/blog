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

> 自動產生資料庫關聯模型

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
sequelize-auto -o "./models" -d tablename -h localhost -u my_username -p 5432 -x my_password -e mysql
```

### 4. User.js

> 這時候就會產生一個跟資料庫對應的模型(/model/User.js)
> 如果欄位自動號碼的話記得加上 （autoIncrement: true)

```javascript

/* jshint indent: 2 */

module.exports = function (sequelize, DataTypes) {
  return sequelize.define('User', {
    ID: {
      type: DataTypes.INTEGER(11),
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
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

![model](./2019-06-14-15-43-05.png)

### 5. sequelize.js

```javascript
const Sequelize = require('sequelize');
const config = require('config');

module.exports = new Sequelize(config.db.database, config.db.user, config.db.password, {
    host: config.db.host,
    dialect: 'mysql',
    define: {
        timestamps: false
    }
});

```

### 6. index.js

```javascript
const Sequelize = require('sequelize');
const sequelize = require('./database/sequelize/sequelize')
const User = require('./models/User')(sequelize, Sequelize);

// Find all users
User.findAll().then(users => {
    console.log("All users:", JSON.stringify(users, null, 4));
});

// Insert
User.create({
    Name: 'Tom',
    Telephone: '09097895541s',
    Age: '20'
}).then(the => {
    console.log(`Insert OK >> ID:${the.ID}`);
});

// Delete
User.destroy({
    where: {
        Name: "Tom"
    }
}).then(() => {
    console.log(`Delete Tom Done`);
});

// Update
User.update({ Name: "WuWu" }, {
    where: {
        Name: "Wu"
    }
}).then(() => {
    console.log("Update Wu Done");
});

```

![shoe](./2019-06-14-15-46-33.png)

## [Demo](https://github.com/ste5022424/sequelize_demo.git)

## Reference

* [sequelizejs](http://docs.sequelizejs.com/manual/getting-started.html)
* [sequelize-auto](https://github.com/sequelize/sequelize-auto)
