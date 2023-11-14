---
title: Python 之 itertools 工具包
authors: Ethan Lin
year: 2023-11-13
tags:
  - 类型/笔记
  - 日期/2023-11-13
  - 内容/编程语言/Python
  - 类型/AI问答笔记
---



> [!attention]
> 以下由AI回答，不保证正确性！
> 经过初步审核。



python 之 工具包 itertools 之 combinations 与 product 的区别？


itertools中的combinations和product都是用于生成组合的工具，但它们有一些区别。

combinations用于生成给定长度的所有可能的组合，而不考虑元素的顺序。例如，`combinations('ABCD', 2)`会生成AB, AC, AD, BC, BD, CD这样的组合。

而product用于生成多个可迭代对象的笛卡尔积，即所有可能的排列组合。例如，`product('AB', 'CD')`会生成AC, AD, BC, BD这样的组合。

因此，combinations生成的组合长度是固定的，而product生成的组合长度可以是可变的。