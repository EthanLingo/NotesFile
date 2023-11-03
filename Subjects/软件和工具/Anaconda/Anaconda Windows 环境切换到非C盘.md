---
title: Anaconda Windows 环境切换到非C盘
authors: Ethan Lin
year: 2023-11-03
tags:
  - 类型/笔记
  - 日期/2023-11-03
  - 来源/转载
---



# 来源

> 







原文：

> [anaconda的envs路径跑到c盘了，修改为D盘](https://zhuanlan.zhihu.com/p/649072923)



问题描述：



以往新建anaconda环境，路径是在anaconda安装目录下的envs中（`D:\anaconda3\envs`），然而，这次创建的却是在 `C:\Users\xxx.conda\envs\` 中。

寻找原因：

z在开始菜单寻找 Anaconda Prompt ，打开之后：



**1. 查看conda 信息**

```text
conda info 或
conda config --show
```

确实默认在C盘



解决办法：



`C:\Users\用户名`下有一个 `.condarc` 文件，将其打开，在其末尾添加下面内容：

**记事本打开并添加，注意将`D://Anaconda//envs`换成自己要保存的位置，建议放在anaconda安装文件夹下的`envs`文件夹中**

```text
envs_dirs:
  - D://Users//【你的用户名】//anaconda3//envs
```

保存，再次试一下创建环境，环境位置是我们指定的位置了。

如果还是不行，看下面一条。

1. 如果环境位置没有切换，查看一下目标路径的文件夹的权限。
   我这里是全勾上了的

需要给envs（`D://Users//【你的用户名】//anaconda3//envs`）这个文件加一个执行权限：

右击envs----选择属性，勾选所有的允许项。



此时就添加好了权限，创建的环境的路径也已经添加，重新再创建环境，发现已经不在C盘，而在我们自定义的anaconda的安装目录下了。



