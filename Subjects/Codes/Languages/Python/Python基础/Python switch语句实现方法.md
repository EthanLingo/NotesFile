
tags: #来源/转载 
#类型/解决


[[Python基础]]
[[switch语句]]

# Python switch语句实现方法

与Java、C\C++等语言不同，Python中是不提供switch/case语句的，这一点让我感觉到很奇怪。我们可以通过如下几种方法来实现switch/case语句。

使用if…elif…elif…else 实现switch/case

可以使用if…elif…elif..else序列来代替switch/case语句，这是大家最容易想到的办法。但是随着分支的增多和修改的频繁，这种代替方式并不很好调试和维护。

使用字典 实现switch/case

可以使用字典实现switch/case这种方式易维护，同时也能够减少代码量。如下是使用字典模拟的switch/case实现：

```python
def num_to_string(num):
    numbers = {
        0 : "zero",
        1 : "one",
        2 : "two",
        3 : "three"
    }

    return numbers.get(num, None)

if __name__ == "__main__":
    print num_to_string(2)
    print num_to_string(5)
```

执行结果如下：

```shell
two
None
```


Python字典中还可以包括函数或Lambda表达式，代码如下：

```python
def success(msg):
    print msg

def debug(msg):
    print msg

def error(msg):
    print msg

def warning(msg):
    print msg

def other(msg):
    print msg

def notify_result(num, msg):
    numbers = {
        0 : success,
        1 : debug,
        2 : warning,
        3 : error
    }

    method = numbers.get(num, other)
    if method:
        method(msg)

if __name__ == "__main__":
    notify_result(0, "success")
    notify_result(1, "debug")
    notify_result(2, "warning")
    notify_result(3, "error")
    notify_result(4, "other")
```


执行结果如下：

```shell
success
debug
warning
error
other
```


通过如上示例可以证明能够通过Python字典来完全实现switch/case语句，而且足够灵活。尤其在运行时可以很方便的在字典中添加或删除一个switch/case选项。

在类中可使用调度方法实现switch/case

如果在一个类中，不确定要使用哪种方法，可以用一个调度方法在运行的时候来确定。代码如下：

```python
class switch_case(object):

    def case_to_function(self, case):
        fun_name = "case_fun_" + str(case)
        method = getattr(self, fun_name, self.case_fun_other)
        return method
    
    def case_fun_1(self, msg):
        print msg
    
    def case_fun_2(self, msg):
        print msg
    
    def case_fun_other(self, msg):
        print msg


if __name__ == "__main__":
    cls = switch_case()
    cls.case_to_function(1)("case_fun_1")
    cls.case_to_function(2)("case_fun_2")
    cls.case_to_function(3)("case_fun_other")

```


执行结果如下：

```shell
case_fun_1
case_fun_2
case_fun_other
```


总结

就个人来说，使用字典来实现switch/case是最为灵活的，但是理解上也有一定的难度。
————————————————
版权声明：本文为CSDN博主「数学与编码」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/l460133921/article/details/74892476