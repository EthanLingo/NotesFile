---
title: importlib库的方法举例
authors: Ethan Lin
year: 2022-11-27 
tags:
  - 日期/2022-11-27 
  - 类型/笔记 
  - 来源/转载 
  - 内容/python 
---


# importlib库的方法举例







importlib库的方法如下
替换如`import MODULE_A`这样的格式

```python
import importlib
module=importlib.import_module("MODULE_A")
#调用MODULE_A中的方法
getNowTime=module.FOUNCTION_B()
```


替换如`from PACKAGE_A import MODULE_B`这样的格式

```python
import importlib
module=importlib.import_module("PACKAGE_A.MODULE_B")
#调用MODULE_B中的方法FOUNCTION_C
getNowTime=module.FOUNCTION_C()
```


替换如`from PACKAGE_A .MODULE_B import FOUNCTION_C`这样的格式

```python
import importlib
from tornado.options import options
module=importlib.import_module("PACKAGE_A.MODULE_B")
FOUNCTION_C=module.FOUNCTION_C
#调用MODULE_B中的方法FOUNCTION_C
getNowTime=FOUNCTION_C()
```


替换如`from PACKAGE_A.MODULE_B import *`这样的格式

```python
import importlib
module=importlib.import_module("PACKAGE_A.MODULE_B")
withoutArgs=['__name__', '__doc__', '__package__', '__loader__', '__spec__', '__file__', '__cached__', '__builtins__']
keyList=list(module.__dict__.keys())
for k in keyList:
    if k not in withoutArgs:
        globals()[k]=module.__dict__.get(k)
#直接调用MODULE_B中的方法FOUNCTION_C
getNowTime=FOUNCTION_C()
```


------------------------------------------------
> 版权声明：本文为CSDN博主「招手熊」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/dorlolo/article/details/117930589
