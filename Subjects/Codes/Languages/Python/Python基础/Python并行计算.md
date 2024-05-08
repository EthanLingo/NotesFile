---
title: Python并行计算
authors: Ethan Lin
year: 2024-04-26
tags:
  - 类型/AI问答笔记
  - 日期/2024-04-26
---
# Python并行计算

采用内置的 `multiprocessing` 多进程并行计算。


> [!attention]
> 以下由AI回答，不保证正确性！







#### `p.starmap`与`p.map`的区别？

`multiprocessing.Pool.map` 和 `multiprocessing.Pool.starmap` 都是 Python 的并行处理函数，它们的主要区别在于如何处理函数参数。  
`multiprocessing.Pool.map(func, iterable)`：它将 `iterable` 中的每个元素作为单个参数传递给 `func`。因此，`func` 应该只接受一个输入参数。  
`multiprocessing.Pool.starmap(func, iterable)`：它将 `iterable` 中的每个元素（这些元素应该是元组）解包，然后将解包后的元素作为多个参数传递给 `func`。因此，`func` 可以接受多个输入参数。 