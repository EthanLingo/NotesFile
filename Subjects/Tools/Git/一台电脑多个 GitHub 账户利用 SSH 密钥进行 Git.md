---
title: 一台电脑多个 GitHub 账户利用 SSH 密钥进行 Git
authors: Ethan Lin
year: 2024-05-25
tags:
  - 类型/笔记
  - 日期/2024-05-25
  - 来源/转载
  - 内容/Git
aliases:
  - 一台电脑多个 GitHub 账户利用 SSH 密钥进行 Git
---



# 一台电脑多个 GitHub 账户利用 SSH 密钥进行 Git

# 来源

> [CSDN - 一台电脑多个GitHub账户利用SSH密钥进行Git](https://blog.csdn.net/qq_49327995/article/details/138089838#:~:text=如果你有两个%20GitHub%20账户，并且你想要在同一台计算机上使用%20SSH%20访问这两个账户，你需要为每个账户生成一个%20SSH,密钥对，并且在你的%20SSH%20配置文件中为每个账户设置一个别名，这是因为%20SSH%20配置文件中的别名用于指定对应的私钥，然后在%20Git%20命令中使用别名来指定你想要使用的账户%E3%80%82)



一、一台电脑使用两个GitHub账户(两个SSH)进行git
如果你有两个 GitHub 账户，并且你想要在同一台计算机上使用 SSH 访问这两个账户，你需要为每个账户生成一个 SSH 密钥对，并且在你的 SSH 配置文件中为每个账户设置一个别名，这是因为 SSH 配置文件中的别名用于指定对应的私钥，然后在 Git 命令中使用别名来指定你想要使用的账户。

生成密钥
在 Windows 上，你可以使用 Git Bash 来生成多个 SSH 密钥。以下是具体步骤：

打开 Git Bash。
输入以下命令来生成第一个 SSH 密钥：
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
1
请将 "your_email@example.com" 替换为你的电子邮件地址。当提示你输入文件路径时，输入一个新的文件路径，例如 ~/.ssh/id_rsa_account1，如下图红色框部分所示（为了方便 id_rsa_account1 可以写成 github 的用户名，最后生成的私钥和公钥会以它命名）。



输入完毕点击回车后，输入访问密码（图方便就直接回车不输，要保险就输个自己的密码，可能下次git的时候会需要输入这个密码）

将每个账户的公钥(文件后缀为.pub)添加到对应的 GitHub 账户。你可以在 GitHub 的设置页面中添加公钥。

重复上述步骤来生成更多的 SSH 密钥。每次生成新的密钥时，都要使用一个新的文件路径，例如 ~/.ssh/id_rsa_account2。

创建配置文件（单个SSH可不用）
创建一个 SSH 配置文件：
touch ~/.ssh/config
1
打开 SSH 配置文件，在你的 SSH 配置文件（通常位于 ~/.ssh/config）中为每个账户设置一个别名：
# 一台电脑多个GitHub账户利用SSH密钥进行Git
Host github.com-account1
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account1

# Account 2
Host github.com-account2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account2
1
2
3
4
5
6
7
8
9
10
11
在这个配置文件中，github.com-account1 和 github.com-account2 是别名（图方便就GitHub张），~/.ssh/id_rsa_account1 和 ~/.ssh/id_rsa_account2 是你的私钥的路径。
那么，当你想要克隆账户 1 的仓库时，你需要使用以下命令：

git clone git@github.com-account1:username/repo.git
1
在这个命令中，username 是你的 GitHub 用户名，repo 是你的 GitHub 仓库的名字。github.com-account1 是你在 SSH 配置文件中为账户 1 设置的别名。

同样，当你想要克隆账户 2 的仓库时，你需要使用以下命令：

git clone git@github.com-account2:username/repo.git
1
在这个命令中，github.com-account2 是你在 SSH 配置文件中为账户 2 设置的别名。

二、只需要一个GitHub账户(一个SSH密钥)
如果你只有一个 GitHub 账户，并且你的计算机上只有一个 SSH 密钥，那么你不需要在 SSH 配置文件中设置别名。你可以直接使用 git@github.com:username/repo.git 格式的 URL 来克隆你的仓库。

如果你的 SSH 配置文件中有别名，那么你可以删除这些别名，或者你可以将 HostName 设置为 github.com，并将 IdentityFile 设置为你的 SSH 私钥的路径。例如：

# Account 1
# Host anqingsan
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/anqingsan

# Account 2 以后可以绑定我的大号
1
2
3
4
5
6
7
8
在这个配置中，~/.ssh/id_rsa 是你的 SSH 私钥的路径。

然后，你可以使用以下命令来克隆你的仓库：

git clone git@github.com:username/repo.git
1
在这个命令中，username 是你的 GitHub 用户名，repo 是你的 GitHub 仓库的名字。

三、Git
在克隆仓库时，直接使用ssh进行克隆，而不要使用http，这样后期在 vscode 中就可以跟往常一样直接提交推送到该仓库。

你可以使用以下命令来克隆你的仓库：

git clone git@github.com:username/repo.git
1
在这个命令中，username 是你的 GitHub 用户名，repo 是你的 GitHub 仓库的名字。

要使用 SSH 推送到 GitHub，你需要确保你已经设置了 SSH 密钥，并且已经将你的公钥添加到了你的 GitHub 账户。然后，你需要确保你的远程仓库 URL 是 SSH 格式的，而不是 HTTPS 格式的。

你可以使用 git remote -v 命令查看你的远程仓库 URL。如果它是 HTTPS 格式的（例如，https://github.com/username/repo.git），你需要将其更改为 SSH 格式的（例如，git@github.com:username/repo.git）。

你可以使用 git remote set-url 命令更改远程仓库 URL。例如：

git remote set-url origin git@github.com:username/repo.git
1
参考链接
git如何使用ssh推送 • Worktile社区

GitHub仓库配置SSH keys步骤流程图解 - 知乎 (zhihu.com)

关于git使用ssh key认证github和gitee远程推送 - g青苹果 - 博客园 (cnblogs.com)
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/qq_49327995/article/details/138089838
