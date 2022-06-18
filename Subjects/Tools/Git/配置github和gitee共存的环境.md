
#教程 
#解决 
tags: #来源/转载 


[[配置Git]]
[[配置GitHub]]
[[配置Gitee]]


# 配置github和gitee共存的环境

## 1.前言

为什么要配置github和gitee共存的环境？对我来说，首先，github的访问速度比较慢，相应的使用git提交的速度也比较慢，虽然通过修改HOSTS可以对访问速度慢的问题有一定的改善，但是速度终究不能让人满意．而使用gitee则可以很好地避免这个问题．其次，github对我更大的作用是寻找一些大型的开源项目，而gitee因其速度优势可以作为我的个人项目云平台，这样我在windows和Linux的代码就可以很方便地通过gitee进行同步．

## 2. SSH配置

### 2.1清除已有的git配置

如果你之前已经安装了git，并且也配置过了全局的user.name和user.email，那么现在就应该讲这些配置全部清除，清除方法如下：

`
git config --global --unset user.name "YourName"
git config --global --unset user.email "YourEmail"`



### 2.2生成新的SSH Keys

（１）github密钥

进入~/.ssh目录下，输入命令，直接两次回车即可．会在文件夹下生成github_id_rsa和github_id_rsa.pub．

`ssh-keygen -t rsa -C "YourGIthubEmail@mail.com" -f "github_id_rsa"`

之后运行命令cat github_id_rsa.pub输出文件公钥内容，复制公钥内容并添加到github的SSH Keys中保存．

（２）gitee密钥

与github生成密钥的操作类似

`ssh-keygen -t rsa -C "YourGiteeEmail@mail.com" -f "gitee_id_rsa"`

复制公钥gitee_id_rsa.pub公钥的内容，并添加到gitee的SSH Keys中保存．

2.3创建config文件避免ssh冲突

在~/.ssh文件夹下新建config文件，添加以下内容

`# gitee

Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gitee_id_rsa`

`# github

Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/github_id_rsa`

## 3.测试

执行`ssh -T git@github.com`，如果返回successfully则github配置成功．

执行`ssh -T git@gitee.com`，如果返回successfully则gitee配置成功．

## ４.仓库配置

以gitee为例，首先在gitee代码仓库里先新建一个repository．然后在本地新建一个与repository名字相同的文件夹，输入命令git init初始化git，然后进行local配置

`git config --local user.name "giteeUserName"
git config --local user.email "giteeUserEmail"`

然后将本地仓库连接到远程的gitee服务器，可以使用如下命令添加:

`git remote add origin <仓库地址>`

## 补充

Git共有三个级别的config文件，分别是system（系统级别）、global（用户级别）和local（当前仓库）。system配置整个系统只有一个，global配置每个账户只有一个，而local配置和git仓库的数目相同，并且只有在仓库目录才能看到该配置。
可通过如git config --local --list命令来查看仓库配置信息，global和system类似．

END.
————————————————
> 版权声明：本文为CSDN博主「nachr」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/qq_42780025/article/details/107129223