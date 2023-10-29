# 因果推理工具包DoWhy


---
title: 因果推理工具包DoWhy
authors: Ethan Lin
year:
tags:
  - 内容/因果推理 
---


tags: #内容/工具 

[因果推理工具包DoWhy线上文档](https://microsoft.github.io/dowhy/)

#### 相关介绍：

因果推断近些年来变的越来越热，然而根据我近期学习的过程来看，实际上[causal inference](https://www.zhihu.com/search?q=causal+inference&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1806691116%7D)还是很难的一个方向，并且现在还是快速突破的方向。DoWhy这个名字的灵感来自Judea Pearl在因果推理中的do-calculus。

  

DoWhy的设计有两个重要的指导原则：明确因果假设，并测试[估计值](https://www.zhihu.com/search?q=%E4%BC%B0%E8%AE%A1%E5%80%BC&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1806691116%7D)对违背这些假设的鲁棒性。

首先，DoWhy区分identification和estimation。[因果效应](https://www.zhihu.com/search?q=%E5%9B%A0%E6%9E%9C%E6%95%88%E5%BA%94&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A1806691116%7D)的Identification涉及对数据生成过程进行假设，并将反事实表达式转换为指定目标的estimand，estimation只是从数据估计目标estimand的统计问题。

其次，一旦做出假设，DoWhy将提供鲁棒性测试和敏感性检查，以测试所获得估计的可靠性。

  
  
> 作者：会飞的鲲  
> 链接：https://www.zhihu.com/question/283897078/answer/1806691116  
> 来源：知乎  
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。