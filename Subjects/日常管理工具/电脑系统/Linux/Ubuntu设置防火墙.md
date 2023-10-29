

tags: #来源/转载 
#教程 
#解决 


[[Ubuntu]]
[[Linux]]
[[软硬件操作]]

# Ubuntu设置防火墙







注意：不管是在Linux服务器还是在Ubuntu服务器中，当防火墙开启以后，会开放一些常用的端口，这时常常直接到自己Windows上telnet已经开放的端口，通常会忽略开放的这些端口在服务器中是否有程序进行监听，如果没有程序进行监听，telnet开放的这些端口时往往是不通的。

1、Ubuntu查看防火墙的状态

在Ubuntu系统进行安装的时候默认安装了ufw防火墙

查看防火墙的状态

命令：

       sudo ufw status



系统提示： “Status: inactive”状态：不活跃

上面提示表示没有开启防火墙，并不是没有安装防火墙

如果没有安装可以使用命令安装

命令：

       sudo sudo apt-get install ufw

2、Ubuntu开启防火墙

开启防火墙，

命令：

       sudo ufw enable          //开启防火墙



注意：Command may disrupt existing ssh connections. Proceed with operation (y|n)?

表示：命令可能会中断现有的ssh连接。继续操作(y|n)?

因为是在远程的Xshell进行连接开启防火墙的，有的系统是没有将SSH的22端口设置为public的，所以会有这样的提示，这里分为两种情况，如果开启防火墙时在防火墙之中检测到22端口已添加为防火墙的开放端口，那么输入y继续操作以后，当前Xshell会自动断开连接；相反，如果开启防火墙时在防火墙之中没有检测到22端口，那么输入y继续操作以后22端口将会不再支持其他连接，只支持当前已有的这个连接，保持当前连接的原因是可以通过该连接开放22端口。

这里之前没有设置过，直接输入y继续执行



系统提示：“防火墙是活动的，并在系统启动时启用”

表示防火墙已经开启

查看防火墙的状态

命令：

       sudo ufw status           //查看防火墙的状态



可以看到系统只对外开放了80端口

在这里通常会有些错觉，22端口没有开放，但是依然是连接状态，这是系统做的人性化优化，便于远程管理服务器，虽然22端口没有开放，但是用户通过当前的连接开启防火墙后，该连接依然处于连接状态，只要不关闭当前连接还是可以在当前连接中正产操作的。如果是重新开启一个连接是连不上的



在windows上进行telnet也是不通的



所以在远程管理服务器时，如果开启了防火墙先查看SSH的22端口有没有开放，如果没有开放，第一时间开放22端口（如果为了安全也可以指定ip开放22端口）

3、Ubuntu添加开放SSH端口

命令：

       sudo ufw allow 22        //开放22端口



开启完成，需要重启防火墙生效

命令：

       sudo ufw reload           //重启ufw防火墙



重启成功

再查看防火墙的状态

命令：

       sudo ufw status           //查看防火墙的状态



22端口已经开放

查看22端口的监听状态

命令：

       sudo netstat -tunlp | grep 22            //查看22端口信息



22端口属于监听状态，在Windows下能够telnet通

命令：

       telnet 192.168.121.135 22





此时其他的Xshell窗口也可也连接



4、Ubuntu防火墙常用命令

4.1、查看ufw防火墙的状态

命令：

       sudo ufw status           //查看防火墙的状态，如果防火墙是关闭状态则显示“Status: inactive”不活动，如果防火墙开启状态则显示当前设置的规则。

关闭状态下查看防火墙状态

命令：

       sudo ufw status



开启状态下该命令查看防火墙的规则

命令：

       sudo ufw status



4.2、启用ufw防火墙

命令：

       sudo ufw enable          //开启防火墙



4.3、重启ufw防火墙

命令：

sudo ufw reload           //重启防火墙，添加规则以后需要使用该命令进行重启防火墙



4.4、关闭ufw防火墙

命令：

       sudo ufw disable          //关闭防火墙



4.5、设置外来访问默认权限

命令：

       sudo ufw default deny        //拒接所有外来访问，本机能正常访问外部



这条命令开放的端口是没有可见的变化的

4.6、端口的开放与关闭

4.6.1、开放普通端口

命令：

       sudo ufw allow 21               //开放21端口



查看端口规则

命令：

       sudo ufw status



21端口开放成功 

开放成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.2、关闭普通端口

命令：

       sudo ufw delete allow 21           //关闭21端口



查看端口规则

命令：

       sudo ufw status



21端口关闭成功 

成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.3、开放规定协议的端口

命令：

       sudo ufw allow 8001/tcp            //指定开放8001的tcp协议



查看端口规则

命令：

       sudo ufw status



端口开放成功     

开放成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.4、关闭指定协议端口

命令：

       命令：
    
       sudo ufw delete allow 8001/tcp        //关闭21端口



查看端口规则

命令：

       sudo ufw status



8001端口关闭成功    

成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.5、开放限定ip地址端口

4.6.5.1、开放指定ip所有操作

命令：

       sudo ufw allow from 192.168.121.1  

// 指定ip为192.168.121.1的计算机操作所有端口



查看端口规则

命令：

       sudo ufw status



开放成功      

成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.5.2、关闭指定ip所有操作

命令：

sudo ufw delete allow from 192.168.121.1

// 关闭指定ip为192.168.121.1的计算机操作所有端口



查看端口规则

命令：

       sudo ufw status



关闭成功      

成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.5.3、开放指定ip对应端口操作

命令：

       sudo ufw allow from 192.168.121.2 to any port 3306

// 开放指定ip为192.168.121.2的计算机访问本机的3306端口



查看端口规则

命令：

       sudo ufw status



开放成功      

成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效



4.6.5.4、关闭指定ip对应端口操作

命令：

       sudo ufw delete allow from 192.168.121.2 to any port 3306

// 关闭指定ip为192.168.121.2的计算机对本机的3306端口的操作



查看端口规则

命令：

       sudo ufw status



关闭成功      

成功以后需要重启生效

命令：

       sudo ufw reload           //重启防火墙，是配置生效




------------------------------------------------
版权声明：本文为CSDN博主「Aaron_Run」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_36938617/article/details/95234909