Julia字典操作
=====

#内容/编程/Julia语言 #内容/科学计算 

# 多个字典合并拼接成一个字典

方法一：
用函数`merge()`：
```julia
julia> a = Dict("foo" => 0.0, "bar" => 42.0)
Dict{String, Float64} with 2 entries:
  "bar" => 42.0
  "foo" => 0.0

julia> b = Dict("baz" => 17, "bar" => 4711)
Dict{String, Int64} with 2 entries:
  "bar" => 4711
  "baz" => 17

julia> merge(a, b)
Dict{String, Float64} with 3 entries:
  "bar" => 4711.0
  "baz" => 17.0
  "foo" => 0.0

julia> merge(b, a)
Dict{String, Float64} with 3 entries:
  "bar" => 42.0
  "baz" => 17.0
  "foo" => 0.0
```

该函数也能用于元组类型。



方法二：

```julia
**julia>** d1=Dict(:d11=>1,:d12=>2)

Dict{Symbol, Int64} with 2 entries:

  :d11 => 1

  :d12 => 2

  

**julia>** d2=Dict(:d21=>3,:d22=>4)

Dict{Symbol, Int64} with 2 entries:

  :d22 => 4

  :d21 => 3


**julia>** dd=Dict([collect(d1);collect(d2)])

Dict{Symbol, Int64} with 4 entries:

  :d11 => 1

  :d22 => 4

  :d21 => 3

  :d12 => 2

```


