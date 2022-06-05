# MATLAB cell矩阵特定字符串检索



cell矩阵中字符的检索不能直接使用等号。

应用strcmp函数判断两个输入字符串是否相等，输入形式如下：

c = strcmp(str1,str2)比较字符串 str1 与 str2 ，若完全相等则返回 1 ，不相等返回 0

应用find函数对矩阵进行检索进一步的得到cell矩阵中特定字符所在的位置，输入形式如下：

[x,y] = find(strcmp(a,‘xx’))

a为需要检索的cell矩阵，‘xx’为特定的字符

示例如下：

\>> class1 = cell(1,4)

class1 =  []  []  []  []

\>> class1 = {'imagewant0','imagewant45','imagewant90','imagewant135'}

class1 =

  'imagewant0'  'imagewant45'  'imagewant90'  'imagewant135'

\>> [x , y] = find(strcmp(class1 , 'imagewant0'))

x =

   1

y =

   1

如果有多项的话x、y会分别是记录向量

 

来自 <http://jingyan.baidu.com/article/647f0115bd3d877f2048a856.html> 