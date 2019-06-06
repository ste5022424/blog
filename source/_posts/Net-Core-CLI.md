---
title: .Net Core CLI run Docker Web API
date: 2018-12-28 10:19:04
categories:
- .net core
tags:
- .net core
- Docker
- .net core cli
- web api
---

先下載 [.net core sdk](https://dotnet.microsoft.com/download)

### .Net Core CLI run Docker Web API

```bash
dotnet new webapi -lang C#
```

![run](https://i.imgur.com/Cl6NlP2.png)

![](https://i.imgur.com/hmUgDAO.png)

### 執行站台

```bash
dotnet run
```

![dotnet](https://i.imgur.com/ZeOSddd.png)

![dotnet](https://i.imgur.com/97j7YQL.png)

### 打包 Docker Image 並執行 Docker Web API

#### Creat Dockerfile

```bash
echo Dockerfile > Dockerfile
```

 > 把官方網站的[範例](https://docs.docker.com/engine/examples/dotnetcore/)貼上去

```bash
FROM microsoft/dotnet:sdk as build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "donetcore.dll"]
```

#### Docker build

```bash
docker build -t apitest:v1 .
```

![docker](https://i.imgur.com/iN1NrFT.png)

#### Docker run

```bash
docker run -d  --name apitest -p 90:80 apitest:v1
```

#### 瀏覽 <http://127.0.0.1:90/api/values>

![瀏覽](https://i.imgur.com/BfEQqZn.png)

> [範例檔案](https://github.com/ste5022424/donetcorewebapi)

## 參考

* [Dockerize a .NET Core application](https://docs.microsoft.com/zh-tw/dotnet/core/tools/dotnet-new?tabs=netcore21)
* [Dockerize a .NET Core application](https://docs.docker.com/engine/examples/dotnetcore/)