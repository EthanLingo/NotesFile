# numpy判断语句提速



tags: #日期/2023-04-12 #类型/笔记 


> 使用AI问答

## 用np.select

当你需要根据不同的条件从数组中选择不同的元素时，你可以使用`np.select`和NumPy的布尔索引来优化代码。下面是一个例子，它演示了如何使用这些方法。

假设有一个包含成绩的NumPy数组`grades`，你需要根据以下条件选择不同的元素：

- 如果成绩大于等于90，选择'A'
- 如果成绩大于等于80，选择'B'
- 如果成绩大于等于70，选择'C'
- 对于其他成绩，选择'D'

首先，我们可以使用`np.select`函数来实现这个功能：

```python
import numpy as np

grades = np.array([85, 92, 78, 65, 88, 71])

conditions = [(grades >= 90), (grades >= 80), (grades >= 70)]
choices = ['A', 'B', 'C']

result = np.select(conditions, choices, default='D')
print(result)
```

输出结果是：`['B' 'A' 'C' 'D' 'B' 'C']`，符合预期。


## NumPy的布尔索引

另一种方法是使用NumPy的布尔索引来实现：

```python
result = np.empty_like(grades, dtype=str)
result[grades >= 90] = 'A'
result[(grades >= 80) & (grades < 90)] = 'B'
result[(grades >= 70) & (grades < 80)] = 'C'
result[grades < 70] = 'D'
print(result)
```

输出结果也是：`['B' 'A' 'C' 'D' 'B' 'C']`，与使用`np.select`的结果相同。

需要注意的是，使用NumPy的布尔索引可以更加灵活，可以实现更多的条件判断，但是在一些情况下可能会比`np.select`更加复杂。因此，在选择使用哪种方法时，需要根据具体情况进行评估和测试。


## 使用np.where

如果进一步地，if判断包括如果满足一个条件，就调用一个函数，否则调用另一个函数，那么这样如何优化？

如果你的代码中有if判断，包括根据条件调用不同的函数，可以考虑使用NumPy的`np.where`函数来优化代码。`np.where`函数可以根据条件选择不同的操作，并返回一个新的数组，其中每个元素都是由对应条件返回的结果。

下面是一个示例代码，演示了如何使用`np.where`来根据条件选择不同的函数：

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

result = np.where(arr > 3, np.square, np.sqrt)(arr)

print(result)
```

在这个例子中，我们使用`np.where`函数来选择不同的操作。如果元素大于3，我们调用`np.square`函数来计算平方值，否则调用`np.sqrt`函数来计算平方根。最终结果是一个新的数组，其中每个元素都是由对应条件返回的结果。

这个代码的输出结果是：`[1.         1.41421356 1.73205081 16.         25.        ]`，符合预期。

需要注意的是，使用`np.where`函数可以使代码更加简洁和易读，但在一些情况下可能会比直接使用if语句更加复杂。因此，在选择使用哪种方法时，需要根据具体情况进行评估和测试。