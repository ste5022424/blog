---
title: android 遠程調試 WebView
date: 2019-05-06 18:40:24
categories:
- android
tags:
- android
- WebView
---

# android 遠程調試 WebView

## 1. 安卓 應用程式 加入 允許 debug

```
WebView.setWebContentsDebuggingEnabled(true);
```
## 2. 開啟 chrome >輸入網址 [chrome://inspect/#devices](chrome://inspect/#devices)

![SB 偵錯 ](https://i.imgur.com/lz9QidS.png)

## 3. 手機 > 設定 > 啟用 USB 偵錯

![](https://i.imgur.com/6GQYCax.png)

## 4. 手機進入 Webbview > 點選 inspect > 就可以針對 Webbview　進行偵錯

![](https://i.imgur.com/rsYvNdu.png)

# 參考
* [遠程調試 WebView](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/webviews?hl=zh-tw)