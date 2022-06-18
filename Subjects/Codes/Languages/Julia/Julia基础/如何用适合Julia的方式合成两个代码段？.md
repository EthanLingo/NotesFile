tags: #内容/编程/Julia语言 
tags: #类型/解决 

# 问题：如何用适合Julia的方式合成两个代码段？



## 背景
有一个文件`model_skeleton.jl`装模型外围架构modelSkeleton，一个文件`model_content.jl`装模型核心内容modelContent。

## 需求
要使用模型生成器modelBuilder把模型核心内容加载进模型外围架构里，形成有意义的模型model，然后调用并运行该模型。

## 问题
目前想到的方法是模型生成器modelBuilder通过读写替换文件里的字符串内容实现生成一个模型。对于Julia来说，有没有比较精巧或者高效的方法，比如用宏+函数，实现同样的功能，调用两个文件`model_skeleton.jl`、`model_content.jl`内的代码段进行合成？

# 方式一：操作文件和替换字符串

文件：相关定义和函数`define.jl`
```julia
# 定义：模型核心内容结构体
struct ModelContent
    content::String
end

"""
定义：模型生成器
做如下事情：
1. 调取模型核心内容modelContent、模型外围框架modelSkeleton；
2. 插入模型核心内容modelContent至模型外围框架modelSkeleton内，组合成模型model；
3. 写出模型model为文件model.jl；
Argument: 
- modelContent::ModelContent: 模型核心内容
"""
function modelBuilder!(modelContent::ModelContent)

    ## 读取模型外围框架部分
    file_modelSkeleton = open("model_skeleton.jl", "r")
    string_modelSkeleton = read(file_modelSkeleton, String) 
    println("模型外围框架：\n" * string_modelSkeleton * "\n")
    close(file_modelSkeleton)
    
    ## 待生成模型
    string_model = string_modelSkeleton 
    println("替换前的模型：\n" * string_model * "\n")
    
    ## 依次替换文本内容
    re010 = r"## 插入modelContent"
    string_model = replace(string_model, re010 => modelContent.content)
    re020 = """println("我是模型外围架构。虽然我可以运行起来，但是我需要被插入核心内容，才能成为一个有意义的模型。")"""
    string_model = replace(string_model, re020 => """println("我是模型外围架构。")""")
    re030 = "modelSkeleton"
    string_model = replace(string_model, re030 => "model")
    println("替换后的模型：\n" * string_model * "\n")
    
    ## 写入文件
    run(`touch model.jl`)
    open("model.jl","w") do file_model
        write(file_model, string_model)
    end
   
end

# 定义：运行模型
macro runModel()
    expr = quote
        include("model.jl")
        model()
    end
    println("开始运行模型model：")
    eval(expr)
    println("结束运行模型model。")
end
```

文件：模型内容实例`model_content.jl`
```julia
# 模型内容实例
modelContent = ModelContent(
    """println("我是模型核心内容。")"""
)
```

文件：模型外围框架`model_skeleton.jl`
```julia
# 模型外围框架
function modelSkeleton()
    println("我是模型外围架构。虽然我可以运行起来，但是我需要被插入核心内容，才能成为一个有意义的模型。")
    ## 插入modelContent
end
```

文件：主程序入口`main.jl`
```julia
# 主程序入口

include("define.jl")
include("model_content.jl")
include("model_skeleton.jl")

## 生成模型model
modelBuilder!(modelContent)

## 运行模型model
@runModel
```

## 运行方式

上述四个程序文件放在同一个文件夹内。运行文件`main.jl`。会生成一个文件`model.jl`。程序自动调用`model.jl`并运行。

## 运行结果
```text
[Running] julia "/Users/ethan/Desktop/test/main.jl"
模型外围框架：
# 模型外围框架
function modelSkeleton()
    println("我是模型外围架构。虽然我可以运行起来，但是我需要被插入核心内容，才能成为一个有意义的模型。")
    ## 插入modelContent
end

替换前的模型：
# 模型外围框架
function modelSkeleton()
    println("我是模型外围架构。虽然我可以运行起来，但是我需要被插入核心内容，才能成为一个有意义的模型。")
    ## 插入modelContent
end

替换后的模型：
# 模型外围框架
function model()
    println("我是模型外围架构。")
    println("我是模型核心内容。")
end

开始运行模型model：
我是模型外围架构。
我是模型核心内容。
结束运行模型model。
```


# 方式二：使用Julia函数和结构体

感谢[Julia中文论坛相关帖子](https://discourse.juliacn.com/t/topic/6167) 中两位讨论者 @johnnychen94 @henry2004y 的想法和建议，结合以上，现在做了这样的改进：

## 改进后的代码

```julia

#===== 定义文件头 ======#

## 定义文件类型
struct ModelType end

## 定义模型核心内容
struct ModelContent
    components::Array{Any}
end

## 定义通用模型
struct GeneralModel{ModelType}
    name::String
    content::ModelContent
    fun::Function
end

## 定义模型外围架构
function modelSkeleton(modelContent::ModelContent)
    println("我是模型外围架构。")
    for i in modelContent.components
        println(i) # 此处运行模型核心内容
    end
    println("\n")
end

## 定义生成模型
function buildModel(modelName::String, modelContent::ModelContent; modelSkeleton::Function=modelSkeleton)
    modelType = Symbol(modelName)
    model = GeneralModel{modelType}(
        modelName,
        modelContent,
        modelSkeleton
    )
    println("已经生成模型$(model.name)")
    return model
end

## 定义运行模型
function runModel(model::GeneralModel)
    model.fun(model.content)
end

#===== 定义文件尾 ======#




#===== 设置文件头 ======#

## 写入模型xxx之名称、核心内容
xxxName = "xxx"
xxxContent = ModelContent(
    [
    "我是模型核心组件1。",
    "我是模型核心组件3。",
    "我是模型核心组件5。"
]
)

## 写入模型yyy之名称、核心内容
yyyName = "yyy"
yyyContent = ModelContent(
    [
    "我是模型核心组件1。",
    "我是模型核心组件2。",
    "我是模型核心组件4。"
]
)

#===== 设置文件尾 ======#



#===== 主文件头 ==========#
# include设置文件、定义文件。

## 生成模型xxx
xxxModel = buildModel(xxxName, xxxContent)

## 运行模型xxx
runModel(xxxModel)

## 生成模型yyy
yyyModel = buildModel(yyyName, yyyContent)

## 运行模型yyy
runModel(yyyModel)
#===== 主文件尾 ==========#

```

## 运行结果


```text
已经生成模型xxx
我是模型外围架构。
我是模型核心组件1。
我是模型核心组件3。
我是模型核心组件5。


已经生成模型yyy
我是模型外围架构。
我是模型核心组件1。
我是模型核心组件2。
我是模型核心组件4。
```



