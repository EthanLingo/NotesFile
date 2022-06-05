# R语言apply\(\)函数集合





本教程旨在介绍apply()函数集合。apply()函数是所有集合中最基本的。我们还将学习sapply()，lapply()和tapply()。apply集合可以看作是循环的替代品。

如果将R与Anaconda一起安装，则apply()集合与**R基本**软件包捆绑在一起。apply()函数可以提供许多函数，以对对象(数据框，列表，向量等)的集合执行冗余应用程序。apply()的目的主要是为了避免显式使用循环结构。它们可用于输入列表，矩阵或数组并应用函数。任何函数都可以传递到apply()中。

在本教程中，您将学习：

- apply()函数
- lapply()函数
- sapply()函数
- 切片矢量
- tapply()函数

## apply()函数

**apply()**将数据框或矩阵作为输入，并以矢量，列表或数组形式输出。apply()函数主要用于避免重复使用循环结构。它是所有可以在矩阵上使用的最基本的集合。

此函数接受3个参数：



```r
apply(X, MARGIN, FUN)
-x：数组或矩阵
-MARGIN：取一个介于1到2之间的值或范围，以定义该函数的应用位置：
    -MARGIN = 1`：对行执行操作
    -MARGIN = 2`：对列执行操作
    -MARGIN = c(1,2)`该操作在行和列上执行
-FUN：告诉应用哪个功能。可以应用平均值，中位数，和，最小值，最大值甚至用户定义的函数等内置函数
```

最简单的示例是对所有列求和。代码apply(m1，2，sum)将sum函数应用于矩阵5x6，并返回数据集中可访问的每一列的总和。



```r
m1 <- matrix(C<-(1:10),nrow=5, ncol=6)
m1
a_m1 <- apply(m1, 2, sum)
a_m1
```

**输出：**



![apply() function example in R](R语言apply函数集合.assets/032918_0401_applysapply1.png)

最佳实践：在将值打印到控制台之前，先存储它们。

## lapply()函数

**lapply()**函数可用于对列表对象执行操作，并返回与原始集合长度相同的列表对象。lappy()返回一个长度与输入列表对象相似的列表，其每个元素都是将FUN应用于列表的相应元素的结果。lapply()将列表，向量或数据框作为输入，并在列表中给出输出。



```r
lapply(X, FUN)
Arguments:
-X: A vector or an object
-FUN: Function applied to each element of x 
```

lapply()中的l代表列表。lapply()和apply()之间的区别在于输出返回之间。lapply()的输出是一个列表。lapply()可以用于其他对象，例如数据框和列表。

lapply()函数不需要MARGIN。

一个非常简单的示例是使用tolower函数将矩阵的字符串值更改为小写。我们用著名电影的名称构造一个矩阵。名称为大写形式。



```cpp
movies <- c("SPYDERMAN","BATMAN","VERTIGO","CHINATOWN")
movies_lower <-lapply(movies, tolower)
str(movies_lower)
```

**输出：**



```r
## List of 4
## $:chr"spyderman"
## $:chr"batman"
## $:chr"vertigo"
## $:chr"chinatown"
```

我们可以使用unlist()将列表转换为向量。



```cpp
films_lower <- unlist(lapply(movies，tolower))
str(movies_lower)
```

**输出：**



```cpp
##  chr [1:4] "spyderman" "batman" "vertigo" "chinatown"
```

## sapply()函数

**sapply()**函数将列表，向量或数据帧作为输入，并以向量或矩阵形式输出。它对列表对象的操作很有用，并返回与原始集合长度相同的列表对象。sapply()函数执行的功能与lapply()函数相同，但返回一个向量。



```cpp
sapply(X, FUN)
Arguments:
-X: A vector or an object
-FUN: Function applied to each element of x
```

我们可以从汽车数据集中测量汽车的最小速度和停车距离。



```swift
dt <- cars
lmn_cars <- lapply(dt, min)
smn_cars <- sapply(dt, min)
lmn_cars
smn_cars
```

**输出：**



```bash
## $speed
## [1] 4
## $ dist
## [1] 2
## speed  dist 
##     4     2
```

我们可以在lapply()或sapply()中使用用户内置函数。我们创建一个名为avg的函数来计算向量最小值和最大值的平均值。



```jsx
avg <- function(x) {  
  ( min(x) + max(x) ) / 2}
fcars <- sapply(dt, avg)
fcars
```

**输出量**



```bash
## speed  dist
##  14.5  61.0
```

sapply()函数在返回的输出中比lapply()更有效，因为sapply()将值直接存储到向量中。在下一个示例中，我们将看到情况并非总是如此。

下表总结了apply()，sapply()和lapply()之间的区别：

| Function | Arguments             | Objective                                         | Input                      | Output              |
| :------- | :-------------------- | :------------------------------------------------ | :------------------------- | :------------------ |
| apply    | apply(x, MARGIN, FUN) | Apply a function to the rows or columns or both   | Data frame or matrix       | vector, list, array |
| lapply   | lapply(X, FUN)        | Apply a function to all the elements of the input | List, vector or data frame | list                |
| sapply   | sappy(X FUN)          | Apply a function to all the elements of the input | List, vector or data frame | vector or matrix    |

## 切片矢量

我们可以使用lapply()或sapply()互换来切片数据框。我们创建一个函数below_average()，该函数接受数值的向量，并返回仅包含严格高于平均值的值的向量。我们将两个结果与 identical() 函数进行比较。



```jsx
below_ave <- function(x) {  
    ave <- mean(x) 
    return(x[x > ave])
}
dt_s <- sapply(dt, below_ave)
dt_l <- lapply(dt, below_ave)
identical(dt_s, dt_l)
```

**输出：**



```bash
## [1] TRUE
```

## tapply()函数

**tapply()**计算向量中每个因子变量的度量(均值，中位数，最小值，最大值等)或函数。这是一项非常有用的功能，可让您创建向量的子集，然后将某些功能应用于每个子集。



```cpp
tapply(X, INDEX, FUN = NULL)
Arguments:
-X: An object, usually a vector
-INDEX: A list containing factor
-FUN: Function applied to each element of x
```

数据科学家或研究人员的部分工作是计算变量汇总。例如，根据特征测量平均值或组数据。大多数数据按ID，城市，国家/地区等分组。总结小组会发现更多有趣的模式。

为了了解其工作原理，让我们使用虹膜数据集。该数据集在机器学习领域非常有名。该数据集的目的是预测三种花类中的每一种的类别：萼片，杂色和维珍妮卡。数据集收集每个物种的长度和宽度信息。

作为先前的工作，我们可以计算每个物种的长度的中位数。tapply()是执行此计算的快速方法。



```R
data(iris)
tapply(iris$Sepal.Width, iris$Species, median)
```

**输出：**



```css
##     setosa versicolor  virginica 
##        3.4        2.8        3.0
```



---



作者：你有康娜可爱吗
链接：https://www.jianshu.com/p/59fb24ca2ea7
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。