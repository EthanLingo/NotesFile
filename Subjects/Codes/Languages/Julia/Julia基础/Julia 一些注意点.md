---
title:
  - Julia 一些注意点
authors: Ethan Lin
year: 2024-03-29
tags:
  - 类型/笔记
  - 日期/2024-03-29
  - 内容/编程语言/Julia
---

# Julia 一些注意点





## 逻辑运算之运算顺序


例子：

`intersect_row .== 0` 是

```
4-element BitVector:
 1
 1
 1
 1
```

。 `intersect_col .== 0` 是

```
4-element BitVector:
 1
 0
 1
 1
```

。但是 `intersect_row .== 0 .& intersect_col .== 0` 结果是

```
4-element BitVector:
 1
 1
 1
 1
```

。







