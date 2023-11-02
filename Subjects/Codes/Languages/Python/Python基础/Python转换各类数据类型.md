---
title: Python转换各类数据类型
authors: Ethan Lin
year:
tags:
  - 内容/编程语言/Python 
  - 来源/转载 
---


# Python转换各类数据类型





1、字典（dict）

dict = {‘name’: ‘Zara’, ‘age’: 7, ‘class’: ‘First’}

1.1 字典——字符串

返回：

print type(str(dict)), str(dict)
1
1.2 字典——元组

返回：(‘age’, ‘name’, ‘class’)

print tuple(dict)
1
1.3 字典——元组

返回：(7, ‘Zara’, ‘First’)

print tuple(dict.values())
1
1.4 字典——列表

返回：[‘age’, ‘name’, ‘class’]

print list(dict)
1
1.5 字典——列表

print dict.values



2、元组

tup=(1, 2, 3, 4, 5)

2.1 元组——字符串

返回：(1, 2, 3, 4, 5)

print tup.__str__()
1
2.2 元组——列表

返回：[1, 2, 3, 4, 5]

print list(tup)
1
2.3 元组不可以转为字典



3、列表

nums=[1, 3, 5, 7, 8, 13, 20];

3.1 列表——字符串

返回：[1, 3, 5, 7, 8, 13, 20]

print str(nums)
1
3.2 列表——元组

返回：(1, 3, 5, 7, 8, 13, 20)

print tuple(nums)
1
3.3 列表不可以转为字典



4、字符串

4.1 字符串——元组

返回：(1, 2, 3)

print tuple(eval("(1,2,3)"))
1
4.2 字符串——列表

返回：[1, 2, 3]

print list(eval("(1,2,3)"))
1
4.3 字符串——字典

返回：

print type(eval("{'name':'ljq', 'age':24}"))
————————————————
> 版权声明：本文为CSDN博主「Violet-Guo」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/violet_echo_0908/article/details/52486689