---
title: AI-Economist工具
authors: Ethan Lin
year:
tags:
  - 类型/笔记 
  - 内容/多智能体强化学习 
  - 内容/程序 
  - 项目/SystemicRisk 
  - 用途/借鉴思路 
---


# AI-Economist工具




# 一些概念：

- 组件`Components`：组件封装特定的交互和动态，以实现场景的行为。支持即插即用的方法构建经济模拟。
- 实体`Entities`：实体包括经济模拟中的代理可以与实体交互。
- 主体`Agents`：每个主体是一个独立单元，可以通过挂载的组件，执行相关的操作，与其他主体互动于环境中。
- 场景`Scenarios`：包括由世界地图、资源、布局好的agents等构成的场景（可以被称为一系列完整的实验组）；





# 核心文件结构：

- `foundation`：基础和核心算法；
	- `agents`：设计基本的agents。默认包含普通的移动agents类`mobiles`、规划者`planners`；
	- `base`：设计各种基类、世界等；
	- `components`：包含各种设计好的组件；
	- `entities`：包含各种实体。默认有3组实体：`landmarks`、`endogenous`、`resources`。
	- `scenarios`：包含各种预设场景；
	  - `utils`：包含一些工具；
	    - `rewards.py`：计算agent之效用；
	- `utils`：实用工具；



# 变量结构

- `env`：
  
  - 初始化之参数：
  
    ```python
    components=None,
    n_agents=None,
    world_size=None,
    episode_length=1000,
    multi_action_mode_agents=False,
    multi_action_mode_planner=True,
    flatten_observations=True,
    flatten_masks=True,
    allow_observation_scaling=True,
    dense_log_frequency=None,
    world_dense_log_frequency=50,
    collate_agent_step_and_reset_data=False,
    seed=None,
    ```
  
  - 
  
  - TODO
  
- `base_agent`：来自`ai_economist/foundation/base/base_agent.py`；

  - `action`：行为之字典；
  - `action_dim`：行为之维度；
  - `_action_names`：行为之名称；
  - `_multi_action_dict`：多重行为之字典；
  - `_unique_actions`：单一行为数；
  - `_total_actions`：总行为数；
  - `state`： 状态，记录位置，持有的资源情况`dict(loc=[0, 0], inventory={}, escrow={}, endogenous={})`；

- `base_env`：来自`ai_economist/foundation/base/base_env.py`

  - 初始化：
  
    ```python
    def __init__(
            self,
            components=None,  # 组件
            n_agents=None,  # agent数量
            world_size=None,  # 世界大小
            episode_length=1000,  # 回合长度
            multi_action_mode_agents=False,  # 普通agent之多重行为模式
            multi_action_mode_planner=True,  # 规划者agent之多重行为模式
            flatten_observations=True,  # 是否展开所得到的观察
            flatten_masks=True,  # 是否展开掩码
            allow_observation_scaling=True,  # 是否允许观察缩放
            dense_log_frequency=None,  # 记录日志频率
            world_dense_log_frequency=50,  # 世界纪录日志频率
            collate_agent_step_and_reset_data=False,  # 是否收集agent之步进信息并且重置数据
            seed=None,  # 随机种子
    ):
    ```
  
    ```python
    self.world = World(
        self.world_size,  # 世界尺寸
        self.n_agents,  # agent数量
        self.resources,  # 资源众
        self.landmarks,  # 标记众
        self.multi_action_mode_agents,  # 普通agent之多重行为模式
        self.multi_action_mode_planner,  # 规划者agent之多重行为模式
    )
    ```
  
    ```python
    component_cls = component_registry.get(component_name)  # 注册组件，获得组件相关的参数
    ```
  
  

- `component_cls`，来自`ai_economist/foundation/base/.py`：

  - `world`
  - `episode_length`
  - `inv_scale`
  - `shofthand`

- `components`关键字：

  需要以元组嵌套字典形式。例如：

  ```python
  'components': [
      # (1) Building houses
      ('Build', {'skill_dist': "pareto", 'payment_max_skill_multiplier': 3}),
      # (2) Trading collectible resources
      ('ContinuousDoubleAuction', {'max_num_orders': 5}),
      # (3) Movement and resource collection
      ('Gather', {}),
  ],
  ```
  
  相关的字段：
  
  `episode_length`
  `inv_scale`
  `resources`
  `landmarks`
  `endogenous`
  `all_agents `
  `previou_episode_metrics`
  `metrics `
  `components`
  `dense_log`
  `replay_log`
  `previous_episode_dense_log`
  `previous_episode_replay_log`
  `generate_rewards`




# 关系
`Components`相当于一个中介，实现互动之于各实体`Entities`与环境`env`。

# 运作流程：
- [ ] TODO AI-Economist之运作流程
