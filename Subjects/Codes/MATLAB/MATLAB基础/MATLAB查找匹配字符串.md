# MATLAB查找匹配字符串

在Matlab中，这几个函数区分如下：

（以下默认S1和S2是字符串，同样也适用于cell细胞类型数据，也就是循环对cell中每个元素分别判断即可。）

findstr(S1,S2)：寻找是否有S1和S2之间的匹配，真返回1，假返回0，双向；

例：     s = 'How much wood would a woodchuck chuck?';

​     findstr(s,'a')   returns  21

​         findstr('a',s)   returns  21

​        findstr(s,'wood') returns  [10 23]

​        findstr(s,'Wood') returns  []

​        findstr(s,' ')   returns  [4 9 14 20 22 32]

strfind(S1,S2):寻找S2是否匹配S1，和上面的唯一区别就是这个是单向的。请注意唯一的区别在例子中红字部分。

例：    s = 'How much wood would a woodchuck chuck?';

​        strfind(s,'a')   returns  21

​        strfind('a',s)   returns  []

​        strfind(s,'wood') returns  [10 23]

​        strfind(s,'Wood') returns  []

​        strfind(s,' ')   returns  [4 9 14 20 22 32]

strcmp(S1,S2):寻找S1和S2是否完全匹配，S1和S2没有顺序的区分。

例：    s= 'wooden';

​       strcmp(s,'wood')   returns 0

​       strcmp(s,'wooden')   returns 1

​       strcmp('wooden',s)   returns 1

strcnmp(S1,S2,n):寻找S1和S2的前n个字符是否完全匹配，S1和S2没有顺序的区分。

例：    s= 'wooden';

​       strncmp(s,'wood',4)   returns 1

​       strncmp(s,'wood',5)   returns 0

​       strncmp(s,'wooden',4)   returns 1

​       strncmp('wooden',s,4)   returns 1

strcmpi(S1,S2)与strncmpi(S1,S2,n)与上面分别对应的strcmp(S1,S2)与strncmp(S1,S2,n)完全相同，唯一的区分是匹配时不区分大小写。

**最重要的：**

strmatch(S1,S2):寻找S1是否匹配S2的开头部分，返回值是S1在S2中匹配的位置。

strmatch(S1,S2,'exact'):寻找S1是否和S2完全匹配，返回值是S1在S2中匹配的位置。

例：     S2=strvcat('max','minimax','maximum')

​        S2 =

max   

minimax

maximum

strmatch('max',S2) returns [1; 3] 表明1和3列匹配

strmatch('max',S2,'exact') returns [1] 表明1列完全匹配

**strmatch的一个好处是可以返回匹配的位置，而其余几个函数都只能返回判断值。**

**但是，strmatch在2011b之后的版本将被删除不再使用。根据个人推测的原因和网上求证如下：**

1、strmatch的功能完全可以由以上的几个函数实现。

2、strmatch是一个M文件，而其余几个函数都是内置的函数，因此在执行时，可以预测到strcmp的效率是远远高于strmatch的。

3、另一个因素，strmatch要先创建一个矩阵来储存返回的真值的位置，且在循环的过程中这个矩阵在不断变化；而strcmp仅仅返回真假。因此推测效率更高。

以上仅为推测，我没有做过测试。因此对于小程序来说，这点时间效率的对比实在不会太重要。总之，还是选择自己适合的函数就可以了。

参考文献：

<http://www.mathworks.com/matlabcentral/newsreader/view_thread/257590>

<http://www.mathworks.com/matlabcentral/newsreader/view_thread/145799>

<http://www.mathworks.com/matlabcentral/newsreader/view_thread/145799>

<http://www.mathworks.de/matlabcentral/newsreader/view_thread/294626>

 

来自 <http://blog.163.com/6_mao/blog/static/63271315201110203738923/> 
