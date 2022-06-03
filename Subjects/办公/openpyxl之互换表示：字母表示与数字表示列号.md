openpyxl之互换表示：字母表示与数字表示列号
=========

 #内容/Excel软件 #内容/自动办公 #内容/编程语言/Python 

```python
from openpyxl.utils import get_column_letter, column_index_from_string

# 根据列的数字返回字母
print(get_column_letter(2))  # B
# 根据字母返回列的数字
print(column_index_from_string('D'))  # 4
```

> 来源：[openpyxl 实现excel字母列号与数字列号之间的转换](https://www.cnblogs.com/apple2016/p/9686433.html)
