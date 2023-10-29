# python `__file__`、`__name__`、`__dict__`三个方法


---
title: python `__file__`、`__name__`、`__dict__`三个方法
authors: Ethan Lin
year:
tags:
  - 日期/2022-11-28 
  - 类型/笔记 
  - 来源/转载 
  - 内容/python 
---





# `__dict__`的用法

  `__dict__`可以作用在文件、类或者类的对象上，最终返回的结果为一个字典。

## 用在文件上

  能够获取到文件里所有的字典、元组、列表等属性，返回结果为一个字典。如，返回demo_test_dict文件里所有定义的字典、元组、列表等信息，

```python
from polls.python_study.study__dict__and__name__and__file__ import demo_test_dict

for i in demo_test_dict.__dict__:
    print(i, "=", demo_test_dict.__dict__[i])
```


其中demo_test_dict.py文件里包含的内容为:

```
a = [1, 2, 3]

b = (1, 2, 3, 4)

c = {"a": 2, "b": 1}
```


打印结果:

```
__name__ = polls.python_study.study__dict__and__name__and__file__.demo_test_dict
__doc__ = None
__package__ = polls.python_study.study__dict__and__name__and__file__
__loader__ = <_frozen_importlib_external.SourceFileLoader object at 0x0000021B1CDEF488>
__spec__ = ModuleSpec(name='polls.python_study.study__dict__and__name__and__file__.demo_test_dict', loader=<_frozen_importlib_external.SourceFileLoader object at 0x0000021B1CDEF488>, origin='D:\\pythonWorkspace\\django-study\\mysite\\polls\\python_study\\study__dict__and__name__and__file__\\demo_test_dict.py')
__file__ = D:\pythonWorkspace\django-study\mysite\polls\python_study\study__dict__and__name__and__file__\demo_test_dict.py
__cached__ = D:\pythonWorkspace\django-study\mysite\polls\python_study\study__dict__and__name__and__file__\__pycache__\demo_test_dict.cpython-37.pyc
__builtins__ = {'__name__': 'builtins', '__doc__': "Built-in functions, exceptions, and other objects.\n\nNoteworthy: None is the `nil' object; Ellipsis represents `...' in slices.", '__package__': '', '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': ModuleSpec(name='builtins', loader=<class '_frozen_importlib.BuiltinImporter'>), '__build_class__': <built-in function __build_class__>, '__import__': <built-in function __import__>, 'abs': <built-in function abs>, 'all': <built-in function all>, 'any': <built-in function any>, 'ascii': <built-in function ascii>, 'bin': <built-in function bin>, 'breakpoint': <built-in function breakpoint>, 'callable': <built-in function callable>, 'chr': <built-in function chr>, 'compile': <built-in function compile>, 'delattr': <built-in function delattr>, 'dir': <built-in function dir>, 'divmod': <built-in function divmod>, 'eval': <built-in function eval>, 'exec': <built-in function exec>, 'format': <built-in function format>, 'getattr': <built-in function getattr>, 'globals': <built-in function globals>, 'hasattr': <built-in function hasattr>, 'hash': <built-in function hash>, 'hex': <built-in function hex>, 'id': <built-in function id>, 'input': <built-in function input>, 'isinstance': <built-in function isinstance>, 'issubclass': <built-in function issubclass>, 'iter': <built-in function iter>, 'len': <built-in function len>, 'locals': <built-in function locals>, 'max': <built-in function max>, 'min': <built-in function min>, 'next': <built-in function next>, 'oct': <built-in function oct>, 'ord': <built-in function ord>, 'pow': <built-in function pow>, 'print': <built-in function print>, 'repr': <built-in function repr>, 'round': <built-in function round>, 'setattr': <built-in function setattr>, 'sorted': <built-in function sorted>, 'sum': <built-in function sum>, 'vars': <built-in function vars>, 'None': None, 'Ellipsis': Ellipsis, 'NotImplemented': NotImplemented, 'False': False, 'True': True, 'bool': <class 'bool'>, 'memoryview': <class 'memoryview'>, 'bytearray': <class 'bytearray'>, 'bytes': <class 'bytes'>, 'classmethod': <class 'classmethod'>, 'complex': <class 'complex'>, 'dict': <class 'dict'>, 'enumerate': <class 'enumerate'>, 'filter': <class 'filter'>, 'float': <class 'float'>, 'frozenset': <class 'frozenset'>, 'property': <class 'property'>, 'int': <class 'int'>, 'list': <class 'list'>, 'map': <class 'map'>, 'object': <class 'object'>, 'range': <class 'range'>, 'reversed': <class 'reversed'>, 'set': <class 'set'>, 'slice': <class 'slice'>, 'staticmethod': <class 'staticmethod'>, 'str': <class 'str'>, 'super': <class 'super'>, 'tuple': <class 'tuple'>, 'type': <class 'type'>, 'zip': <class 'zip'>, '__debug__': True, 'BaseException': <class 'BaseException'>, 'Exception': <class 'Exception'>, 'TypeError': <class 'TypeError'>, 'StopAsyncIteration': <class 'StopAsyncIteration'>, 'StopIteration': <class 'StopIteration'>, 'GeneratorExit': <class 'GeneratorExit'>, 'SystemExit': <class 'SystemExit'>, 'KeyboardInterrupt': <class 'KeyboardInterrupt'>, 'ImportError': <class 'ImportError'>, 'ModuleNotFoundError': <class 'ModuleNotFoundError'>, 'OSError': <class 'OSError'>, 'EnvironmentError': <class 'OSError'>, 'IOError': <class 'OSError'>, 'WindowsError': <class 'OSError'>, 'EOFError': <class 'EOFError'>, 'RuntimeError': <class 'RuntimeError'>, 'RecursionError': <class 'RecursionError'>, 'NotImplementedError': <class 'NotImplementedError'>, 'NameError': <class 'NameError'>, 'UnboundLocalError': <class 'UnboundLocalError'>, 'AttributeError': <class 'AttributeError'>, 'SyntaxError': <class 'SyntaxError'>, 'IndentationError': <class 'IndentationError'>, 'TabError': <class 'TabError'>, 'LookupError': <class 'LookupError'>, 'IndexError': <class 'IndexError'>, 'KeyError': <class 'KeyError'>, 'ValueError': <class 'ValueError'>, 'UnicodeError': <class 'UnicodeError'>, 'UnicodeEncodeError': <class 'UnicodeEncodeError'>, 'UnicodeDecodeError': <class 'UnicodeDecodeError'>, 'UnicodeTranslateError': <class 'UnicodeTranslateError'>, 'AssertionError': <class 'AssertionError'>, 'ArithmeticError': <class 'ArithmeticError'>, 'FloatingPointError': <class 'FloatingPointError'>, 'OverflowError': <class 'OverflowError'>, 'ZeroDivisionError': <class 'ZeroDivisionError'>, 'SystemError': <class 'SystemError'>, 'ReferenceError': <class 'ReferenceError'>, 'MemoryError': <class 'MemoryError'>, 'BufferError': <class 'BufferError'>, 'Warning': <class 'Warning'>, 'UserWarning': <class 'UserWarning'>, 'DeprecationWarning': <class 'DeprecationWarning'>, 'PendingDeprecationWarning': <class 'PendingDeprecationWarning'>, 'SyntaxWarning': <class 'SyntaxWarning'>, 'RuntimeWarning': <class 'RuntimeWarning'>, 'FutureWarning': <class 'FutureWarning'>, 'ImportWarning': <class 'ImportWarning'>, 'UnicodeWarning': <class 'UnicodeWarning'>, 'BytesWarning': <class 'BytesWarning'>, 'ResourceWarning': <class 'ResourceWarning'>, 'ConnectionError': <class 'ConnectionError'>, 'BlockingIOError': <class 'BlockingIOError'>, 'BrokenPipeError': <class 'BrokenPipeError'>, 'ChildProcessError': <class 'ChildProcessError'>, 'ConnectionAbortedError': <class 'ConnectionAbortedError'>, 'ConnectionRefusedError': <class 'ConnectionRefusedError'>, 'ConnectionResetError': <class 'ConnectionResetError'>, 'FileExistsError': <class 'FileExistsError'>, 'FileNotFoundError': <class 'FileNotFoundError'>, 'IsADirectoryError': <class 'IsADirectoryError'>, 'NotADirectoryError': <class 'NotADirectoryError'>, 'InterruptedError': <class 'InterruptedError'>, 'PermissionError': <class 'PermissionError'>, 'ProcessLookupError': <class 'ProcessLookupError'>, 'TimeoutError': <class 'TimeoutError'>, 'open': <built-in function open>, 'quit': Use quit() or Ctrl-Z plus Return to exit, 'exit': Use exit() or Ctrl-Z plus Return to exit, 'copyright': Copyright (c) 2001-2019 Python Software Foundation.
```



## 用在类上

  能够获取到类的所有成员方法和属性，包括静态方法(`@staticmethod`修饰)、非静态方法和类的构造方法。
   定义一个User类:

```
class User:
    # 类变量
    a = 1

    def __init__(self):
        self.a = 2
        self.b = 3
    
    @staticmethod
    def getUser():
        print(111)
    
    def get_name(self):
        print("获取用户名!")
```

获取到类的__dict__:

```python
from polls.python_study.study__dict__and__name__and__file__.__dict__class import User

for i in User.__dict__:
    print(i, ":", User.__dict__[i])
```


打印结果:

```
__module__ : polls.python_study.study__dict__and__name__and__file__.__dict__class
a : 1
__init__ : <function User.__init__ at 0x00000297FFC469D8>
getUser : <staticmethod object at 0x00000297FFC5F6C8>
get_name : <function User.get_name at 0x00000297FFC46AF8>
__dict__ : <attribute '__dict__' of 'User' objects>
__weakref__ : <attribute '__weakref__' of 'User' objects>
__doc__ : None
```


  由上可以发现，定义的成员变量和方法都可以获取到，最终返回的结果为字典。

## 用在类的对象上

  如果__dict__作用在对象上，那么获取到的是由类的属性构成的字典。

# 在对象上使用__dict__
```python
from polls.python_study.study__dict__and__name__and__file__.`__dict__`class import User

user = User()
for i in user.__dict__:
    print(i, "=", user.__dict__[i])
```


打印结果:

```
a = 2
b = 3
```


  由结果可知，返回的是User类的变量a和变量b。

# __name__的用法

  简单的来说，__name__就是用来获取名字。如果指定__name__的值为"main", 那么该if 语句可以当成程序的主方法入口，如果__name__所在的文件被其他文件import，那么__name__值为被调用的文件路径。

demo01.py:

```python
# 读取当前,如果没有指定，那么获取到的__name__为"__main__"

print(__name__)


class User:
    a = 1


# 读取类

print(User.__name__)

if __name__ == "__main__":
    print("这是程序的入口")
```


demo03.py:

```python
# 读取当前,如果没有指定，那么获取到的__name__为"__main__"

print(__name__)
from polls.python_study.study__dict__and__name__and__file__.name import demo01

class User:
    a = 1


# 读取类

print(User.__name__)

if __name__ == "__main__":
    print("这是程序的入口")
```


打印结果:

```
__main__
polls.python_study.study__dict__and__name__and__file__.name.demo01
User
User
这是程序的入口
```



# __file__的用法

   获取当前文件的绝对路径。

```python
print(__file__)
```


打印结果:

```
D:/pythonWorkspace/django-study/mysite/polls/python_study/study__dict__and__name__and__file__/file/demo01.py
```



------------------------------------------------
> 版权声明：本文为CSDN博主「Dream_it_possible！」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/qq_33036061/article/details/112799381
