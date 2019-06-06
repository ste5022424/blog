---
title: 'C# HttpWebRequest Expect:100-continue'
date: 2019-03-20 20:31:18
categories:
- HttpWebRequest
tags:
- HttpWebRequest
- C#
- 筆記
---

# HttpWebRequest Expect:100-continue'

> 使用 .net HttpWebRequest Post時，碰到第三方串接商API無回應，導致 Reseponse TimeOut，使用 Fiddler 攔了一下，發現Header多了一個 "Expect:100-continue"，原來第三方串接商API不支援，所以才會沒有回應導致Reseponse Timeout，把 Expect100Continue 設定成  false 就可以解決了

```C#
HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create("Url");
request.ServicePoint.Expect100Continue = false;
```

![Fiddler](https://i.imgur.com/v9iKHBX.png)

# 參考

* [How to disable the “Expect: 100 continue” header in HttpWebRequest for a single request?](https://stackoverflow.com/questions/14063327/how-to-disable-the-expect-100-continue-header-in-httpwebrequest-for-a-single)
* [Expect:100-continue](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/100)
[100 Continue
](http://www.laruence.com/2011/01/20/1840.html)