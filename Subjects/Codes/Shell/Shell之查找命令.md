Shell之查找命令
======

tags: #查阅笔记 #来源/转载 #知识 #发布/个人网站

  
  
  

日常操作时，经常需要查找文件。在Linux中，有很多方法可以做到这一点。

  
  

Linux常用命令中，有些命令可以帮助我们查找二进制文件，帮助手册或源文件的位置，也有的命令可以帮助我们查找磁盘上的任意文件，今天我们就来看看这些命令如何使用。

  

# 一

  

## **which**

  

which命令会在PATH变量指定的路径中，搜索某个系统命令的位置。例如：

  

```text

which -a which #查看命令which所在位置，-a参数表示找出所有

/usr/bin/which

/bin/which

```

  

PATH变量有哪些内容呢？我们来看一下(不同电脑可能不同)：

  

```text

echo $PATH

/home/hyb/bin:/home/hyb/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/jvm/java-8-oracle/bin:/usr/lib/jvm/java-8-oracle/db/bin:/usr/lib/jvm/java-8-oracle/jre/bin

```

  

PATH环境变量存放着一些路径信息，例如/usr/bin，当你在shell终端敲入一个命令，但是在PATH中包含的路径下没有时并且也不是内置命令时，就会提示：command not found。

  

当你已经安装了一个命令，但是使用时却提示找不到该命令，可以查看该环境变量，是否有你安装命令的路径。

  

所以是不是明白了为什么有些命令或程序需要添加环境变量才能直接使用了吧？

  

## **whereis**

  

whereis命令用于搜索程序的二进制文件，源代码文件或帮助文档。例如：

  

```text

whereis ls #如果上述三者有，则三者都会显示。

ls: /bin/ls /usr/share/man/man1/ls.1.gz

  

whereis -m ls #只查看ls的帮助手册

ls: /usr/share/man/man1/ls.1.gz

  

whereis -b ls #只查找ls的二进制文件

ls: /bin/ls

  

whereis stdio.h #查找stdio.h头文件，和帮助手册

stdio: /usr/include/stdio.h /usr/share/man/man3/stdio.3.gz

```

  

同样地，它不能查找到内置命令。

  

## **type**

  

type用于查看命令类型，一般有以下类型：

  

```text

alias：别名

keyword：关键字

builtin：内置命令

file：外部命令

```

  

而常见参数如下：

  

```text

-t 输出类型名，如file

-p 如果是外部命令，则显示其所在路径

-a 对于外部命令，它会显示命令路径，命令类型等信息

```

  

我们来看几个例子：

  

```text

type ls #ls是一个别名

ls is aliased to `ls --color=auto'

  

type cd #cd是一个内置命令

cd is a shell builtin

  

type find

find is /usr/bin/find

  

type function #function是一个shell关键字

function is a shell keyword

  

type -a which #显示所有路径

which is /usr/bin/which

which is /bin/which

```

  

## locate

  

前面所说的命令都限于查找命令，帮助手册或源文件，而locate用于快速查找任何文件。它从一个系统数据库进行文件查找，而不需要遍历磁盘，因此速度极快。通常该系统数据库每天更新一次（可以查看系统的/etc/cron.daily/[mlocate](https://www.zhihu.com/search?q=mlocate&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"427486457"})，不同系统可能不一样）。

  

常见选项如下：

  

```text

-e 仅查找存在的文件

-q 安静模式，不会显示任何错误讯息

-n 至多显示 n个输出

-r 使用正规运算式

-i 查找忽略大小写

-c 打印匹配结果数量

```

  

假设当前目录早已存在以下文件:

  

```text

locate.txt locate.log LOCATE.zip

```

  
  
  

我们来看一些实例。

  

**快速查找文件**

  

```text

locate locate.txt #查找locate.txt

/home/hyb/workspaces/shell/locate/locate.txt

```

  
  
  

**查找存在的文件**

  

```text

locate locate.txt #查找之前删除locate.txt

#虽然文件不存在，但是仍然被查找出来

/home/hyb/workspaces/shell/locate/locate.txt

locate -e locate.txt #-e参数可以查找只存在的文件

(由于该文件不存在，因此也不会被查找出来)

```

  

**查找计算文件的数量**

  

```text

locate -c locate.log #只计算查找到的数量

1

```

  
  
  

**忽略大小写查找**

  

```text

locate -i locate.zip

/home/hyb/workspaces/shell/locate/LOCATE.zip

```

  
  
  

**使用正则表达式**

  

普通的查找是模糊匹配的，因此只要目标名称中包含要搜索的名称，都会被搜索出来，但是我们可以利用正则表达式，来精确查找。

  

```text

locate -r /locate.log$ #查找以/locate.log结尾的文件

```

  
  
  

结合正则表达式，locate有更丰富的查找方式，这里不展开。

  

locate查找存在的一个问题是，如果最近有文件被删除，它仍然能找出来，最近有文件增加，它却找不到。也就是说，它的查找并不具备实时性。当然我们可以手动执行updatedb命令来更新数据库（可能需要root权限）。

  
  
  

## **find**

  

find命令是linux下一个强大的查找命令。与locate命令相比，它需要遍历磁盘文件，因此查找速度较慢，但正因如此，它的实时性比locate好得多。另外一方面，find命令的查找条件比locate丰富得多。

  

**以名称为条件**

  

最常用的恐怕就是以文件名为条件了，涉及参数-name，-iname，例如：

  

当前目录下查找以sort开头的文件：

  

```text

find ./ -name "sort*"

./sort4.txt

./sort2.txt

./sort3.txt

./sort.txt

find ./ -iname "SORT.txt" #忽略大小写

./sort.txt

```

  

**以权限为条件**

  

有时候需要查找特定权限的文件，可以使用-perm参数，例如查找当前目录下权限为777的文件：

  

```text

find ./ -perm 777

./test

./sort.txt

```

  

**以文件类型为条件**

  

涉及参数-type，例如要查找当前目录下的符号链接文件：

  

```text

find ./ -type l

./test

ls -al test

lrwxrwxrwx 1 hyb hyb 8 11月 24 10:10 test -> home.zip

```

  

主要类型有：

  

- f 普通文件

- d 目录

- b 块设备文件

- c 字符设备文件

- l 符号链接

- s 套接字

- p 管道文件

  

**以文件大小为条件**

  

涉及参数-size，例如：

  

```text

find ./ -size 1k #查找当前目录下小于1k的文件

./test

./sort4.txt

./sort2.txt

./sort3.txt

./test.sh

./sort.txt

find -size +1M #查找当前目录下大于1M的文件

./test.zip

```

  

常用单位有：

  

- k 千字节

- M 兆字节

- G 吉字节

- c 字节

- b 块，一般为512字节

- w 字大小，两个字节

  

**以归属为条件**

  

涉及参数-user，-nouser，-group，-nogroup等，例如：

  

```text

find ./ -user root #查找当前目录下root用户的文件

find ./ -nouser #查找当前目录下root用户的被删除的文件

```

  

-group，-nogroup类似的用法，只不过条件是用户组。

  

**以时间为条件**

  

涉及参数-mtime，-atime，-ctime，-newer，-anewer，-cnewer，-amin，-cmin等，例如：

  

```text

find ./ -mtime 3 #查找3天前更改过的文件

  

find ./ -mtime -3 #查找3天内更改过的文件

  

find ./ -mtime 0 #查找今天更改过的文件

  

find ./ -newer sort.txt #查找比sort.txt修改时间更新的文件

  

find ./ -anewer sort.txt #查找比sort.txt访问时间更新的文件

  

find ./ -amin 5 #查找5分钟之前访问过的文件

```

  

注：

  

- atime 最后访问时间

- mtime 最后修改时间

- ctime 最后修改时间，这里包括属性和权限

  

find命令的查找条件比较多，而其用法也非常丰富，本文仅简单介绍。

  
  
  
  
  
  
  

> 参考：

>

> 作者：通宵写代码

> 链接：https://zhuanlan.zhihu.com/p/427486457

> 来源：知乎

> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。