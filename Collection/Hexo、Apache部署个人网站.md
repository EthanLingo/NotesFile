# Hexo、Apache部署个人网站



# 总述



本人本地端设备：Macos。远程端设备：华为弹性云服务器，系统Ubuntu 18 。



前期准备，包括：

- 配置于本地：

  - 安装Node；

  - 安装Hexo；
  - 部署Hexo；
  - 如果需要免密，则配置rsa；

- 配置于云端：

  - 设置用户名（如果没有的话）；
  - 安装git（如果没有的话）；
  - 开放端口4000；
  - 如果需要免密，且本地端生成了密钥，则配置公钥；
  - 部署服务器。这里用apache；
    - 更换apache之路径（可选项）；



# 安装Node、Git、Hexo

安装Node、Git、Hexo，具体见 [官方文档](https://hexo.io/zh-cn/docs/) 或者 [Hexo系列 | Hexo的基本使用](https://zhuanlan.zhihu.com/p/85037427)，不赘述。如果已经安装过，可以跳过此步骤。



# 建站



安装完Hexo之后，执行下列命令，Hexo将会在指定目录中新建所需要的文件，指定的目录`<folder>`是你的目录文件夹，即为Hexo的工作站。

```shell
$ hexo init <folder>
$ cd <folder>
$ npm install
```



# 服务器端配置Git

```shell
$ sudo adduser git # 回车之后需要设置你的密码
$ su git
$ cd
$ mkdir .ssh && chmod 700 .ssh
$ touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
 # 在配置免密登录之后，继续：
$ cd /srv/git
$ mkdir 你的项目名字.git
$ cd 你的项目名字.git
$ git init --bare
Initialized empty Git repository in /srv/git/你的项目名字.git/
$ chown -R git:git /srv/myfiles.git/ # 因为当前用户是 root，为了让后面 git 专用账户能够操作仓库目录，我们需要把仓库目录授权给 git


```



# 配置免密登录

具体见[[Linux设置免密登录]]

推荐本地用linux系统, 可以很方便处理

- 本地终端输入`ssh-keygen`, 一路回车即可
  创建记录里, 会出现`id_rsa.pub`文件的全路径
- `ssh-copy-id -i ~/.ssh/id_rsa.pub <your user name>@10.10.10.100`
- 下次直接输入`ssh <your user name>@10.10.10.100`可以不用密码

如果是本地是win系统, 则先用某台linux系统整一次免密登陆, 然后执行下面操作

- 本地终端输入`ssh-keygen`, 一路回车即可
  创建记录里, 会出现`id_rsa.pub`文件的全路径
- 把本地的`id_rsa.pub`中的所有内容, 写入到服务器里的`~/.ssh/authorized_keys`文件中, 就可以实现免密登陆



注意，如果配置多对密钥，可以本地终端输入`ssh-keygen`，首次回车之后输入`id_rsa_<你自己填的名字>.pub`，然后剩余一路回车即可。







> 参考：
>
> - https://blog.csdn.net/weixin_42107987/article/details/104683595
> - https://blog.csdn.net/jackandsnow/article/details/105537684
> - [Hexo官方文档](https://hexo.io/zh-cn/docs/)
> - [服务器上的 Git - 配置服务器](https://www.git-scm.com/book/zh/v2/服务器上的-Git-配置服务器)
