# Python语言获取list指定下标


---
title: Python语言获取list指定下标
authors: Ethan Lin
year:
tags:
  - 内容/编程语言/Python 
---




方法一：index字段

```python
list1 = [1,22,31,4,6,7,8,23,5,89,90]
f1 = list1.index(22)
```


方法二：numpy.where
```python
>>> import numpy
>>> vector = numpy.array([5,10,15,20])
>>> print(vector)
>>> a = numpy.where(vector==10)  
>>> print(a)

```



