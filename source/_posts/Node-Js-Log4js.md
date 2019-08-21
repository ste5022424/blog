---
title: Node Js - Log4js
date: 2019-06-18 18:44:42
categories:
  - log4js
tags:
  - log4js
  - Node JS
---

## 1. install package

```bash
npm i config
npm i log4js
```

## 2. Creat config/default.json

```json
{
  "logger": {
    "appenders": {
      "file": {
        "type": "file",
        "filename": "logs/log.log",
        "maxLogSize": 104857600,
        "backups": 10,
        "layout": {
          "type": "json"
        }
      },
      "console": {
        "type": "console"
      }
    },
    "categories": {
      "default": {
        "appenders": ["file"],
        "level": "trace"
      }
    }
  }
}
```

## 3. Creat log.js

```javascript
const config = require('config');
const log4js = require('log4js');

log4js.addLayout('json', function(config) {
  return function(logEvent) {
    return JSON.stringify(logEvent);
  };
});

log4js.configure(config.logger);

module.exports = {
  log4js,
  getLogger: log4js.getLogger
};
```

## 4. Ceate index.js

```javascript
const logger = require('./log').getLogger('logtest');
logger.trace('testTrace');
logger.debug('testDebug');
logger.info('testInfo');
logger.warn('testWarn');
logger.error('testError');
logger.fatal('testFatal');
```

## 5. Run

```bash
node index.js
```

![index](./2019-06-19-10-26-02.png)

> [Demo](https://github.com/ste5022424/log4j_demo.git)

## Reference

- [log4js](https://www.npmjs.com/package/log4js)
- [log4js-node.github.io](https://log4js-node.github.io/log4js-node/)
