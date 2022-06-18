# R语言管理包

tags: #内容/编程/R语言 

library和require都可以载入包，但二者存在区别。

在一个函数中，如果一个包不存在，执行到library将会停止执行，require则会继续执行。

在[http://stackoverflow.com/questions/5595512/what-is-the-difference-between-require-and-library](http://stackoverflow.com/questions/5595512/what-is-the-difference-between-require-and-library)看到对二者详细的说明。

require将会根据包的存在与否返回true或者false，

