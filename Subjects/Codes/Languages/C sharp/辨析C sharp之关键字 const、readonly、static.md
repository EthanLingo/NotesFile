# 辨析C Sharp之关键字 const、readonly、static
tags: #来源/转载 #内容/编程/Csharp #类型/辨析 #发布/个人网站 

const: compile time初始化，效率高，属于类（所以不用加static）的常量，只能用常数来给它赋值。 

readonly：runtime初始化，效率没有const高。
	如果前面加上了static，那么它就是属于类的常量，如果没有加，就是属于对象的常量，无论加没有加static，都可以在定义的时候初始化，而如果加了static，还可以在static constructor里面初始化，如果没有加static，还可以在一般的constructor里面初始化。
	readonly没有const限制那么大，因为readonly在runtime而不是compile time初始化的，所以我们可以用常数或者用函数的返回值来给他初始化（比如：readonly int a = GetInt()，const就不行）。

————————————————

> 版权声明：本文为CSDN博主「Andy韩」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：[Fetching Title#l46q](https://blog.csdn.net/andyhan_1001/article/details/80331460)

