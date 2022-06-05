#来源/转载
#资料 

[[Python]]
[[配置Python]]



![img](python-environment-mac-20210320114006317.jpg)

# Mac下终端pip与pip3配置（软链接）

[2020-02-05 由 ](https://www.omegaxyz.com/2020/02/05/mac-pip-config/)[xyjisaw](https://www.omegaxyz.com/author/xuyi/)

本文共1483个字，预计阅读时间需要5分钟。

## 文章目录

- [缘起](https://www.omegaxyz.com/2020/02/05/mac-pip-config/#缘起)
- Mac两个bin目录
  - [相同点](https://www.omegaxyz.com/2020/02/05/mac-pip-config/#相同点)
  - [不同点](https://www.omegaxyz.com/2020/02/05/mac-pip-config/#不同点)
- [Mac的终端的用户可配置文件](https://www.omegaxyz.com/2020/02/05/mac-pip-config/#mac的终端的用户可配置文件)
- [查看位置命令](https://www.omegaxyz.com/2020/02/05/mac-pip-config/#查看位置命令)
- [实例](https://www.omegaxyz.com/2020/02/05/mac-pip-config/#实例)

## **缘起**

今日Mac上的Python环境绝对是个asshole。
\1. 系统自带一个Python2.7
\2. 我官网下载一个3.6
\3. homebrew悄悄下了个3.x
\4. anaconda自带了一个3.x
\5. 前天更新了一下Xcode命令行工具，竟然给我偷偷下了个3.7，顺带把某一软连接变量写入系统盘，安装的包放到数据盘
~~**MacOS Catalina文件系统属实拉胯，绝对没有Windows好使。**~~

为了使得终端运行pip命令时能够正确指向所需的Python，需要重新配置软链接。

------

## **Mac两个bin目录**

### **相同点**

/usr/bin和/usr/local/bin都是用来存储终端命令二进制文件或者命令的软链接
这两个bin目录都是已经包含在环境变量里的目录，程序放在里面或者链接到里面命令就可以在终端里直接执行。

### **不同点**

Mac的/usr/bin目录是不允许增删文件的，/usr/local/bin增删文件来实现在终端里直接运行，只需要有管理员权限。

**注意搜索目录时最前面的”/”不能缺少**

------

## **Mac的终端的用户可配置文件**

可配置文件根据终端类型分为两种，这些文件都是隐藏的，语法结构相同，可以用来配置环境变量等，需要“Command+Shift+.”才能显示
**bash终端：**/Users/你的用户名/.bash_profile

**zsh终端：**
/Users/你的用户名/.zsh_profile
/Users/你的用户名/.zshrc

------

## **查看位置命令**

**which pip和which pip3:** 查看python 的pip 包管理工具的启动路径（软链接的位置），一般都在上述提到的两个bin目录中间

**pip –version和pip3 –version:** 用来展示命令的真实地址存储位置

------

## **实例**

下面以pip3为例，在zsh中的针对pip3具体操作，**同理要将终端中2.7版本的pip改为自己下载的pip版本，直接将下述所有的pip3改为pip**
所有命令需根据自己的Python版本和真实位置而修改

**①首先需要保证/usr/local/bin的环境变量位置在/usr/bin前面，这样才能先读/usr/local/bin的数据，因为前者的数据可以更改**

zsh终端下执行：



ZSH

| 1    | echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc |
| ---- | ----------------------------------------------------- |
|      |                                                       |

注意此步可以先不操作，如果出现了permission denied或者command not find问题说明你碰到了/usr/bin，到时候再执行第一步

**②找到pip3的真实位置**

一般来说，你下载的python 3.x的pip在
/Library/Frameworks/Python.framework/Versions/3.x/lib/python3.x/site-packages/pip (python 3.x)

**③删除已经存在的冗余数据**



ZSH

| 1    | rm -rf /usr/local/bin/pip3 |
| ---- | -------------------------- |
|      |                            |

**④在/usr/local/bin/中重新创建pip3的软链接至上述pip3的真实位置**



ZSH

| 1    | ln -s /Library/Frameworks/Python.framework/Versions/3.x/bin/pip /usr/local/bin/pip3 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

此时在命令行输入pip3会自动指向你的Python版本的真实位置

**⑤验证**



ZSH

| 1    | pip3 --version |
| ---- | -------------- |
|      |                |

我的终端显示：
pip 19.0.3 from /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages/pip (python 3.6)



ZSH

| 1    | which pip3 |
| ---- | ---------- |
|      |            |

我的终端显示：
/usr/local/bin/pip3

 