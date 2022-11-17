# PettingZoo学习笔记


tags: #日期/2022-11-01 #类型/笔记 #内容/多智能体强化学习 #内容/程序 #项目/EntelechySystem #用途/借鉴思路 



# 一些概念

 

# 一些文件结构



`core.py`：来自`pettingzoo/mpe/_mpe_utils/core.py`。包括内容：

- `Agent`：多主体。主要参数如下：
  是否可动`movable`、是否哑`silent`、是否盲`blind`、物理行为噪声量`u_noise`、通讯行为噪声量`c_noise`、可控制的半径`u_range`、多主体之状态`state=AgentState()`、行为集合`action=Action()`、要执行的脚本行为`action_callback`；

- `World`：多主体世界相关参数集。主要参数如下：
  主体列表`agents`、标记物列表`landmarks`、信息交流频道维数、空间维数、颜色维数、步长值、阻尼系数、接触力、接触面积
