# pip备份离线包


---
title: pip备份离线包
authors: Ethan Lin
year:
tags:
  - 日期/2022-10-27 
  - 类型/笔记 
  - 内容/python 
---



1. 导出

`pip freeze >  requirements.txt`

2. 在其他环境安装

`pip install -r  requirements.txt  `

3. 离线包

`pip download  -r requestments.txt  -d  ./pip_packages    #从当前环境的网络中下载requestments.txt`中写的包，下载到当前目录下的pip_packages目录中，这时候你会发现，里面有很多依赖，还有一些whl文件

4. 安装

`pip install --no-index --find-links=d:\packages -r requirements.txt # --find-links指定的是包文件的存放地址，-r指定的是txt文件的位置`

> 来源：
> [python 导出环境输出到requirements.txt，导出离线包，并安装 - 乔小生1221 - 博客园](https://www.cnblogs.com/qxh-beijing2016/p/13187153.html)

