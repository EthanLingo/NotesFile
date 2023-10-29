# R与Python第三方工具包对比


---
title: R与Python第三方工具包对比
authors: Ethan Lin
year:
tags:
  - 日期/2023-03-05 
  - 类型/笔记 
  - 类型/转载 
---



> 来源：[数据分析：R与Python怎么选？ - 知乎](https://zhuanlan.zhihu.com/p/272100187#:~:text=1%20在%20深度学习%20领域，例如自然语言处理、图像识别等%E3%80%82%20相对于R，Python对GPU有更好的支持，虽然R也支持KERAS运算，但是实现效率较低、成本较高，你可以想象这样的一个场景，当你使用R做深度学习时，经历一番搜索和研究，刚把需要的环境搭建好，人家用Python的已经可以提交项目结果了%E3%80%82%20...%202%20在,统计分析%20领域，R的综合表现更优于Python%E3%80%82%20...%204%20在%20数据可视化%20领域，虽然Python有一些很好的可视化程序库，例如Seaborn、Bokeh和Pygal，但与R对比，在Python中进行可视化有些复杂，可调节的参数较少，且图表样式的控制会更麻烦一些%E3%80%82%20)





R和Python有丰富的第三包可供加载和框架选择，可以很好帮助分析师、研究员以及开发员提高工作效率：

| 功能名称           | R语言                                                        | Python语言                                   |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------- |
| 爬虫               | Rvest、Rcurl、httr、XML、Rwebdriver                          | Urllib、requests、bs4、selenium、splash      |
| 数据读取           | Openxlsx、utils、readxl、xlsx、xlsx2、data.table             | pandas                                       |
| 数据加工(ETL)      | Plyr、dplyr、reshape2、caret、tidyr、mice、stringr           | numpy、pandas、sklearn、re                   |
| 数据可视化         | ggplot2、ggmap、lattice、gganimate、leaflet、REmap、plotly、rCharts、animation | Matplotlib、seaboen、bokeh、pyecharts、Pygal |
| 统计分析、回归分析 | Stats、tseries、lmtest、nlme                                 | statsmodels、scipy                           |
| 机器学习           | Stats、glmnet                                                | statsmodels、scipy                           |
| 深度学习           | Keras、MXNetR、darch、deepnet、H2O、deepr                    | TensorFlow、Keras、Pytorch、Theano、MXNET    |

通过加载不同的功能包，用户可以在用少量的代码下，快速实现算法逻辑：

| 算法名称   | R语言                       | Python语言           |
| ---------- | --------------------------- | -------------------- |
| 决策树算法 | Repart、party、C50、RWeka   | sklearn              |
| 集成算法   | adabag、randomForest        | sklearn、xgboost     |
| 贝叶斯算法 | klaR                        | sklearn              |
| K邻近算法  | Stats、kknn                 | sklearn              |
| 支持向量机 | Kernlab、e1071              | sklearn              |
| 神经网络   | RSNNS、neuralnet、nnet      | Neurolab、tensorflow |
| 聚类算法   | stats、Nbclust、fpc、mclust | sklearn              |
| 关联规则   | arules                      | mlxtend              |