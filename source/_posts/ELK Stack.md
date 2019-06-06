---
title: ELK Stack
date: 2019-01-09 17:00:00
categories:
- ELK Stack
tags:
- ELK Stack
- Docker
- Elasticsearch
- Kibana
- Logstash
---

# ELK Stack
ELK Stack 是 Elasticsearch、Logstash、Kibana這三個Open Source專案

![](https://i.imgur.com/Fk7k1EP.png)


### Elasticsearch 

> Elasticsearch是用於分佈式搜索和實時數據進行分析的平台

### Kibana 

> Kibana是讓Elasticsearch儲存的數據視覺化的平台

### Logstash

> 日誌搜集工具

### Beat

> Beats是一系列產品的統稱，屬於ElasticStack裡面收集數據的這一層


#  Docker Run ELK

## 1. Install Dokcer

```
curl -fsSL https://get.docker.com/ | sh
```
#### Dokcer 指令
>  -d 背景執行
    --name 名稱
    --restart=always 自動重啟
    -p port
    -V 指定資料夾位置

## 2. Run elasticsearch


### 2-1. Creat elasticsearch 持久層資料夾跟設定權限

```
mkdir -m 777 /data/elasticsearch
```

### 2-2. Run elasticsearch 之前要先設定 [max_map_count](https://github.com/docker-library/elasticsearch/issues/111)

```
sudo sysctl -w vm.max_map_count=262144
```
### 2-3. docker run

```
docker run  -d -p 9200:9200 -p 9300:9300 --name elasticsearch -v /data/elasticsearch:/usr/share/elasticsearch/data docker.elastic.co/elasticsearch/elasticsearch:6.5.4
```
> [Install Elasticsearch with Docker](https://www.elastic.co/guide/en/elasticsearch/reference/6.5/docker.html#docker)
> 
### 2-4 Preview elasticsearch

```
curl 127.0.0.1:9200
```
![](https://i.imgur.com/DspQBxW.png)

## 3. Run kibana

### 3-1 docker run
```
docker run -d --name kibana --restart=always -p 5601:5601 --link elasticsearch:elasticsearch docker.elastic.co/kibana/kibana:6.5.4
```
> [Run kibana with Docker](https://www.elastic.co/guide/en/kibana/6.5/docker.html)

> Set [kibana.yml](https://www.elastic.co/guide/en/kibana/6.5/settings.html)

### 3-2 Preview kibana(http://yourhost:5601)

![](https://i.imgur.com/NRw4J3U.png)

### 3-3  Check kibana status (http://yourhost:5601/status)

![](https://i.imgur.com/LUBhBbr.png)

## 4. Run Logstash

### 4-1 Run [donetcoreapi](https://ste5022424.github.io/2019/01/04/Net-Core-Nlog/)

#### Run
![](https://i.imgur.com/2lT45G1.png)
#### Log
![](https://i.imgur.com/zoE34DD.png)

### 4-2 Creat logstash.conf

#### Creat in /tmp/logstash/pipeline/
```
cd ..
cd /tmp/logstash/pipeline/
vi logstash.conf
```
#### logstash.conf
```
file {
    path => "/usr/share/logstash/Log/*"
    type => "file"
    start_position => "beginning"
   }
 }

filter {
    grok {
           match => ["message", "%{TIMESTAMP_ISO8601:[@metadata][timestamp]} %{NUMBER:threadid} %{LOGLEVEL:loglevel} %{NOTSPACE:logger} %{GREEDYDATA:message}"]
           overwrite => [ "message" ]
        }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "logstash-test"  
   }
  stdout { codec => rubydebug}
}
```
> [logstash pattern](https://github.com/elastic/logstash/blob/v1.4.2/patterns/grok-patterns)

> [Grok filter plugin](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html)
### 4-3 docker run
```
docker run it ---name logstash --link elasticsearch:elasticsearch -v /tmp/logstash/pipeline:/usr/share/logstash/pipeline/ -v /tmp/Log/:/usr/share/logstash/Log/ docker.elastic.co/logstash/logstash:6.5.4
```

> /tmp/Log/:/usr/share/logstash/Log/   → [donetcoreapi](https://ste5022424.github.io/2019/01/04/Net-Core-Nlog/) log 共用至 logstash
 
> /tmp/logstash/pipeline:/usr/share/logstash/pipeline/ →  自定義 logstash.conf

> [Configuring Logstash for Docker](https://www.elastic.co/guide/en/logstash/6.5/config-setting-files.html)
  
### 4-4 Push to elasticsearch

#### attach  logstash
```
docker attach logstash
```
![](https://i.imgur.com/H5u5hz5.png)

### 4-4 Set kibana

#### Set index
![](https://i.imgur.com/JZOrSEX.png)

#### Set Time Filter
![](https://i.imgur.com/jfVaVXd.png)

#### Discover
![](https://i.imgur.com/0GrJwU1.png)

## 5. Filebeat

> 官網的[架構圖](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html)可以知道 Filebeat 是一個搜集器，它可以把 log 蒐集起來之後往後面送

![架構圖](https://i.imgur.com/l9fRRUE.png)


> Integrating with Messaging Queuesedit

> 在Log量很大的情況下，會使用 MessagQueue 來減輕負擔，以下是官方網站的[架構圖](https://www.elastic.co/guide/en/logstash/current/deploying-and-scaling.html)

![架構圖](https://www.elastic.co/guide/en/logstash/current/static/images/deploy4.png)

> filebeat 蒐集log後，推送到 kafka，logstash 訂閱 kafka，logstash 從 kafa 抓資料後，再將 log parser，然後再送到 elasticsearch ，最後再由 kibana 顯示資料

## 5.1 Docker  run [Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/running-on-docker.html#_custom_image_configuration)

> Dockerfile

```bash
FROM docker.elastic.co/beats/filebeat:6.6.2
COPY filebeat.yml /usr/share/filebeat/filebeat.yml
USER root
RUN chown root:filebeat /usr/share/filebeat/filebeat.yml
USER filebeat
```

> [Configure the Logstash output](https://www.elastic.co/guide/en/beats/filebeat/master/kafka-output.html)

## 參考

* [installing-elastic-stack](https://www.elastic.co/guide/en/elastic-stack/current/installing-elastic-stack.html)
* [deploying-and-scaling](https://www.elastic.co/guide/en/logstash/6.5/deploying-and-scaling.html)
* [官方網站](https://www.elastic.co/cn/elk-stack)