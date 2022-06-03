#知识 
#笔记 
#内容/编程语言/Python/Numpy
#内容/编程
#内容/科学计算



# Numpy知识笔记

## 数据类型

![[Pasted image 20211101191327.png]]



## 常用功能函数

   
### max、maximum
-   np.max：(a, axis=None, out=None, keepdims=False) 

-   求序列的最值
-   最少接收一个参数
-   axis：默认为列向（也即 axis=0），axis = 1 时为行方向的最值；

-   np.maximum：(X, Y, out=None) 

-   X 与 Y 逐位比较取其大者；
-   最少接收两个参数

来自 <[http://blog.csdn.net/lanchunhui/article/details/52700895](http://blog.csdn.net/lanchunhui/article/details/52700895)>

   

## Numpy多维数组的轴对换 transpose

2018年04月01日 11:49:50 [TzeSing](https://me.csdn.net/weixin_40001181) 阅读数：219

转置中，transpose方法返回的是源数据的视图，就是说修改了视图就会把源数据也改了。

高维数组，transpose的方法如下展示

创建一个形状为(2,2,4)的三维数组：

```python
>>> arr = np.arange(16).reshape((2,2,4))
>>> arr

array([[[ 0, 1, 2, 3],
[ 4, 5, 6, 7]],
[[ 8, 9, 10, 11],
[12, 13, 14, 15]]])
```

transpose需要放入一个由轴编号组成的元组才能变换，意思就是放入需要改变的shape

我需要把 0轴 和 1轴 对调，2轴不变，就是放入(1,0,2)

```python
>>> arr.transpose((1,0,2))

array([[[ 0, 1, 2, 3],
[ 8, 9, 10, 11]],
[[ 4, 5, 6, 7],
[12, 13, 14, 15]]])
```

这里就需要解释一下了，例如第二行的8这个数，这个位置原来是4，4对应的坐标为(0,1,0)——第3维的第一个元素中的第二个元素的第一个。经过transpose转换之后，这个位置对应的便是(1,0,0)中的8，如此类推
## 数组

### 保存数组

   

[Python Numpy数组保存](http://www.cnblogs.com/ice-daigua/archive/2012/11/16/2772674.html)

 Numpy提供了几种数据保存的方法。

 以3\*4数组a为例：

`a.tofile("filename.bin")`

 这种方法只能保存为二进制文件，且不能保存当前数据的行列信息，文件后缀不一定非要是bin，也可以为txt，但不影响保存格式，都是二进制。

 这种保存方法对数据读取有要求，需要手动指定读出来的数据的的dtype，如果指定的格式与保存时的不一致，则读出来的就是错误的数据。

`b = numpy.fromfile("filename.bin",dtype = **)`

 读出来的数据是一维数组，需要利用

 `b.shape = 3,4`重新指定维数。

`numpy.save("filename.npy",a)`

 利用这种方法，保存文件的后缀名字一定会被置为.npy，这种格式最好只用

 `numpy.load("filename")`来读取。

```python
numpy.savetxt("filename.txt",a)
b =  numpy.loadtxt("filename.txt")
```

 用于处理一维和二维数组

来自 <[http://www.cnblogs.com/ice-daigua/archive/2012/11/16/2772674.html](http://www.cnblogs.com/ice-daigua/archive/2012/11/16/2772674.html)>

### 多维数组



### 展平数组

ravel()

flatten()

reshape()用元组设置维度