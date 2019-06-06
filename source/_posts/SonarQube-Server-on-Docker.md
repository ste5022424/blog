---
title: SonarQube Server on Docker
date: 2019-01-15 16:34:30
categories:
- SonarQube
tags:
- SonarQube
- Docker
- docker-compose
- PostgreSql
---

## SonarQube Server on Docker

### 1. 建立持久層資料夾

```
mkdir -p -m 777 ./sonarqube && mkdir -p -m 777 ./sonarqube/conf && mkdir -p -m 777 ./sonarqube/data && mkdir -p -m 777 ./sonarqube/logs && mkdir -p -m 777 ./sonarqube/extensions
```

### 2. docker-compose.yml

```
version: "3.5"
services:
    postgresql:
                container_name: "postgresql"
                image: "postgres"
                ports:
                - "5432:5432"
                volumes:
                - "/postgresql:/var/lib/postgresql/data"
                environment:
                - "POSTGRES_USER=sonar"
                - "POSTGRES_PASSWORD=sonar"
                restart: always
    sonarqube:
                container_name: "sonarqube"
                image: "sonarqube:7.7-community"
                ports:
                - "9000:9000"
                volumes:
                - "/sonarqube/conf:/opt/sonarqube/conf"
                - "/sonarqube/data:/opt/sonarqube/data"
                - "/sonarqube/logs:/opt/sonarqube/logs"
                - "/sonarqube/extensions:/opt/sonarqube/extensions"
                environment:
                - "sonar.jdbc.username=sonar"
                - "sonar.jdbc.password=sonar"
                - "sonar.jdbc.url=jdbc:postgresql://postgresql/sonar"
                links:
                - "postgresql:postgresql"
                restart: always

```

### ADserver 設定

> [設定](https://docs.sonarqube.org/latest/instance-administration/delegated-auth/)
> [LDAP Plugin](https://docs.sonarqube.org/display/SONARQUBE67/LDAP+Plugin)
> [团队环境：代码质量管理SonarQube安装](https://blog.frognew.com/2017/05/install-sonarqube.html)

#### 1. 將 sonar.properties 放置 SONARQUBE_HOME/conf/sonar.properties

```bash=

# General Configuration
# LDAP configuration
sonar.security.realm=LDAP
sonar.authenticator.createUsers=true
sonar.security.savePassword=true
sonar.security.updateUserAttributes=true

ldap.url=ldap://YourAdServer
ldap.bindDn=bindDn
ldap.bindPassword=bindPassword

# User Configuration
ldap.user.baseDn=baseDn
ldap.user.request=(&(objectClass=user)(sAMAccountName={login}))

```

#參考
* [sonarqube-postgres-docker.md](https://gist.github.com/ceduliocezar/b3bf93125024482b5f2f479696842046)
* [postgres docker](https://hub.docker.com/_/postgres)
* [sonarqube docker](https://hub.docker.com/_/sonarqube/)