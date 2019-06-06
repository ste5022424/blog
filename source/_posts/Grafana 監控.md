---
title: 'Grafana 監控'
date: 2019-02-25 11:50:40
categories: 
- Grafana
tags: 
- Grafana
- Docker
- InfluxDb
- telegraf
---

# Grafana 監控

## [influxdb](https://hub.docker.com/_/influxdb/)

### 1. Docker Run

```bash
docker run -d -p 8083:8083 -p 8086:8086 -e INFLUXDB_ADMIN_ENABLED=true --name influxdb --restart=always -v influxdb:/var/lib/influxdb influxdb:1.1
```

![docker run](https://i.imgur.com/0oLjQzH.png)

### 2. 進入 influxdb (http://YourHost:8083)

![進入 influxdb](https://i.imgur.com/CkP0t3G.png)

### 3. 建立一個  grafana 資料庫

```bash
CREATE DATABASE "grafana"
```

![建立一個  grafana 資料庫](https://i.imgur.com/yCIRXMp.png)

### 4. 檢查是否建立成功

```bash
SHOW DATABASES
```

![檢查是否建立成功](https://i.imgur.com/nN52eAs.png)

## [grafana](https://hub.docker.com/r/grafana/grafana/)

### 1. Docker run

```bash
docker run -d -p 3000:3000 --link influxdb:influxdb --restart=always --name grafana grafana/grafana:4.6.2
```

![Docker run ](https://i.imgur.com/J7M3e8q.png)

### 2. 登入grafana <http://YourHost:3000)>

> 帳號跟密碼預設是 admin

![帳號跟密碼預設是 admin](https://i.imgur.com/zv65arG.png)

![帳號跟密碼預設是 admin](https://i.imgur.com/MFEJxKj.png)

### 3. Add data source

[!Add data source](https://i.imgur.com/4GvRimh.png)

![Add data source](https://i.imgur.com/SDNjczQ.png)

#### 3.1 Name

> Name 輸入 grafana

#### 3.2 HTTP settings

> URL輸入 <http://influxdb:8086> (influxdb為你的 containerau名稱)

#### 3.3 InfluxDB Details

> Database 輸入gragana

#### 設定完就可以看到 Grafana 與 InfluxDB 已經連結成功

![設定完就可以看到](https://i.imgur.com/HzHakcG.png)

## Telegraf

### [telegraf官網](https://www.influxdata.com/time-series-platform/telegraf/)

![telegraf官網](https://i.imgur.com/nlJIjUU.png)

### 1. [下載](https://dl.influxdata.com/telegraf/releases/telegraf-1.9.4_windows_amd64.zip)

### 2. 設定 [telegraf.conf](https://github.com/influxdata/telegraf)

![設定](https://i.imgur.com/VlY1Cf2.png)

#### 2.1. Input Plugins 使用 [win_perf_counters](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/win_perf_counters) 這個套件(官方預設套件)

![win_perf_counters](https://i.imgur.com/tTqZVrg.png)

#### 2.2  設定 Output influxdb

![設定](https://i.imgur.com/AtxDOGt.png)

### 3. 啟動服務

```bash
D:
cd D:\telegraf\
telegraf.exe -config D:\telegraf\telegraf.conf --service install
net start telegraf

```

![啟動服務](https://i.imgur.com/FXW0ePJ.png)

### 4. grafana 新增一個 dashborad

![新增一個](https://i.imgur.com/KiTs1PU.png)

![新增一個](https://i.imgur.com/d8Uy0zk.png)

#### 4.1 輸入 1902

> [1902 dashboards](https://grafana.com/dashboards/1902)

![1902 dashboards](https://i.imgur.com/6hjOm25.png)

![1902 dashboards](https://i.imgur.com/V9M6Xic.png)

#### 4.2 選擇 grafana db

![選擇 grafana db](https://i.imgur.com/6yReJH8.png)

#### 4.3 進入 grafana 就可以看到系統的資訊

![grafana](https://i.imgur.com/qOxQh4n.png)

# 參考

* [influxdb docker hub](https://hub.docker.com/_/influxdb/)
* [Grafana docker hub](https://hub.docker.com/r/grafana/grafana/)
* [telegraf官網](https://www.influxdata.com/time-series-platform/telegraf/)
* [telegraf git](https://github.com/influxdata/telegraf)
* [telegraf Input Plugins - win_perf_counters](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/win_perf_counters)