---
title: Slack Incoming Webhooks
date: 2019-03-07 15:55:46
categories:
- Slack
tags:
- Slack
- Incoming Webhooks
---
# Slack Incoming Webhooks

## 1. 建立 Slack app

![ Slack app ](https://i.imgur.com/Eff4v91.png)

![Slack app](https://i.imgur.com/KmXrjtJ.png)

![Slack app](https://i.imgur.com/JQ5extf.png)

> App Name: 應用程式名稱
> Workspace: 選擇一個 Workspace ，如果沒有就建立一個

## 2.選擇 Incoming Webhooks

![Incoming Webhooks](https://i.imgur.com/3orCXKV.png)

## 3. 將開關打開

![將開關打開](https://i.imgur.com/3Zb16k7.png)

![將開關打開](https://i.imgur.com/P5DQmEu.png)

## 4. 先在 slack 上面建立一個頻道

![建立一個頻道](https://i.imgur.com/z1RrkOP.png)

![建立一個頻道](https://i.imgur.com/Eycl1uJ.png)

![建立一個頻道](https://i.imgur.com/OW8GBXE.png)

![建立一個頻道](https://i.imgur.com/7E0dji9.png)

### 5. Add New Webhook to Workspace

![Add New Webhook to Workspace](https://i.imgur.com/3Mntuo1.png)

![Add New Webhook to Workspace](https://i.imgur.com/qP7F4pb.png)

## 6. 複製網址

![複製網址](https://i.imgur.com/s3jRDZY.png)

## 7. 發送訊息

>使用 [Restlet Client - REST API Testing](https://chrome.google.com/webstore/detail/restlet-client-rest-api-t/aejoelaoggembcahagimdiliamlcdmfm) 來測試post

![發送訊息](https://i.imgur.com/AqRyHPU.png)

>channel:頻道名稱
>text:要發送的data

```json
{
  "channel":"myhooktest",
   "text": "Hello, world.ipblock"
}
```

## 8. 確認有收到訊息

![收到訊息](https://i.imgur.com/NGe3FxW.png)

# 參考
* [Incoming Webhooks](https://api.slack.com/incoming-webhooks)