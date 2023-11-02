---
title: Linux设置免密登录
authors: Ethan Lin
year:
tags:
  - 内容/办公 
  - 内容/Linux/操作 
---


# Linux设置免密登录





Linux系统远程端与其它终端设备之间，通过生成密钥对方式实现免密登录。
操作如下：

1. 本地终端输入指令：
	指令：`ssh-keygen -t rsa -C '《你的备注》'  -f  ~/.ssh/id_rsa_x
	注解：`-t rsa`表示密钥对类型；`-C '《你的备注》'`表示备注；` -f  ~/.ssh/id_rsa_x`表示生成密钥对之名称与所在路径；
2. 部署公钥至远程端：
   指令 `ssh-copy-id -i ~/.ssh/id_rsa.pub <your user name>@10.10.10.100`
	下次直接输入`ssh <your user name>@10.10.10.100`可以不用密码。

注意，如果配置多对密钥，可以本地终端输入`ssh-keygen`，首次回车之后输入`id_rsa_<你自己填的名字>.pub`，然后剩余一路回车即可。



### 删除密钥：

用OpenSSH的人都知ssh会把你每个你访问过计算机的公钥(public key)都记录在`~/.ssh/known_hosts`。

当下次访问相同计算机时，OpenSSH会核对公钥。如果公钥不同，OpenSSH会发出警告，

如果我们重新安装系统，其公钥信息还在，连接会出现如下警告。解决方法如下：

方法一：  
`rm -rf ~/.ssh/known_hosts`

优点：干净利索

缺点：把其他正确的公钥信息也删除，下次链接要全部重新经过认证

  
方法二：

`vi ~/.ssh/known_hosts`

删除对应ip的相关rsa信息（本例可知删除53行信息即可）

优点：其他正确的公钥信息保留

缺点：还要vi，还要找到对应信息，稍微优点繁琐

  
方法三：

清除旧的公钥信息

`ssh-keygen -R 192.168.0.100`

优点：快、稳、狠

缺点：没有缺点
`

