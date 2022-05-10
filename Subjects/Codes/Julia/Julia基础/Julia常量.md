Julia常量
====


# 关于`undef`、`missing`、`nothing`

**undef** 是一个常量，它代表着单例类型 UndefInitializer 的唯一值。所谓的单例类型，是 指有且仅有一个实例的类型。无论我们实例化这种类型多少次，都只会得到同一个值，即该类型 的唯一值。UndefInitializer 类型专用于数组的初始化，其值表达的含义是创建一个未初始化 的数组。或者说，它表达的是上述构造函数的调用者不想向这个数组填充任何元素值。这时，Julia 会在该数组的所有元素位置上填充随机值。

在前面，我们传给数组构造函数的第一个参数值一直是 undef。但这只是初始化元素值的一 种选项而已。我们还可以选择 nothing 或 missing 作为这个参数的值。但前提是，该数组的元素类型必须是 nothing 或 missing 的类型的超类型。

nothing 和 missing 也是常量，它们的含义同样比较特殊，我们在前面的章节中对它们做过 解释。**nothing** 代表着单例类型 Nothing 的唯一值，它的含义是“此处没有值”。而 **missing** 代表单例类型 Missing 的唯一值，它的含义是“此处的值是缺失的”。


# 关于常量数组


Julia 常量只能保证名称与值之间的绑定是不可变的，并不能防止值本身的变化。

不建议使用常量数组赋值操作。实例如下：
```julia
**julia>** const O=ones(3)

3-element Vector{Float64}:

 1.0

 1.0

 1.0

  

**julia>** a=O

3-element Vector{Float64}:

 1.0

 1.0

 1.0

  

**julia>** b=O

3-element Vector{Float64}:

 1.0

 1.0

 1.0
 
**julia>** b[2]=5.0

5.0

  

**julia>** b

3-element Vector{Float64}:

 1.0

 5.0

 1.0

  

**julia>** a

3-element Vector{Float64}:

 1.0

 5.0

 1.0
```
变量`a`、变量`b`共同指向同一个内存区。此时会发现，当变量`b`修改之后，变量`a`也跟着修改。日常编程中，导致一些异常现象，因此不推荐用常量数组赋值操作。

