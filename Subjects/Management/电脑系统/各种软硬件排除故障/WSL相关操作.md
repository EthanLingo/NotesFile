

#解决 
#资料 
#来源/转载 


[[WSL]]

[[工具常用操作]]




### 重启WSL

```powershell
# PowerShell (admin)
Restart-Service LxssManager

# CMD (admin)
net stop LxssManager
net start LxssManager
```



### 配置GUI并远程





#### WSL2使用xrdp实现图形桌面

Dexter Lien
Dexter Lien

郑州大学 软件工程硕士

##### 前言

话说自从有了WSL以后就很少再用过虚拟机了,不过有些不得不用图形化环境启动的程序在WSL里面一直没法实现有点缺憾,前段时间折腾树莓派的时候用了下xrdp+xfce4实现远程图形化桌面访问挺方便的,寻思着WSL里面应该也可以的,搞了一下还真成功了,分享一下过程.

##### 安装包

老规矩,先更新,再安装,一共就俩包xfce4和xrdp,都很轻量,分分钟装好

$ sudo apt update
$ sudo apt install -y xfce4 xrdp

ps:安装xfce4过程中会出现选择显示管理DM选择的提示,建议用lightdm

如果错过了安装过程中出现的这个向导,那么可以在安装完成后执行下面的命令重新设置DM

$ sudo dpkg-reconfigure lightdm

##### 修改xrdp默认端口

由于xrdp安装好后默认配置使用的是和Windows远程桌面相同的3389 端口,为了防止和Windows系统远程桌面冲突,建议修改成其他的端口

$ sudo vim /etc/xrdp/xrdp.ini

修改下面这一行,将默认的3389改成其他端口即可

port=3390

##### 为当前用户指定登录session类型

注意这一步很重要,如果不设置的话会导致后面远程桌面连接上闪退

$ vim ~/.xsession

写入下面内容(就一行)

xfce4-session

##### 启动xrdp

由于WSL2里面不能用systemd,所以需要手动启动

$ sudo /etc/init.d/xrdp start

##### 远程访问

在Windows系统中运行mstsc命令打开远程桌面连接,地址输入localhost:3390

注意这里的端口号应当与上面修改配置中一致

输入WSL2中使用的账号密码,噔噔蹬蹬~完美!

##### 结束语

没有使用任何第三方的工具就完美实现了WSL2的图形化界面访问,而且流畅度还相当不错,看来以后可以彻底告别虚拟机啦~
编辑于 2020-07-30