---
title: Google OAuth
date: 2019-06-05 16:06:18
categories:
  - Google OAuth
tags:
  - Google OAuth
---

## Google OAuth

### 1. 建立一組 [Goole APIS Clinet ID](https://console.developers.google.com)

#### 1.1 憑證 > 建立憑證

![建立憑證](./2019-06-05-16-41-51.png)

#### 1.2 OAuth 用戶端 ID

![用戶端 ID](./2019-06-05-16-43-42.png)

#### 1.3 設定 來源網址 ＆ 重新導向 URL

![重新導向 URL](./2019-06-05-16-53-17.png)

> 因為 Goole 會驗證來源網址，所以網址必須是要公開的，為了方便測試這邊使用 [Surge](https://ste5022424.github.io/2018/11/02/surge/)建立一個對外的 Domain

#### 1.4 建立新增成功，取得用戶端 ID，

![取得用戶端](./2019-06-05-16-58-18.png)

### 2. 新增一個 index.html，貼上官方的範例，並將 ID 貼到範例提供的 meta 上面

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <script src="https://apis.google.com/js/platform.js" async defer></script>
    <meta
      name="google-signin-client_id"
      content="你的用戶端ID.apps.googleusercontent.com"
    />
    <title>Document</title>
  </head>

  <script>
    function onSignIn(googleUser) {
      var profile = googleUser.getBasicProfile();
      console.log('ID: ' + profile.getId()); // Do not send to your backend! Use an ID token instead.
      console.log('Name: ' + profile.getName());
      console.log('Image URL: ' + profile.getImageUrl());
      console.log('Email: ' + profile.getEmail()); // This is null if the 'email' scope is not present.
    }

    function signOut() {
      var auth2 = gapi.auth2.getAuthInstance();
      auth2.signOut().then(function() {
        console.log('User signed out.');
      });
    }
  </script>
  <body>
    <div class="g-signin2" data-onsuccess="onSignIn"></div>
    <a href="#" onclick="signOut();">Sign out</a>
  </body>
</html>
```

#### 2.1 [http://myoauth.surge.sh/](http://myoauth.surge.sh/#)

![page](./2019-06-05-17-04-27.png)

![login](./2019-06-05-17-08-51.png)

![data](./2019-06-05-17-10-13.png)

## 參考

- [ntegrating Google Sign-In into your web app](https://developers.google.com/identity/sign-in/web/sign-in)
- [Authenticate with a backend server](https://developers.google.com/identity/sign-in/web/backend-auth)
