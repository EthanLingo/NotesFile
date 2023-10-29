# DataFrames


---
title: DataFrames
authors: Ethan Lin
year:
tags:
  - 内容/编程/Julia语言 
  - 内容/科学计算 
---



# 一些注意点


由于`df[!, :col]`不复制，更改此语法返回的列向量元素将影响存储在原始`df`中的值。要获取列的副本，请使用`df[:, :col]`：更改此语法返回的向量不会更改`df`。


# 数据类型转换


## 例子：导出字典数组为DataFrame

问题：

有一系列的字典，如下所示：

```julia
julia> data  
2-element Array{Any,1}:  
 Dict{String,Any}("ratio1"=>1.36233,"time"=>"2014-06-19T15:47:40.000000Z","ratio2"=>1.36243)
 Dict{String,Any}("ratio1"=>1.3623,"time"=>"2014-06-19T15:48:00.000000Z","ratio2"=>1.36245)
```

如何一次将其弹出到DataFrame中，而无需循环遍历每本词典并逐个键入关键字

答案：

一种方法是

```
julia> vcat(DataFrame.(data)...)
2×3 DataFrame
│ Row │ ratio1  │ ratio2  │ time                        │
│     │ Float64 │ Float64 │ String                      │
├─────┼─────────┼─────────┼─────────────────────────────┤
│ 1   │ 1.36233 │ 1.36243 │ 2014-06-19T15:47:40.000000Z │
│ 2   │ 1.3623  │ 1.36245 │ 2014-06-19T15:48:00.000000Z │

julia> @btime vcat(DataFrame.($data)...)
  31.146 μs (157 allocations: 12.19 KiB)
```

即将每个`Dict`转换为`DataFrame`并将它们连接起来。

更详细的解释：

-   `DataFrame(somedict)`是一个构造函数调用，它从`DataFrame`创建一个`Dict`
-   `DataFrame.(arrayofdicts)`：构造函数调用[broadcasts](https://docs.julialang.org/en/v1/manual/arrays/#Broadcasting-1)处的点使得所有包含的`Dict`都转换为`DataFrame` s，并且我们得到{{ 1}} s。有关更多信息，请参见Julia文档中的[Dot Syntax for Vectorizing Functions](https://docs.julialang.org/en/v1/manual/functions/#man-vectorized-1)。
    
-   `DataFrame`：我们现在将`vcat(DataFrame.(arrayofdicts)...)`的数组[splat](https://docs.julialang.org/en/v1/base/base/#...)放入`DataFrame`函数中，该函数将它们垂直（行）连接。
    




