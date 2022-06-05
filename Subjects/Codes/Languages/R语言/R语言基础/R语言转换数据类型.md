# R语言转换数据类型


#内容/编程/R语言 
#转载 
   

Clipped from: [https://blog.csdn.net/g863402758/article/details/53389495](https://blog.csdn.net/g863402758/article/details/53389495)

R语言数据类型转化

转自：[http://www.wangluqing.com/2014/09/10/r-share34/](http://www.wangluqing.com/2014/09/10/r-share34/)

有时候，对于一些问题，需要进行数据类型之间的转换。R提供了基本类型转换函数以解决数据类型转换这个问题。常用的基本数据类型转换函数汇总如下。

函数一：as.character(x)

函数二：as.complex(x)

函数三：as.numeric(x)或者as.double(x)

函数四：as.integer(x)

函数五：as.logical(x)

说明：上述函数表示，对于每个基本的数据类型，都有一个函数用来把其它数据类型的值转换为自己数据类型。转换成功，则得到相应的结果；反之，则得到NA值。举例说明如下。

> as.numeric("3.14") [1] 3.14 > as.logical(1) [1] TRUE > as.character(360) [1] "360" > as.complex(1) [1] 1+0i > as.numeric("abc") [1] NA Warning message: NAs introduced by coercion

上述转换函数可以扩展到基本向量类型，例如。

> as.character(c(1, 2, 3)) [1] "1" "2" "3" > as.numeric(c("1", "2", "3")) [1] 1 2 3

注意：逻辑值转换为数值时，TRUE的值为1，FALSE的值为0，例如。

> as.numeric(TRUE) [1] 1 > as.logical(1) [1] TRUE > as.numeric(FALSE) [1] 0 > as.logical(0) [1] FALSE