# PettingZoo学习笔记


tags: #日期/2022-11-01 #类型/笔记 #内容/多智能体强化学习 #内容/程序 #项目/EntelechySystem #用途/借鉴思路 



# 一些概念

 

# 一些文件结构



`core.py`：来自`pettingzoo/mpe/_mpe_utils/core.py`。包括内容：

- `EntityState`：物体状态。参数：
  位置`p_pos`、速度`p_vel`。
- `AgentState`：主体状态。继承`EntityState`。参数：
  通讯状态`c`；
- `Entity`：物体。主要参数：
  静止`movable=False`、可碰撞`collide=True`、物体之状态`state=EntityState()`、行为集合`action=Action()`、要执行的脚本行为`action_callback`；

- `Agent`：主体。继承`Entity`。主要参数如下：
  可动`movable=True`、可通讯`silent=False`、目明`blind=False`、物理行为噪声量`u_noise`、通讯行为噪声量`c_noise`、可控制的半径`u_range`、多主体之状态`state=AgentState()`、行为集合`action=Action()`、要执行的脚本行为`action_callback`。这里若`action_callback=True`则该主体众称为`scripted_agents`是由world脚本所控制，否则称为policy_agents，其由外部策略所控制。
- `Action`：行为。主要参数如下：
  物理行为`u`、通讯行为`c`

- `World`：多主体世界相关参数集。主要参数如下：
  主体列表`agents`、标记物列表`landmarks`、通讯频道维数、空间维数、颜色维数、步长值、阻尼系数、接触力、接触面积
- 
