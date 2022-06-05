
Map函数

In[1]:= Map[f, {a, b, c, d, e}]

Out[1]= {f[a], f[b], f[c], f[d], f[e]}

	

其他输入形式：

In[1]:= f /@ {a, b, c, d, e}

Out[1]= {f[a], f[b], f[c], f[d], f[e]}

	

用明确的纯函数：

In[1]:= (1 + g[#]) & /@ {a, b, c, d, e}

Out[1]= {1 + g[a], 1 + g[b], 1 + g[c], 1 + g[d], 1 + g[e]}

In[2]:= Function[x, x^2] /@ {1, 2, 3, 4}

Out[2]= {1, 4, 9, 16}

	

作用到顶层：

In[1]:= Map[f, {{a, b}, {c, d, e}}]

Out[1]= {f[{a, b}], f[{c, d, e}]}

作用到第 2 层：

In[2]:= Map[f, {{a, b}, {c, d, e}}, {2}]

Out[2]= {{f[a], f[b]}, {f[c], f[d], f[e]}}

作用到第 1 层和第 2 层：

In[3]:= Map[f, {{a, b}, {c, d, e}}, 2]

Out[3]= {f[{f[a], f[b]}], f[{f[c], f[d], f[e]}]}

	

使用映射操作符：

In[1]:= Map[f][{a, b, c, d}]

Out[1]= {f[a], f[b], f[c], f[d]}

	

把函数映射到 Association 的数值中：

In[1]:= Map[h, < | a -> b, c -> d | >]

Out[1]= < | a -> h[b], c -> h[d] | >

	

作用于嵌入式 Association 的第二层：

In[1]:= Map[h, < | a -> < | b -> c | >, d -> < | e -> f | > | >, {2}]

Out[1]= < | a -> < | b -> h[c] | >, d -> < | e -> h[f] | > | >

	

作用到 Association 的几个层中：

In[1]:= Map[h, < | a -> < | b -> c | >, d -> {< | e -> f | >} | >, {1, 3}]

Out[1]= < | a -> h[< | b -> h[c] | >], d -> h[{h[< | e -> h[f] | >]}] | >