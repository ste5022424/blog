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
quickstart();
```

## 6. Create Subscription

```javascript
async function createSubscription(topicName, subscriptionName) {
  // [START pubsub_create_pull_subscription]
  // Imports the Google Cloud client library
  const { PubSub } = require('@google-cloud/pubsub');

  // Creates a client
  const pubsub = new PubSub();

  /**
   * TODO(developer): Uncomment the following lines to run the sample.
   */
  // const topicName = 'my-topic';
  // const subscriptionName = 'my-sub';

  // Creates a new subscription
  await pubsub.topic(topicName).createSubscription(subscriptionName);
  console.log(`Subscription ${subscriptionName} created.`);

  // [END pubsub_create_pull_subscription]
}
createSubscription('my-topic', 'my-topic-Subscription');
```

## 7. Push Message

```javascript
async function publishMessage(topicName, data) {
  // [START pubsub_publish]
  // [START pubsub_quickstart_publisher]
  // Imports the Google Cloud client library
  const { PubSub } = require('@google-cloud/pubsub');

  // Creates a client
  const pubsub = new PubSub();

  /**
   * TODO(developer): Uncomment the following lines to run the sample.
   */
  // const topicName = 'my-topic';
  // const data = JSON.stringify({ foo: 'bar' });

  // Publishes the message as a string, e.g. "Hello, world!" or JSON.stringify(someObject)
  const dataBuffer = Buffer.from(data);

  const messageId = await pubsub.topic(topicName).publish(dataBuffer);
  console.log(`Message ${messageId} published.`);

  // [END pubsub_publish]
  // [END pubsub_quickstart_publisher]
}
publishMessage('my-topic', 'TestData');
```

## 8. Pull Message

```javascript
function listenForMessages(subscriptionName, timeout) {
  // [START pubsub_subscriber_async_pull]
  // [START pubsub_quickstart_subscriber]
  // Imports the Google Cloud client library
  const { PubSub } = require('@google-cloud/pubsub');

  // Creates a client
  const pubsub = new PubSub();

  /**
   * TODO(developer): Uncomment the following lines to run the sample.
   */
  // const subscriptionName = 'my-sub';
  // const timeout = 60;

  // References an existing subscription
  const subscription = pubsub.subscription(subscriptionName);

  // Create an event handler to handle messages
  let messageCount = 0;
  const messageHandler = message => {
    console.log(`Received message ${message.id}:`);
    console.log(`\tData: ${message.data}`);
    console.log(`\tAttributes: ${message.attributes}`);
    messageCount += 1;

    // "Ack" (acknowledge receipt of) the message
    message.ack();
  };

  // Listen for new messages until timeout is hit
  subscription.on(`message`, messageHandler);

  setTimeout(() => {
    subscription.removeListener('message', messageHandler);
    console.log(`${messageCount} message(s) received.`);
  }, timeout * 1000);
  // [END pubsub_subscriber_async_pull]
  // [END pubsub_quickstart_subscriber]
}
listenForMessages('my-topic-Subscription', 3);
```

> [範例](https://github.com/ste5022424/GcpPubSub)

## Reference

- [nodejs-pubsub](https://github.com/googleapis/nodejs-pubsub)
- [將 Cloud Pub/Sub 與 Node.js 搭配使用](https://cloud.google.com/nodejs/getting-started/using-pub-sub?hl=zh-tw)
- [Google Cloud Pub/Sub: Node.js Client](https://www.npmjs.com/package/@google-cloud/pubsub)
