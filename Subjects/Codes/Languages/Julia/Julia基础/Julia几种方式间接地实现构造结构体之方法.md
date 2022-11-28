tags: #内容/编程/Julia语言 
#笔记 
#解决 
#类型/技巧


# Julia几种方式间接地实现构造结构体之方法

  

> 感谢QQ群：Julia中文社区（316628299）同学Indigo（1092702101）、yeruo（1954402990）的解答。

  

现状：需要构造除了结构体输入字段外，还希望构造能够通过某种函数形式初始化字段的方式，如平方和的函数形式。

问题：Julia语言不支持直接构造结构体方法。

解决：间接地实现构造结构体之方法。

  
  

## 方式1：构建函数

  
```julia
mutable struct A

a1

a2

# 希望定义a3=a1^2+a2^2 .

end

  

function a3(x::A)

x.a1^2 + x.a2^2

end

  

println(A(1, 2))



println(sumSquare(A(1, 2)))
```
 
优点：能通过在结构体外构造一个函数，间接实现结构体伪方法之实现。
缺点：不能直接将字段a3纳入结构体中。

## 方式2

  

```julia
mutable struct B

b1

b2

b3 # 希望定义b3=b1^2+b2^2 .

end

  

function B(x1, x2) # 这里实际上是函数B，只是同名于结构体B，建议写成不同名。

B(x1, x2, x1^2 + x2^2)

end

  

B1 = B(1, 2)

  

println(B1)
```

优点：可以实现将字段b3，其中$b3=b1^2+b2^2$纳入数组中。
缺点：只有在构造的时候直接写出该函数形式，不能够固化方法构造函数。
  

## 方式3

  
```julia
mutable struct E

e1

e2

e3 # 希望定义e3=e1^2+e2^2 .

end

  

function E_e3(s1, s2)

s1^2 + s2^2

end

  

function E(x1, x2) # 这里实际上是函数E，只是同名于结构体E，建议写成不同名。

E(x1, x2, e3(x1, x2))

end

  

E1 = E(1, 2)

  

println(E1)
```

优点：能够直接固化方法构造函数。
缺点：TODO。