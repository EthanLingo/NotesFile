# Python获取目录路径

#内容/Python 

在使用python的时候总会遇到路径切换的使用情况，如想从文件夹test下的test.py调用data文件夹下的data.txt文件：

```text
.
└── folder
    ├── data
    │   └── data.txt
    └── test
        └── test.py
```

一种方法可以在data文件下加入__init__.py 然后在test.py 中import data 就可以调用data.txt文件；

另一种方法可以借助python os模块的方法对目录结构进行操作，下面就说一下这种方式的使用：

```python
import os

print '***获取当前目录***'
print os.getcwd()
print os.path.abspath(os.path.dirname(__file__))

print '***获取上级目录***'
print os.path.abspath(os.path.dirname(os.path.dirname(__file__)))
print os.path.abspath(os.path.dirname(os.getcwd()))
print os.path.abspath(os.path.join(os.getcwd(), ".."))

print '***获取上上级目录***'
print os.path.abspath(os.path.join(os.getcwd(), "../.."))

输出结果为：

***获取当前目录***
/workspace/demo/folder/test
/workspace/demo/folder/test

***获取上级目录***
/workspace/demo/folder
/workspace/demo/folder
/workspace/demo/folder

***获取上上级目录***
/workspace/demo
```
————————————————
> 版权声明：本文为CSDN博主「ljzhangi」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/leorx01/article/details/71141643



# Python设置工作路径



> 来源：[菜鸟教程：Python os.chdir() 方法](https://www.runoob.com/python/os-chdir.html)

## Python os.chdir() 方法

 [![Python File(文件) 方法](https://www.runoob.com/images/up.gif) Python OS 文件/目录方法](https://www.runoob.com/python/os-file-methods.html)

---

### 概述

os.chdir() 方法用于改变当前工作目录到指定的路径。

### 语法

**chdir()**方法语法格式如下：

```os.chdir(path)```

### 参数

-   **path** -- 要切换到的新路径。 
    

### 返回值

如果允许访问返回 True , 否则返回False。

### 实例

以下实例演示了 chdir() 方法的使用：

```python
#!/usr/bin/python

# -*- coding: UTF-8 -*-

import os, sys

path = "/tmp"



# 查看当前工作目录

retval = os.getcwd()
print "当前工作目录为 %s" % retval

# 修改当前工作目录

os.chdir( path )

# 查看修改后的工作目录

retval = os.getcwd()

print "目录修改成功 %s" % retval

执行以上程序输出结果为：

当前工作目录为 /www
目录修改成功 /tmp
```

 [![Python File(文件) 方法](https://www.runoob.com/images/up.gif) Python OS 文件/目录方法](https://www.runoob.com/python/os-file-methods.html)