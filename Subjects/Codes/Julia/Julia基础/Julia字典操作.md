Julia字典操作
=====

#内容/编程/Julia语言 #内容/科学计算 

# 多个字典扁平地拼接成一个字典

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
