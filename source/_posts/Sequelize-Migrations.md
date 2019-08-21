---
title: Sequelize Migrations
date: 2019-07-02 16:54:34
categories:
  - Sequelize
tags:
  - Sequelize
  - Node js
---

> mysql 可以參考[這篇](https://ste5022424.github.io/2019/05/28/Mysql-on-Docker/)

## 1. Installing CLI

```bash
npm install --save sequelize
npm install --save sequelize-cli
npm install mysql2
```

## 2. Init

```bash
npx sequelize-cli init
```

![Init](./2019-07-02-17-07-31.png)

## 3. 設定相關連線資訊

![set](./2019-07-02-17-26-11.png)

## 4. Create Database

```bash
npx sequelize-cli db:create mydatabase
```

## 5. Create First Model

```bash
npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string
```

## 6. Running Migrations

```bash
npx sequelize-cli db:migrate
```

![Migrations](./2019-07-03-10-42-23.png)

## 7. Creating First Seed

```bash
npx sequelize-cli seed:generate --name demo-user
```

> seeders/xxxxxxxxxxxx-demo-user.js

```javascript
'use strict';

module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.bulkInsert(
      'Users',
      [
        {
          firstName: 'John',
          lastName: 'Doe',
          email: 'demo@demo.com',
          createdAt: new Date(),
          updatedAt: new Date()
        }
      ],
      {}
    );
  },

  down: (queryInterface, Sequelize) => {
    return queryInterface.bulkDelete('Users', null, {});
  }
};
```

## 8. Running Seeds

```bash
npx sequelize-cli db:seed:all
```

![Running Seeds](./2019-07-03-10-44-45.png)

## Reference

- [Sequelizejs](http://docs.sequelizejs.com/manual/migrations.html)
- [Sequelize-cli](https://www.npmjs.com/package/sequelize-cli)
