# Python复制文件及其路径简易方法（后文附9种方法）


#内容/Python 

本文实例讲述了python实现复制整个目录的方法。分享给大家供大家参考。具体分析如下：

python有一个非常好用的目录操作类库shutil，通过这个库可以很简单的复制整个目录及目录下的文件

```python
import shutil
#复制文件
shutil.copyfile('listfile.py', 'd:/test.py')
#复制目录
shutil.copytree('d:/temp', 'c:/temp/')
#其余可以参考shutil下的函数
```


Python 中有许多“开盖即食”的模块（比如 os，subprocess 和 shutil）以支持文件 I/O 操作。在这篇文章中，你将会看到一些用 Python 实现文件复制的特殊方法。下面我们开始学习这九种不同的方法来实现 Python 复制文件操作。

在开始之前，你必须明白为什么了解最适合你的 Python 复制文件方法是如此重要。这是因为文件 I/O 操作属于性能密集型而且经常会达到瓶颈。这就是为什么你应该根据你的应用程序的设计选择最好的方法。

一些共享资源的程序会倾向于以阻塞模式来复制文件，而有些则可能希望以异步方式执行。比如 — 使用线程来复制文件或者启动单独的进程来实现它。还有一点需要考虑的是平台的可移植性。这意味着你应该知道你要运行的程序所在的目标操作系统（Windows/Linux/Mac OS X 等）。

# 用 Python 复制文件的 9 种方法具体是：

-   shutil copyfile() 方法
-   shutil copy() 方法
-   shutil copyfileobj() 方法
-   shutil copy2() 方法
-   os popen 方法
-   os system() 方法
-   threading Thread() 方法
-   subprocess call() 方法
-   subprocess check_output() 方法

## Shutil Copyfile()方法

只有当目标是可写的，这个方法才会将源内容复制到目标位置。如果你没有写入权限，则会导致 IOError 异常。

它会打开输入文件进行读取并忽略其文件类型。接下来，它不会以任何不同的方式处理特殊文件，也不会将它们复制为新的特殊文件。

Copyfile() 方法使用下面的低级函数 copyfileobj()。它将文件名作为参数，打开它们并将文件句柄传递给 copyfileobj()。这个方法中有一个可选的第三个参数，你可用它来指定缓冲区长度。然后它会打开文件并读取指定缓冲区大小的块。但是，默认是一次读取整个文件。

copyfile(source_file, destination_file)

以下是关于 copyfile() 方法的要点。

它将源内容复制到目标文件中。

如果目标文件不可写入，那么复制操作将导致 IOError 异常。

如果源文件和目标文件都相同，它将会返回 SameFileError。

但是，如果目标文件之前有不同的名称，那么该副本将会覆盖其内容。

如果目标是一个目录，这意味着此方法不会复制到目录，那么会发生 Error 13。

它不支持复制诸如字符或块驱动以及管道等文件。



```python
# Python Copy File - Sample Code

from shutil import copyfile  
from sys import exit

source = input("Enter source file with full path: ")  
target = input("Enter target file with full path: ")

# adding exception handling  

try:  
   copyfile(source, target)  
except IOError as e:  
   print("Unable to copy file. %s" % e)  
   exit(1)  
except:  
   print("Unexpected error:", sys.exc_info())  
   exit(1)

print("\nFile copy done!\n")

while True:  
   print("Do you like to print the file ? (y/n): ")  
   check = input()  
   if check == 'n':  
       break  
   elif check == 'y':  
       file = open(target, "r")  
       print("\nHere follows the file content:\n")  
       print(file.read())  
       file.close()  
       print()  
       break  
   else:  
       Continue
```



## Shutil Copy()方法

copyfile(source_file, [destination_file or dest_dir])

copy() 方法的功能类似于 Unix 中的“cp”命令。这意味着如果目标是一个文件夹，那么它将在其中创建一个与源文件具有相同名称（基本名称）的新文件。此外，该方法会在复制源文件的内容后同步目标文件权限到源文件。



```python
	import os  
import shutil

source = 'current/test/test.py'  
target = '/prod/new'

assert not os.path.isabs(source)  
target = os.path.join(target, os.path.dirname(source))
# create the folders if not already exists  

os.makedirs(target)

# adding exception handling  

try:  
   shutil.copy(source, target)  
except IOError as e:  
   print("Unable to copy file. %s" % e)  
except:  
   print("Unexpected error:", sys.exc_info())
```





## copy() vs copyfile() :

copy() 还可以在复制内容时设置权限位，而 copyfile() 只复制数据。

如果目标是目录，则 copy() 将复制文件，而 copyfile() 会失败，出现 Error 13。

有趣的是，copyfile() 方法在实现过程中使用 copyfileobj() 方法，而 copy() 方法则是依次使用 copyfile() 和 copymode() 函数。

在 Potion-3 可以很明显看出 copyfile() 会比 copy() 快一点，因为后者会有一个附加任务（保留权限）。

## Shutil Copyfileobj()方法

该方法将文件复制到目标路径或者文件对象。如果目标是文件对象，那么你需要在调用 copyfileobj() 之后关闭它。它还假定了一个可选参数（缓冲区大小），你可以用来设置缓冲区长度。这是复制过程中保存在内存中的字节数。系统使用的默认大小是 16KB。



```python
from shutil import copyfileobj  
status = False  
if isinstance(target, string_types):  
   target = open(target, 'wb')  
   status = True  
try:  
   copyfileobj(self.stream, target, buffer_size)  
finally:  
   if status:  
       target.close()
```



## Shutil Copy2()方法

虽然 copy2() 方法的功能类似于 copy()。但是它可以在复制数据时获取元数据中添加的访问和修改时间。复制相同的文件会导致 SameFileError 异常。

copy() vs copy2() :

copy() 只能设置权限位，而 copy2() 还可以使用时间戳来更新文件元数据。

copy() 在函数内部调用 copyfile() 和 copymode(), 而 copy2() 是调用 copystat() 来替换copymode()。

## Os Popen()方法



```python
from shutil import *  
import os  
import time  
from os.path import basename

def displayFileStats(filename):  
   file_stats = os.stat(basename(filename))  
   print('\tMode    :', file_stats.st_mode)  
   print('\tCreated :', time.ctime(file_stats.st_ctime))  
   print('\tAccessed:', time.ctime(file_stats.st_atime))  
   print('\tModified:', time.ctime(file_stats.st_mtime))

os.mkdir('test')

print('SOURCE:')  
displayFileStats(__file__)

copy2(__file__, 'testfile')

print('TARGET:')  
displayFileStats(os.path.realpath(os.getcwd() + '/test/testfile'))
```



该方法创建一个发送或者接受命令的管道。它返回一个打开的并且连接管道的文件对象。你可以根据文件打开模式将其用于读取或者写入比如‘r’（默认）或者‘w’。

os.popen(command[, mode[, bufsize]])

mode – 它可以是‘r’（默认）或者‘w’

Bufsize – 如果它的值是0，那么就不会出现缓冲。如果将它设置为1，那么在访问文件时就会发生行缓冲。如果你提供一个大于1的值，那么就会在指定缓冲区大小的情况下发生缓冲。但是，对于负值，系统将采用默认缓冲区大小。

对于Windows系统：

```python
import os  
os.popen('copy 1.txt.py 2.txt.py')
```

对于Liunx系统：

```python
import os  
os.popen('cp 1.txt.py 2.txt.py')
```



## Os System()方法

这是运行任何系统命令的最常用方式。使用 system() 方法，你可以调用 subshell 中的任何命令。在内部，该方法将调用 C 语言的标准库函数。

该方法返回该命令的退出状态。

对于 Windows 系统：

```python
import os  
os.system('copy 1.txt.py 2.txt.py') 
```

对于 Liunx 系统：

```python
import os  
os.system('cp 1.txt.py 2.txt.py')
```

使用异步方式的线程库复制文件

如果你想以异步方式复制文件，那么使用下面的方法。在这里，我们使用 Python 的线程模块在后台进行复制操作。

在使用这种方法时，请确保使用锁定以避免锁死。如果你的应用程序使用多个线程读取/写入文件，就可能会遇到这种情况。



```python
import shutil  
from threading import Thread

src="1.txt.py"  
dst="3.txt.py"

Thread(target=shutil.copy, args=[src, dst]).start()
```



## 使用Subprocess的Call()方法复制文件

Subprocess 模块提供了一个简单的接口来处理子进程。它让我们能够启动子进程，连接到子进程的输入/输出/错误管道，并检索返回值。

subprocess 模块旨在替换旧版模块和函数，比如 – os.system, os.spawn*, os.popen*, popen2.*

它使用 call() 方法调用系统命令来执行用户任务。



```python
import subprocess

src="1.txt.py"  
dst="2.txt.py"  
cmd='copy "%s" "%s"' % (src, dst)

status = subprocess.call(cmd, shell=True)

if status != 0:  
    if status < 0:  
        print("Killed by signal", status)  
    else:  
        print("Command failed with return code - ", status)  
else:  
    print('Execution of %s passed!\n' % cmd)
```



## 使用 subprocess 中的 Check_output() 方法复制文件

使用 subprocess 中的 Check_output() 方法，你可以运行外部命令或程序并捕获其输出。它也支持管道。



```python
import os, subprocess

src=os.path.realpath(os.getcwd() + "[http://cdn.techbeamers.com/1.txt.py](http://cdn.techbeamers.com/1.txt.py)")  
dst=os.path.realpath(os.getcwd() + "[http://cdn.techbeamers.com/2.txt.py](http://cdn.techbeamers.com/2.txt.py)")  
cmd='copy "%s" "%s"' % (src, dst)

status = subprocess.check_output(['copy', src, dst], shell=True)

print("status: ", status.decode('utf-8'))
```

