# Julia卸载


部署Jilia在linux





Linux 下 卸载 Julia 旧版本 & 更新到 1.5

Mr_Vague 2020-10-08 19:35:43   256   收藏 1
分类专栏： Julia 文章标签： linux julia
版权
julia版本迭代很快，卸载旧版本，更新到最新版本是很方便的。

卸载 julia 其实就是删除安装目录和包目录
a. 通常在安装的时候是用软连接把安装路径的执行文件与系统执行文件目录关联起来，使用以下命令找到真正的安装目录，并删除

[root]# which julia
/usr/local/bin/julia

[root]# ll /usr/local/bin/julia
lrwxrwxrwx 1 root root 27 Oct  8 17:15 /usr/local/bin/julia -> /data/julia-1.3/bin/julia

[root]# rm -f /data/julia-1.3/bin/julia

b. 包目录一般为 ~/.julia，直接使用 rm 删除即可

至此完全移除了旧版 julia。

安装新的 julia
a. 到 https://julialang.org/downloads/ 官方下载网址下载二进制文件（tar.gz压缩包）

b. 解压 tar -xzvf julia-1.5.2-linux-x86_64.tar.gz

c. 创建连接 ln -sb /data/julia-1.5.2/bin/julia /usr/local/bin/julia

安装结束。

ps.
julia 1.5+ 版本默认使用官方服务器 pkg.julialang.org，无需额外设置，安装 pkg 时会根据 IP 地域自动导流到国内区域服务器，安装官方 pkg 更方便和迅速了。详细见【Julia中文论坛】Julia PkgServer 镜像服务及镜像站索引
------------------------------------------------
版权声明：本文为CSDN博主「Mr_Vague」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/m0_37952030/article/details/108966452