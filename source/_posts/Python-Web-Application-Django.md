---
title: Python Web Application Django
date: 2018-11-14 15:32:10
categories:
- python
tags:
- Python
- Django
- Visual Studio Code
---
## Writing your first Django app

### 建立專案

```
django-admin startproject mysite

 mysite/urls.py
```

![](https://i.imgur.com/BYPZQIH.png)

### 啟動 Server

```
python manage.py runserver
```
![](https://i.imgur.com/JU85NzY.png)

![](https://i.imgur.com/zDb7byA.png)

### 建立 Polls App
```
python manage.py startapp polls
```
![](https://i.imgur.com/upH5XoD.png)

#### 建立一個 views.py

```
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

![](https://i.imgur.com/V47boWo.png)

#### 建立一個 urls.py

```
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

![](https://i.imgur.com/fDb7ZSY.png)

##### 修改 mysite/urls.py

```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```
![](https://i.imgur.com/gzYI2UE.png)

#### 在 run 一次就可以看到剛剛寫的 Hello, world. You're at the polls index.

```
python manage.py runserver
```

![](https://i.imgur.com/RLjX5c4.png)


# 參考
* [Writing your first Django app, part 1](https://docs.djangoproject.com/en/2.1/intro/tutorial01/)

* [Use Django in Visual Studio Code](https://code.visualstudio.com/docs/python/tutorial-django)