---
title: .Net Core SKD For Linux
date: 2018-12-28 12:02:10
categories:
- .net core
tags:
- .net core
- Linux build
---
## .Net Core SKD For Linux

```
cd tmp/
mkdir netcoresdk2.1
cd netcoresdk2.1

wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb


sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1

```

## 參考
* [https://dotnet.microsoft.com/download/dotnet-core/2.1](https://dotnet.microsoft.com/download/dotnet-core/2.1)
* [Install .NET Core 2.1 SDK on Linux Ubuntu 16.04 x64](https://dotnet.microsoft.com/download/linux-package-manager/ubuntu16-04/sdk-2.1.502)
