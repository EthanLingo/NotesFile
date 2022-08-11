# Julia字典数据赋值给结构体数据

tags: #日期/2022-08-11 #类型/笔记 #内容/编程语言/Julia #内容/处理数据 

```julia
julia> # 定义结构体
       mutable struct St
           s1::Int64
           s2::Int64
       end

julia> # 生成数组，元素为结构体
       st1 = St(10,20)
St(10, 20)

julia> st2 = St(10 .* 10, 20 .* 10)
St(100, 200)

julia> a = @dict(
           s1,
           s2
       )
Dict{Symbol, Int64} with 2 entries:
  :s1 => 10
  :s2 => 20

julia> # 获取结构体成员名列表
       fieldNames=fieldnames(St)
(:s1, :s2)

julia> # 遍历成员名，设置以字典值
       for (i,v) in enumerate(fieldNames)
           setfield!(st2,v,a[v])
       end

julia> st2
St(10, 20)
```