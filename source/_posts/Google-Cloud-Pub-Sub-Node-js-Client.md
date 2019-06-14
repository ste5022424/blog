---
title: 'Google Cloud Pub/Sub: Node.js Client'
date: 2019-06-10 15:12:30
categories:
- GCP Pub/Sub
tags:
- GCP Pub/Sub
- Node.js
---

## Google Cloud Pub/Sub: Node.js Client

## 1. 啟用 [API 服務](https://console.developers.google.com/apis/library/pubsub.googleapis.com?q=pub&id=e5839763-4006-424c-89ae-49057442b67a&project=green-cell-242807)

![API 服務](https://i.imgur.com/qGZefyd.png)

## 2. [建立服務帳戶金鑰](https://console.cloud.google.com/apis/credentials/)

![建立服務帳戶金鑰](https://i.imgur.com/nyJzv1P.png)

![建立服務帳戶金鑰](https://i.imgur.com/H39UREY.png)

## 3. [啟用驗證](https://cloud.google.com/docs/authentication/getting-started#auth-cloud-implicit-nodejs)

> 將下載的檔案放到專案中並指定路徑

```bash
export GOOGLE_APPLICATION_CREDENTIALS="[PATH]"
```

## 4. install Package

```bash
npm install @google-cloud/pubsub
```

## 5. Create Topic

```javascript
// Imports the Google Cloud client library
const { PubSub } = require('@google-cloud/pubsub');

async function quickstart(
  projectId = 'your-project-id', // Your Google Cloud Platform project ID
  topicName = 'my-topic' // Name for the new topic to create
) {
  // Instantiates a client
  const pubsub = new PubSub({ projectId });

  // Creates the new topic
  const [topic] = await pubsub.createTopic(topicName);
  console.log(`Topic ${topic.name} created.`);
}
```

## 6. Run

![Run](https://i.imgur.com/lstmT7J.png)

## Reference

- [nodejs-pubsub](https://github.com/googleapis/nodejs-pubsub)
- [將 Cloud Pub/Sub 與 Node.js 搭配使用](https://cloud.google.com/nodejs/getting-started/using-pub-sub?hl=zh-tw)
- [Google Cloud Pub/Sub: Node.js Client](https://www.npmjs.com/package/@google-cloud/pubsub)
