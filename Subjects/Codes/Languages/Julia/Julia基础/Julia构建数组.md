#内容/编程/Julia语言 


# Julia构建数组

构建一个元组素组，尺寸3×3，用于表示矩阵行列下标。

```julia
reshape([(i, j) for j = 1:3 for i = 1:3], 3, 3)
```



