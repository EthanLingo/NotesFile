---
title: Julia数组视图
authors: Ethan Lin
year:
tags:
  - 内容/编程/Julia语言 
  - 内容/处理数据 
---


# Julia数组视图






视图索引：

我们也可以把数组中的多个元素值汇聚到同一个视图里。这时，我们需要用中括号把多个线 性索引号包裹起来，并将其作为 view 函数的第二个参数值。比如：

```julia
julia> array4d_view2 = view(array4d, [1,3,5])

3-element view(::Array{Int64,1}, [1, 3, 5]) with eltype Int64: 1 3 5

julia> array4d_view2[[1, 2, 3]] 3-element Array{Int64,1}:

1

3

5

julia>
```

注意，视图中的各个元素值的线性索引号，不一定就等于它们在父数组中的那个线性索引号。 就拿视图 array4d_view2 来说。其中有 3 个元素值，它们在这个视图中的线性索引号分别是 1、 2 和 3。但是，后两个元素值在该视图的父数组 array4d 中的线性索引号却分别是 3 和 5。也就 是说，视图上分配的线性索引号与它的父数组没有任何关系。它们是单独排列的，互不干扰。