#内容/编程/Julia语言 
#教程 
#笔记 


赋值规则`=`，函数`copy()`与`deepcopy()`只针对数组有效。


Julia数组复制，是否取子值的影响，见示例：
      
```julia
julia> a=[1 1 1]

1×3 Matrix{Int64}:

 1 1 1

  

julia> b=[2 2 2]

1×3 Matrix{Int64}:

 2 2 2

  

julia> a=b[:]

3-element Vector{Int64}:

 2

 2

 2

  

julia> a=[1 1 1]

1×3 Matrix{Int64}:

 1 1 1

  

julia> a[:]=b

1×3 Matrix{Int64}:

 2 2 2

  

julia> b.+=3

1×3 Matrix{Int64}:

 5 5 5

  

julia> a

1×3 Matrix{Int64}:

 2 2 2

  

julia>
```