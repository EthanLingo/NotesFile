
在vscode里打开待处理文件，选择带正则表达式的搜索替换：

输入于搜索栏：
```text
(font-family: )("[^c].*)
```
输入于替换栏：
```text
$1serif, "Noto Serif CJK SC", $2
```
