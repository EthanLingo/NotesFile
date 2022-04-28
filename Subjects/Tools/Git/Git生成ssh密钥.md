# 在VSCode中使用码云进行代码管理


#解决 
#来源/转载 
#教程 

[[配置Git]]
[[配置VS Code]]
[[配置Gitee]]






# 在VSCode中使用码云进行代码管理

[TOC]

## 前言

### 本教程核心内容

本文主要是整合了网上教程，

从Git安装开始，配置关联本地仓库到码云，最终用上VScode这个流程。

非常基础和简单，照着操作就行了。

### 起因

平时常写python脚本，原先用Sublime，现在用VScode，发现编辑器左侧有代码管理这个按钮，于是开始找怎么设置VSCode能和码云连在一起。

踩了一些坑，理顺了思路，才发现一点关系都没有。

正确的思路是：安装Git；关联码云；打开VSCode。

是的你没看错，前两步设置好了，打开VSCode直接就能用上码云的代码管理了。

### Git和Github的关系：

Git是一个分布式的版本控制系统，只是软件，需要你下载装到电脑上，实现git功能。

Github、BitBucket、Gitee基于git的项目托管平台，说白了是云服务器或云盘，存储分享你的代码，查看追更别人的代码。 理解了这些，大概就能明白有一堆程序员所在的Github为什么被戏称是全球最大的同性交友平台这个梗了。Github、BitBucket是国外的，连接速度因人而异；另外Github收费用户才能创建私有项目（2020-09-19备注：卖给微软后现在已经可以创建私有项目了）。

### 准备内容

注册码云(Gitee)，创建一个项目，得到项目url：https://gitee.com/YourGiteeName/projectname
下载git安装， 全都按下一步就行了。
下载VSCode安装。

### 如何生成ssh公钥

本段内容大部分引用自码云平台帮助文档

打开Git Bash，安装完git就有这个了。

你可以按如下命令来生成 sshkey：

```
ssh-keygen -t rsa -C "youremail@xxx.com"
# Generating public/private rsa key pair...
# 三次回车即可生成 ssh key
```

查看你的 public key

```
cat ~/.ssh/id_rsa.pub
# ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6eNtGpNGwstc....
```


## 在Github上添加ssh密钥
3.在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥。

打开[https://github.com/](https://github.com/settings/ssh) ，在settings里面点击SSH keys。自行输入title，复制id_rsa.pub里面的内容到key。

就设置成功了。

> [来源网页](http://t.zoukankan.com/long5683-p-10629235.html)


## 在Gitee上添加ssh密钥

打开码云SSH公钥管理页面 https://gitee.com/profile/sshkeys

填写标题：

```
yourname's SSH key
```

公钥：

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6eNtGpNGwstc...
```

添加后，回到Git Bash中输入

```
ssh -T git@gitee.com
```

如果有弹出询问(yes/no)，输入

```
yes
```

若返回

```
# Welcome to Gitee.com, YourGiteeName!
```

则证明添加成功。

### Git Gui

上面说的都是代码上的操作，实际上安装完Git之后，也有GUI界面可以直接使用。

打开 Git Gui，选择Open Existing Repository，找到刚刚创建的本地库打开。

界面比简单，只有几个按钮：

Rescan检查仓库中文件状态； Stage Changed就是add暂存； Commit、Push就是提交、推送。

注：如果发现中文乱码，我们修改一下配置文件编码，改为utf-8就好了

```
git config --global gui.encoding utf-8
```



------------------------------------------------
版权声明：本文为CSDN博主「watfe」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/watfe/article/details/79761741