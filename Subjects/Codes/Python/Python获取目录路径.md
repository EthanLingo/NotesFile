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