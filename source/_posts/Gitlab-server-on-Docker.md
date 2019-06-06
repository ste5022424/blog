---
title: Gitlab server on Docker
date: 2019-05-24 13:55:55
categories:
- Gitlab
tags:
- Gitlab
- Docker
---

# Gitlab server on Docker

```bash
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/etc/gitlab \
  --volume /srv/gitlab/logs:/var/log/gitlab \
  --volume /srv/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest

```

# 參考
* [GitLab Docker](https://docs.gitlab.com/omnibus/docker/)