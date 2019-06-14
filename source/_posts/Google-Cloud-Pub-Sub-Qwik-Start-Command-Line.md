---
title: 'Google Cloud Pub/Sub: Qwik Start - Command Line'
date: 2019-06-10 15:31:21
categories:
- GCP Pub/Sub
tags:
- GCP Pub/Sub
---

## Google Cloud Pub/Sub: Qwik Start - Command Line

### Set Project ID 設定 Project ID

```bash
gcloud config set project qwiklabs-gcp-5c43d7b7f27776fe
```

## Topics

### Create Pub/Sub Topics 建立主題

```bash
gcloud pubsub topics create myTopic
gcloud pubsub topics create Test1
gcloud pubsub topics create Test2
```

### Delete Topics 刪除主題

```bash=
gcloud pubsub topics delete Test1
```

## Subscriptions

### Create Subscriptions 建立訂閱

```bash
gcloud pubsub subscriptions create --topic myTopic mySubscription
```

### Delete Subscription 刪除主題

```bash
gcloud pubsub subscriptions delete mySubscription
```

### Autoack

```bash
gcloud pubsub subscriptions pull mySubscription --auto-ack
```

## Publish

### Publish message 加入 Message 至 Topic

```bash
gcloud pubsub topics publish myTopic --message "Hello"
```

## Pull

### Pull Message

```bash=
gcloud pubsub subscriptions pull mySubscription --auto-ack --limit=3
```

> --limit=3 取得前三個

## Reference

* [Google Cloud Pub/Sub: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/925?catalog_rank=%7B%22rank%22%3A5%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=2711958)
* [將 Cloud Pub/Sub 與 Node.js 搭配使用](https://cloud.google.com/nodejs/getting-started/using-pub-sub?hl=zh-tw)
* [nodejs-pubsub](https://github.com/googleapis/nodejs-pubsub)
