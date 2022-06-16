#来源/转载 #资料 #类型/教程

[[C#]]
[[.Net]]


本文介绍如何创建和运行“Hello World!” .NET 应用。

如果不确定什么是 .NET，请从 [.NET 简介](https://docs.microsoft.com/zh-cn/dotnet/core/introduction)开始。

## [](https://docs.microsoft.com/zh-cn/dotnet/core/get-started#create-an-application)创建应用程序

首先，在计算机上下载并安装 [.NET SDK](https://dotnet.microsoft.com/download/dotnet-core)。

然后，打开某一终端，如 PowerShell、命令提示符或 Bash 。 输入以下 `dotnet` 命令，创建并运行 C# 应用程序：

.NET Core CLI复制

```
dotnet new console --output sample1
dotnet run --project sample1
```

可以看到以下输出：

输出复制

```
Hello World!
```

祝贺你！ 你现已创建了一个简单的 .NET 应用程序。