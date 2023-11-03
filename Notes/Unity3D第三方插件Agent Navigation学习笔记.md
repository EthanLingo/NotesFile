---
title: Unity3D第三方插件Agent Navigation学习笔记
authors: Ethan Lin
year:
tags:
  - #类型/笔记 
  - #类型/AI问答笔记 
---


# Unity3D第三方插件Agent Navigation学习笔记




# 相关资源

官方文档：[Agents Navigation](https://lukaschod.github.io/agents-navigation-docs/manual/)



# 基础知识

## 多种 agent 组件之执行顺序

if you have agents that have components: `Agent`, `AgentBody`, `AgentShape`, `AgentSteering`, `AgentSonarAvoid`, `AgentCollider`, `NavMeshPath` and `NavMeshNode`.

Execution logic would be:

1. `NavMeshPath` would request new path into `DynamicBuffer<NavMeshNode>`.
2. `AgentSteering` would compute steering direction into `AgentBody`.
3. `DynamicBuffer<NavMeshNode>` would modify steering direction of `AgentBody` by following path locations.
4. `AgentSonarAvoid` would modify steering direction of `AgentBody` to account for avoiding nearby `Agents`.
5. `AgentSteering` and `AgentBody` would be used to translate `Agent` position.
6. `NavMeshPath` would be used to correct position to make sure `Agent` is still in Nav Mesh.


# AI问答系列

> [!attention]
> 以下由AI回答，不保证正确性！




#### `Execute`与`Entities.WithReadOnly().ForEach(){}.Schedule()`

> [!question] 
> 这两段代码`ProjectDawn.Navigation/Flock/AgentFlockSystem.cs`与`ProjectDawn.Navigation/Flock/FlockGroupSystem.cs`中，一个用了`Execute`方法，另一个在Update方法里用了`Entities.WithReadOnly().ForEach(){}.Schedule()`，二者有什么区别吗？
> 

`Execute`方法是用于执行单个实体的逻辑，而`Entities.WithReadOnly().ForEach(){}.Schedule()`是用于并行处理多个实体的逻辑。在这两段代码中，它们的用途和作用不同。

在第一个代码中，`Execute`方法是`IJobEntity`接口的一部分，它被用于处理实现该接口的群组系统中的每个实体。该系统使用`ScheduleParallel()`命令来并行执行这些`Execute`方法。因此，`Execute`方法是用于并行处理多个实体。

在第二个代码中，`Entities.WithReadOnly().ForEach(){}.Schedule()`是用于并行处理多个实体的逻辑。`WithReadOnly()`方法用于指定只读数据，`ForEach()`方法用于定义要在每个实体上执行的操作。最后，`Schedule()`方法用于将该操作安排在Job系统中进行处理。因此，`Entities.WithReadOnly().ForEach(){}.Schedule()`也是用于并行处理多个实体。

总的来说，这两段代码都是用于并行处理实体的逻辑，只不过前者是在群组系统中实现的，后者是在Job系统中实现的。


#### `IComponentData`与`IBufferElementData`

> [!question] 
> `ProjectDawn.Navigation/Flock/FlockGroup.cs`之`FlockGroup : IComponentData`与`FlockEntity : IBufferElementData`区别？


`FlockGroup`和`FlockEntity`是两种不同的结构体。`FlockGroup`是一个实现了`IComponentData`接口的结构体，用于描述一群鸟的群体行为，包括领导者实体、群体半径、凝聚力和对齐力的权重、平均位置和方向等信息。`IComponentData`是Unity ECS（Entity Component System）中组件数据的基础接口，用于描述实体的属性和状态。

相比之下，`FlockEntity`是一个实现了`IBufferElementData`接口的结构体，用于描述一只鸟的实体信息，包括实体的ID。`IBufferElementData`是Unity ECS中动态缓冲区的接口，用于描述具有相同类型的多个实体的数据。

因此，`FlockGroup`和`FlockEntity`是不同的结构体，分别用于描述群体行为和单个实体的信息。在一个群体中，可以有多个`FlockEntity`实体，它们共享同一个`FlockGroup`组件。
