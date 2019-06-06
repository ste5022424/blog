---
title: '升級 Jenkins ver. 2.151 發生問題'
date: 2018-11-20 16:49:02
categories: 
- Jenkins
tags: 
- Jenkins
---
## 升級 Jenkins ver. 2.151 發生問題

org.apache.commons.jelly.JellyTagException:jar:file:/D:/Jenkins/war/WEB-INF/lib/jenkins-core-2.151.jar!/lib/layout/hasPermission.jelly:35:20: <d:invokeBody> com/trilead/ssh2/crypto/Base64

![升級](https://i.imgur.com/1H5x5TZ.png)

## issue

<https://issues.jenkins-ci.org/browse/JENKINS-54708>
<https://issues.jenkins-ci.org/browse/JENKINS-54686?focusedCommentId=354378&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel#comment-354378>

### 問題是發生SSH Slaves版本(1.29.0)不相容，所以降版至(1.28.1)就可以了

>因為jenkins掛掉了，所以要手動更新

### 先找到要下載的pluin [ssh-slaves.hpi](http://updates.jenkins-ci.org/download/plugins/)

![下載](https://i.imgur.com/MN9ATxE.png)
![下載](https://i.imgur.com/7DDIV6T.png)

### 下載 [jenkins-cli.jar](https://wiki.jenkins.io/display/JENKINS/Jenkins+CLI)

```bash
https://你的jenkins網址/jnlpJars/jenkins-cli.jar
```

### 使用 [jenkins-cli.jar 手動安裝](https://jenkins.io/doc/book/managing/plugins/#install-with-cli)

```bash
java -jar jenkins-cli.jar -s http://127.0.0.1 install-plugin http://updates.jenkins-ci.org/download/plugins/ssh-slaves/1.28.1/ssh-slaves.hpi -restart
```

![手動安裝](https://i.imgur.com/UZkX9KM.png)

> 如果有權限不足，先調整權限，之後再刪除 [config.xml](https://blog.csdn.net/myNameIssls/article/details/70227838)

![權限不足](https://i.imgur.com/k9IF6yL.png)

```bash
<permission>hudson.model.Hudson.Administer:anonymous</permission>
<permission>hudson.model.Hudson.ConfigureUpdateCenter:anonymous</permission>
<permission>hudson.model.Hudson.Read:anonymous</permission>
<permission>hudson.model.Hudson.RunScripts:anonymous</permission>
<permission>hudson.model.Hudson.UploadPlugins:anonymous</permission>
```

### 重新啟動 jenkins 就可以了

![重新啟動](https://i.imgur.com/WSE6PIE.png)
