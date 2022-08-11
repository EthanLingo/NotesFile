#内容/编程/Julia语言
#内容/赋值


# Julia给结构体数组赋值



```julia
# 构建一个结构体

mutable struct s

s1::Int64

s2::String

s3::Float64

end

  

# 构建一个结构体数组vec_a

  

vec_a=fill(s(1," ",2.0),10)

  

# 修改vec_a其中一个元素之值

vec_a[2].s2="hello"

  

# 输出vec_a，发现其各个元素全变了，因为每一个元素指向同一个struct

vec_a

  

# 如果采用这个方式，则每一个元素指向各自的struct实例，不会出现一处赋值，处处变动的情况

vec_b=[s(1," ",2.0) for vec_b in 1:10]

vec_b[2].s2="hello"

vec_b
```