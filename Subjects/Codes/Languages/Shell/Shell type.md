type命令其实不能算查找命令，它是用来区分某个命令到底是由shell自带的，还是由shell外部的独立二进制文件提供的。如果一个命令是外部命令，那么使用-p参数，会显示该命令的路径，相当于which命令。

type命令的使用实例：

　　**$ type cd**

系统会提示，cd是shell的自带命令（build-in）。

　　**$ type grep**

系统会提示，grep是一个外部命令，并显示该命令的路径。

　　**$ type -p grep**

加上-p参数后，就相当于which命令。