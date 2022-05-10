#内容/编程/Julia语言 
#教程 

Julia操作数组，应该在所有操作符前加`.`。

例如指定类型赋值：`a=Bool.([1,1,0,0])`、自累加：`a .|= [true,false,true,false]`。



# 函数`zip`

函数 [Base.Iterators.zip](https://docs.juliacn.com/dev/base/iterators/#Base.Iterators.zip) 用于生成元组对，通过两个同尺寸数组。实例用法：

```
julia> a = 1:5
1:5

julia> b = ["e","d","b","c","a"]
5-element Vector{String}:
 "e"
 "d"
 "b"
 "c"
 "a"

julia> c = zip(a,b)
zip(1:5, ["e", "d", "b", "c", "a"])

julia> length(c)
5

julia> first(c)
(1, "e")
```