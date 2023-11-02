---
title: abcEcnomics工具
authors: Ethan Lin
year: 2022-11-21 
tags:
  - 日期/2022-11-21 
  - 类型/笔记 
  - 内容/经济金融 
  - 内容/多主体建模 
---


# abcEcnomics工具







# 资源

相关的平台：

教程类：

[abc-Economics-examples官方教程](https://github.com/AB-CE/examples.git)



# 使用方法


# 一些概念

# 官方介绍





# 使用案例



## 如果我有很多代理人，那么可以用向量的方法批量快速初始化吗？



是的，你可以使用向量方法来批量快速初始化代理人。AB-CE中提供了多种向量方法，包括使用numpy数组、pandas数据框等。

下面是一个使用numpy数组的示例：

```python
import numpy as np
from abce import Simulation
from abce.agents import Agent

class MyAgent(Agent):
    def init(self, simulation_parameters, agent_parameters):
        self.name = agent_parameters['name']
        self.wealth = agent_parameters['wealth']

    def go(self):
        pass

class MySimulation(Simulation):
    def add_objects(self):
        # 生成100个代理人
        agent_params = np.array([
            {'name': f'agent{i}', 'wealth': i} for i in range(100)
        ])
        self.agents['my_agent'] = MyAgent.from_array(
            agent_params, self, agent_parameters={}, agent_options={}
        )

    def round(self):
        pass

sim = MySimulation()
sim.run()

```

在这个示例中，我们定义了一个MyAgent代理人，并使用numpy数组生成了100个代理人。在add_objects方法中，我们使用MyAgent.from_array方法，将代理人参数数组传递给它，它会根据数组中的每一行创建一个代理人，并将每行的字典作为参数传递给MyAgent的init方法。此外，我们还传递了一个空字典作为agent_parameters参数，以及一个空字典作为agent_options参数。

这样一来，我们就可以使用向量方法来批量快速初始化代理人了。这种方法可以大大减少代码量和时间，特别是当代理人数量较多时。




