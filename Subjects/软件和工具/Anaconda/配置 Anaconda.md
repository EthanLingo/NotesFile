---
title:
  - 配置Anaconda
authors: Ethan Lin
year: 2024-03-19
tags:
  - 类型/笔记
  - 日期/2024-03-19
  - 来源/转载
---


[[Python]]
[[配置 Anaconda]]

# 配置 Anaconda


## 部署Anaconda

### 删除Anaconda于Mac系统

2019年1月15日更新

-   第一步，删除Anaconda的配置，命令如下：

    > $: conda install anaconda-clean
    >
    > $: anaconda-clean

    运行完第二个命令，命令行会提示是否删除，直接选**y**就可以，并且会在你的根目录下会生成一个备份，截图如下：  

    ![](//upload-images.jianshu.io/upload_images/1791824-0f24eedadafa22b5.png?imageMogr2/auto-orient/strip|imageView2/2/w/491)

    屏幕快照

备份也可以删除掉，命令如下：

> rm -r /Users/zc/.anaconda\_backup/**2019-**\*

**注：命令中黑色文字需要更改为自己的备份名字**



-   第二步，删除Anaconda的文件夹，命令如下：

    > $: rm -rf ~/Apps/anaconda3

    **注：文件夹可能在其他位置，请确认**

    

-   第三步，删除 _~/.bash\_profile_中anaconda的环境变量，可以使用_vim_打开删除，删除内容如图所示：  

    ![](//upload-images.jianshu.io/upload_images/1791824-8caa874787ad6335.png?imageMogr2/auto-orient/strip|imageView2/2/w/439)

    image.png

-   第四步，删除Anaconda的可能存在隐藏的文件，建议执行一下命令：

    > rm -rf ~/.condarc ~/.conda ~/.continuum

    经过上述4步后，Anaconda被彻底删除了。

  

> 作者：BillieZhang  
> 链接：https://www.jianshu.com/p/8747a347ea8b  
> 来源：简书  
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## 解决问题
#### 关闭Anaconda的自动启动base环境
mac安装了conda后，前面会有一个(base)，很烦人，终于找到最佳解决方案了：

$ conda config --set auto\_activate\_base false

原因：

安装conda后，每次启动终端，都会自动启动conda的base环境，conda的环境可以用 conda env list 查看

只要设置conda不要自动启动base环境就可以了。

> [水木青枫](https://blog.csdn.net/u010666669) 2019-05-10 22:56:16 