---
title: pip删除所有包
authors: Ethan Lin
year: 2022-10-27 
tags:
  - 日期/2022-10-27 
  - 类型/笔记 
  - 内容/python 
---


# pip删除所有包







1. 导出所有包
`pip freeze > requirements.txt`

2. 删除所有包

`pip uninstall -r requirements.txt`
or
`pip uninstall -r requirements.txt -y`

————————————————
> 版权声明：本文为CSDN博主「子燕若水」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/u010087338/article/details/108914416


