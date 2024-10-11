---
title: Shell手动终止进程
authors: Ethan Lin
year: 2024-10-08
tags:
  - 类型/笔记
  - 日期/2024-10-08
aliases:
  - Shell手动终止进程
---
# Shell手动终止进程



手动终止进程。终止方式为：在终端键入`ps aux | grep ssh`查看相关进程的 sid，然后键入
`kill -9 【查找到的sid】`。

备注：
- sid 是列表的第二列的那个五位数的值。
- 如果想要一次终止多个进程，可以用空格隔开输入多个sid号。
