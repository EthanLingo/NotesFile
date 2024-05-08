---
title: Pandas 注意事项
authors: Ethan Lin
year: 2024-04-30
tags:
  - 类型/笔记
  - 日期/2024-04-30
aliases:
  - Pandas 注意事项
---

# Pandas 注意事项


### 元组数据赋值给 pandas

在 `pandas.DataFrame` 中元组数据类型被视为序列（sequence）。当试图将这个序列赋值给 DataFrame 的一行时，pandas 试图将这个序列展开到多个列中，而不是将该序列直接存在单独的列。

