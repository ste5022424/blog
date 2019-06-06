---
title: .Net Core Nlog
date: 2019-01-04 14:26:39
categories:
- .net core
tags:
- .Net Core
- Nlog
---
## .Net Core Nlog

### 1. 用之前的[webapi範例](https://ste5022424.github.io/2018/12/28/Net-Core-CLI/)來實作

### 2. 安裝 Nlog

```
Install-Package NLog.Web.AspNetCore -Version 4.7.0
```
![](https://i.imgur.com/kTy4hbj.png)

### 3. 新增 nlog.config

![](https://i.imgur.com/PvtJXCY.png)


### 4. 設定相關檔案

nlog 設定可以看[官網](https://github.com/nlog/NLog/wiki/Configuration-file)

> nlog.config

```
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      autoReload="true"
      internalLogLevel="info"
      internalLogFile="c:\temp\internal-nlog.txt">

	<!-- enable asp.net core layout renderers -->
	<extensions>
		<add assembly="NLog.Web.AspNetCore" />
	</extensions>
	<!-- the targets to write to -->
	<targets>
		<target xsi:type="File"
			name="file"
			encoding="utf-8"
			layout="${date:universalTime=true:format=yyyy-MM-dd HH\:mm\:ss.fff} ${threadid} ${uppercase:${level}} ${logger} ${message} ${exception:format=tostring}"
			fileName="D:\Log\donetcore.log"
			archiveFileName="D:\Log\donetcore.{#}.log"
			archiveNumbering="Date"
			archiveEvery="Hour"
			archiveDateFormat="yyyyMMdd-HH"
			maxArchiveFiles="720" />

		<target xsi:type="File"
			name="filelinux"
			encoding="utf-8"
			layout="${date:universalTime=true:format=yyyy-MM-dd HH\:mm\:ss.fff} ${threadid} ${uppercase:${level}} ${logger} ${message} ${exception:format=tostring}"
			fileName="Log/donetcore.log"
			archiveFileName="Log/donetcore.{#}.log"
			archiveNumbering="Date"
			archiveEvery="Hour"
			archiveDateFormat="yyyyMMdd-HH"
			maxArchiveFiles="720" />
	</targets>
	<rules>
		<!--Skip non-critical Microsoft logs and so log only own logs-->
		<logger name="Microsoft.*" maxLevel="Info" final="true" />
		<!--<logger name="*" minlevel="Info" writeTo="filelinux" />-->
		<logger name="*" minlevel="Info" writeTo="file" />
	</rules>
</nlog>
```
> program.cs

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using NLog.Web;

namespace donetcore
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // NLog: setup the logger first to catch all errors
            var logger = NLog.Web.NLogBuilder.ConfigureNLog("nlog.config").GetCurrentClassLogger();
            try
            {
                logger.Debug("init main");
                CreateWebHostBuilder(args).Build().Run();
            }
            catch (Exception ex)
            {
                //NLog: catch setup errors
                logger.Error(ex, "Stopped program because of exception");
                throw;
            }
            finally
            {
                // Ensure to flush and stop internal timers/threads before application-exit (Avoid segmentation fault on Linux)
                NLog.LogManager.Shutdown();
            }
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseStartup<Startup>()
                .ConfigureLogging(logging =>
                {
                    logging.ClearProviders();
                    logging.SetMinimumLevel(Microsoft.Extensions.Logging.LogLevel.Trace);
                })
                .UseNLog();  // NLog: setup NLog for Dependency injection
    }
}
```

> appsettings.json

```
{
  "Logging": {
    "LogLevel": {
      "Default": "Trace",
      "Microsoft": "Information"
    }
  },
  "AllowedHosts": "*"
}
```
### 5. 程式寫 log

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Logging;

namespace donetcore.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ValuesController : ControllerBase
    {
        private readonly ILogger<ValuesController> _logger;

        public ValuesController(ILogger<ValuesController> logger)
        {
            _logger = logger;
        }

        // GET api/values
        [HttpGet]
        public ActionResult<IEnumerable<string>> Get()
        {
            this._logger.LogInformation(".net core api 測試");
            return new string[] { "value1", "value2" };
        }
    }
}
```
### 6. Run 專案並檢查 log 是否有寫成功

![](https://i.imgur.com/3puq5ZY.png)


## Run docker in linux

### 1. 更改 nlog.config 設定
>nlog.config
```
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      autoReload="true"
      internalLogLevel="info"
      internalLogFile="c:\temp\internal-nlog.txt">

	<!-- enable asp.net core layout renderers -->
	<extensions>
		<add assembly="NLog.Web.AspNetCore" />
	</extensions>
	<!-- the targets to write to -->
	<targets>
		<!--<target xsi:type="File"
			name="file"
			encoding="utf-8"
			layout="${date:universalTime=true:format=yyyy-MM-dd HH\:mm\:ss.fff} ${threadid} ${uppercase:${level}} ${logger} ${message} ${exception:format=tostring}"
			fileName="D:\Log\donetcore.log"
			archiveFileName="D:\Log\donetcore.{#}.log"
			archiveNumbering="Date"
			archiveEvery="Hour"
			archiveDateFormat="yyyyMMdd-HH"
			maxArchiveFiles="720" />-->

		<target xsi:type="File"
			name="filelinux"
			encoding="utf-8"
			layout="${date:universalTime=true:format=yyyy-MM-dd HH\:mm\:ss.fff} ${threadid} ${uppercase:${level}} ${logger} ${message} ${exception:format=tostring}"
			fileName="Log/donetcore.log"
			archiveFileName="Log/donetcore.{#}.log"
			archiveNumbering="Date"
			archiveEvery="Hour"
			archiveDateFormat="yyyyMMdd-HH"
			maxArchiveFiles="720" />
	</targets>
	<rules>
		<!--Skip non-critical Microsoft logs and so log only own logs-->
		<logger name="Microsoft.*" maxLevel="Info" final="true" />
		<logger name="*" minlevel="Info" writeTo="filelinux" />
		<!--<logger name="*" minlevel="Info" writeTo="file" />-->
	</rules>
</nlog>
```

### 2. build docker image

> linux 建置 .net core 可以參考[這篇](https://ste5022424.github.io/2018/12/28/Net-Core-SKD-For-Linux/)

```
docker  build -t dotnetcoreapi:v2 .
```

### 3. docker run

```
docker run -d -p 8181:80 --name netcorenlog -v /tmp/Log:/app/Log dotnetcoreapi:v2
```
> 如果要進入docker內，可以使用 [exec](https://philipzheng.gitbooks.io/docker_practice/content/container/enter.html) 

```
docker exec -ti netcorenlog bash
```

### 4. 執行

![](https://i.imgur.com/1UmE73P.png)

### 5. 檢查宿主就可以看到 log已經共享出來了

![](https://i.imgur.com/0Xr9hvW.png)

![](https://i.imgur.com/5glSt7g.png)


> [範例檔案](https://github.com/ste5022424/donetcorewebapi)

## 參考
* [Getting started with ASP.NET Core 2](https://github.com/NLog/NLog.Web/wiki/Getting-started-with-ASP.NET-Core-2)
* [nlog設定](https://github.com/nlog/NLog/wiki/Configuration-file)