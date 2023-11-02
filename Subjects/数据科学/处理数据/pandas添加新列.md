---
title: pandas添加新列
authors: Ethan Lin
year: 2023-01-01 
tags:
  - 日期/2023-01-01 
  - 类型/笔记 
  - 类型/转载 
  - 内容/处理数据 
  - 内容/pandas 
  - 内容/python 
---


# pandas添加新列




pandas为DataFrame格式数据添加新列的方法非常简单，只需要新建一个列索引，再为其赋值即可。

添加新列的方法，如下：

## 一、`insert()`函数

语法：

> DataFrame.insert(loc, column, value,allow_duplicates = False)

参数

说明

loc

必要字段，int类型数据，表示插入新列的列位置，原来在该位置的列将向右移。

column

必要字段，插入新列的列名。

value

必要字段，新列插入的值。如果仅提供一个值，将为所有行设置相同的值。可以是int，string，float等，甚至可以是series /值列表。

allow_duplicates

布尔值，用于检查是否存在具有相同名称的列。默认为False，不允许与已有的列名重复。


## 二、直接赋值法

语法：df[‘新列名’]=新列的值

## 三、`reindex()`函数

语法：df.reindex(columns=[原来所有的列名,新增列名],fill_value=值)

reindex()函数用法较多，此处只是针对添加新列的用法

注：该方法需要把原有的列名和新列名都加上，如果列名过多，就比较麻烦。



## 四、`concat()`函数

原理：利用拼接的方式，添加新的一列。好处是可以同时新增多个列名。

concat()函数用法较多，此处只是针对添加新列的用法


## 五、`loc()`函数

原理：利用loc的行列索引标签来实现。

语法：df.loc[:,新列名]=值


> 来源：
> [pandas添加新列的5种常见方法_python_脚本之家](https://www.jb51.net/article/251192.htm)