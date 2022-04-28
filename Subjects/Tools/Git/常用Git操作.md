# 常用Git操作


# 常用Git操作

#### 初始化Git

首先，你需要执行下面两条命令，作为 git 的基础配置，作用是告诉 git 你是谁，你输入的信息将出现在你创建的提交中。

```
# 常用Git操作

git config --global user.name yourname  # "你的名字或昵称"
git config --global user.email youremail@xxx.com # "你的邮箱"
```

#### 创建版本库

本段内容大部分引用自廖雪峰的官方网站 创建版本库

什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录YourProjName（名字任意）：

```
cd /e/
mkdir YourProjName
cd YourProjName
```

如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

第二步，通过git init命令把这个目录变成Git可以管理的仓库：

```
git init
# Initialized empty Git repository in E:/YourProjName/.git/
```

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

#### 关联

本段内容大部分引用自码云平台帮助文档V1.2 Git 常用命令与名词解释

把一个本地仓库与一个云端Gitee仓库关联。

项目地址形式为:https://gitee.com/YourGiteeName/YourProjName.git 或者 git@gitee.com:YourGiteeName/YourProjName.git

```
git remote add origin https://gitee.com/YourGiteeName/YourProjName.git
```

如果只是需要使用vscode管理，到这里就可以直接跳到本文最后一段【在VSCode实现代码管理】去看了

下面接着讲git命令行其他操作

其中origin代表的是你远程的仓库，习惯如此命名，可以通过命令 git remote -v 查看

```
git remote -v
# origin  https://gitee.com/YourGiteeName/YourProjName.git (fetch)
# origin  https://gitee.com/YourGiteeName/YourProjName.git (push)
```

如果你想克隆一个项目，只需要执行：

```
git clone <项目地址>
```

#### 同步（拉取）

同步，也可以称之为拉取，在Git中是非常频繁的操作，和SVN不同，Git的所有仓库之间是平等的，所以，为了保证代码一致性，尽可能的在每次操作前进行一次同步操作，具体的为在工作目录下执行如下命令:

```
git pull origin master
```

master是分支名，如果你本地是其他分支，请换成其他分支的名字，另，因为远程仓库与你本地仓库可能存在冲突，故当存在冲突时，请参考进阶篇的如何处理冲突

查看文件夹，会发现 Gitee仓库上 README.md 文件被下载回来了。

#### 提交

git作为支持分布式版本管理的工具，它管理的库（repository）分为本地库、远程库。

这里我们把 add(暂存)、提交(commit)、推送(push)，放到一起说，因为每次上传代码都需要执行这三步（关于冲突处理、分支合并等以后用到了再研究，本文只说基础部分）。

```
git add     # 加入到暂存区
git commit  # 提交到本地库
git push    # 发送给远程库
```

首先，我们打开 README.md ，在里面稍稍加上几个字，保存。这样文件就做了修改。

再来查看git状态

```
git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#         modified:   README.md
#
# no changes added to commit (use "git add" and/or "git commit -a")
```

会提示你modified: README.md ，意思是这个文件被修改了。no changes added to commit 是说目前暂时没有文件放到暂存区。

所以我们将文件加入暂存区。

```
git add -A
```

-A表示将所有文件的修改，文件的删除，文件的新建，都添加到暂存区。

然后提交到本地库，并附加注释。

```
git commit -m "第一次提交"
# [master 1cc3dd5] 第一次提交
#  1 file changed, 1 insertion(+), 1 deletion(-)
```

-m后面的是本次提交的说明，通常可以备注你改了什么，便于以后翻看历史记录时，能直观知道这是哪个版本，这个版本改了些什么东西。

最后推送到远程库，也就是Gitee上的项目里。


```
git push origin master
# Counting objects: 3, done.
# Writing objects: 100% (3/3), 297 bytes | 297.00 KiB/s, done.
# Total 3 (delta 0), reused 0 (delta 0)
# To https://gitee.comYourGiteeName/YourProjName.git
#    5464c11..1cc3dd5  master -> master
```





------------------------------------------------
版权声明：本文为CSDN博主「watfe」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/watfe/article/details/79761741

