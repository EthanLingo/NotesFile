#内容/编程/Julia语言 
#教程 

Julia操作数组，应该在所有操作符前加`.`。

例如指定类型赋值：`a=Bool.([1,1,0,0])`、自累加：`a .|= [true,false,true,false]`。