---
title: 'GRPC C# Quickstart'
date: 2018-12-11 14:15:11
categories:
- GRPC
tags:
- GRPC
---

# GRPC Quickstart

## Clone GRPC

```bash
git clone -b v1.17.0 https://github.com/grpc/grpc

```

![Clone GRPC](https://i.imgur.com/F5MAgGK.png)

## Build

```bash
cd D:\GRPC\grpc\examples\csharp\Helloworld
dotnet build Greeter.sln

```

![Build](https://i.imgur.com/p9eDKj6.png)

### Run a gRPC application

> Server

```bash
cd D:\GRPC\grpc\examples\csharp\Helloworld\GreeterServer>
 dotnet run -f netcoreapp2.1

```

![Server](https://i.imgur.com/snarP0h.png)

> Client

```bash
cd D:\GRPC\grpc\examples\csharp\Helloworld\GreeterClient
dotnet run -f netcoreapp2.1
```

![Client](https://i.imgur.com/xQDQpZC.png)

## 參考

* [C# Quickstart](https://grpc.io/docs/quickstart/csharp.html)
* [gRPC 官方文檔中文版 V1.0](https://doc.oschina.net/grpc?t=60132)
* [https://github.com/grpc/grpc](https://github.com/grpc/grpc)