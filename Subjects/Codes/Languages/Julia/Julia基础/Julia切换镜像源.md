# Julia切换镜像源


tags: #日期/2022-10-10 #类型/笔记 #内容/编程语言/Julia 

[Julia切换镜像源相关教程](https://mirror.tuna.tsinghua.edu.cn/help/julia/)

## Julia 镜像使用帮助

TUNA 目前提供了 Julia 的官方包注册表 [General](https://github.com/JuliaRegistries/General) 镜像来加速 Julia 包的安装。 TUNA 同时也提供了 Julia 二进制程序的镜像，关于其使用请参考 [Julia Releases](https://mirrors.tuna.tsinghua.edu.cn/help/julia-releases/).

注：本镜像的使用需要 Julia `v1.4.0` 或更新的版本。

## 使用方式

只需要设置环境变量 `JULIA_PKG_SERVER` 即可切换镜像。若成功切换镜像，则能通过 `versioninfo()` 查询到相关信息，例如：

```
julia> versioninfo()
Julia Version 1.4.1
Commit 381693d3df* (2020-04-14 17:20 UTC)
Platform Info:
  OS: Linux (x86_64-pc-linux-gnu)
  CPU: Intel(R) Core(TM) i7-6800K CPU @ 3.40GHz
  WORD_SIZE: 64
  LIBM: libopenlibm
  LLVM: libLLVM-8.0.1 (ORCJIT, broadwell)
Environment:
  JULIA_PKG_SERVER = https://mirrors.tuna.tsinghua.edu.cn/julia
```

若不设置该环境变量则默认使用官方服务器 `pkg.julialang.org` 作为上游。

### 临时使用

不同系统和命令行下设置环境变量的方式各不相同，在命令行下可以通过以下方式来临时修改环境变量

-   Linux Bash: `export JULIA_PKG_SERVER=https://mirrors.tuna.tsinghua.edu.cn/julia`
-   Windows Powershell: `$env:JULIA_PKG_SERVER = 'https://mirrors.tuna.tsinghua.edu.cn/julia'`

也可以利用 JuliaCN 社区维护的中文本地化工具包 [JuliaZH](https://github.com/JuliaCN/JuliaZH.jl) 来进行切换：

```
using JuliaZH # 在 using 时会自动切换到国内的镜像站
JuliaZH.set_mirror("BFSU") # 也可以选择手动切换到 BFSU 镜像
JuliaZH.mirrors # 查询记录的上游信息
```

### 永久使用

不同系统和命令行下永久设定环境变量的方式也不相同，例如 Linux Bash 下可以通过修改 `~/.bashrc` 文件实现该目的：

```
# ~/.bashrc
export JULIA_PKG_SERVER=https://mirrors.tuna.tsinghua.edu.cn/julia
```

此外，这里再提供一种针对 Julia 的全平台通用的方式：`$JULIA_DEPOT_PATH/config/startup.jl` ( 默认为 `~/.julia/config/startup.jl` ) 文件定义了每次启动 Julia 时都会执行的命令，编辑该文件，添加以下内容即可：

```
# ~/.julia/config/startup.jl
ENV["JULIA_PKG_SERVER"] = "https://mirrors.tuna.tsinghua.edu.cn/julia"
```

也可以选择使用 `JuliaZH` 来一键修改/创建 `startup.jl` 文件：

```
# 以 BFSU 镜像站为例
julia> JuliaZH.generate_startup("default")
┌ Info: 添加 PkgServer
│   服务器地址 = "https://pkg.julialang.org"
└   配置文件 = "/root/.julia/config"

julia> JuliaZH.generate_startup("BFSU")
┌ Info: 更新 PkgServer
│   原服务器地址 = "https://pkg.julialang.org"
│   新服务器地址 = "https://mirrors.bfsu.edu.cn/julia"
└   配置文件 = "/root/.julia/config"
```

若要临时禁止，可以通过 `julia --startup-file=no` 来取消执行 `startup.jl` 文件。