# MATLAB建立cell数组问题



- 问题   如题，建立一个3*3的cell数组，想要让其中的每个元素都为矩阵a，该怎么办？   我的方法报错，，       >> clear all   >> b=cell(3)       b =          []  []  []     []  []  []     []  []  []       >> a=zeros(3)       a =          0   0      0      0   0      0      0   0      0       >> b{:,:}=a   需要大括号或点索引表达式中的一个输出，但结果有 9 个。

- 解答

- 方法一

- 1. b      = zeros(9,9);
  1. b =      mat2cell(b,3*ones(1,3),3*ones(1,3));

- *复制代码*

- 方法二

- 1. f      = @(x) zeros(3,3);
  1. b =      cell(3,3);
  1. b =      cellfun(f,b,'UniformOutput',false);

- *复制代码

- 来自 <http://www.ilovematlab.cn/thread-475270-1-1.html> 
