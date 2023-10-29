# 《DOTS之路系列教程》之代码笔记


---
title: 《DOTS之路系列教程》之代码笔记
authors: Ethan Lin
year:
tags:
  - 日期/2023-04-18 
  - 类型/笔记 
  - 内容/DOTS 
  - 类型/AI问答笔记 
---





> [!attention]
> 以下由AI回答，不保证正确性！





# Entities


> [!question] 
> `Assets/EntitiesTutorials/Lesson3/Scripts/Systems/CubeGenerateByPrefabSystem.cs`

> [!summary] 
> 这段代码定义了一个名为 "`CubeGenerateByPrefabSystem`" 的部分结构体，它实现了 `Unity.Entities.ISystem` 接口。该结构体的实例在 `UpdateInGroup` 属性指定的 `CreateEntitiesByPrefabSystemGroup` 组中运行。
> 
> 在 `OnCreate` 方法中，系统注册了一个 `CubeGeneratorByPrefab` 组件，以便在更新时进行查询。
> 
> 在 `OnUpdate` 方法中，系统获取了一个名为 "`CubeGeneratorByPrefab`" 的单例组件，并使用 `EntityManager.Instantiate` 方法生成了指定数量的实体。对于每个实体，系统添加了一个 `RotateAndMoveSpeed` 组件，以及一个 `LocalTransform` 组件，并使用计数器 `count` 控制了它们的旋转和移动速度以及位置。
> 
> 最后，系统关闭了自身，因为该系统只需要在启动时运行一次。

> [!question] 
> 为什么不在`OnCreate`方法里实例化生成器`generator`呢？我的理解是，如果再`OnCreate`方法里实例化生成器，那么只需要运行一次呀?


您的理解是正确的，将生成器实例化放到 `OnCreate` 方法中，可以保证系统只在启动时运行一次，并且只会实例化一次生成器。

实例化生成器的代码可以放在 `OnCreate` 方法中，如下所示：

```C#
[BurstCompile]
public void OnCreate(ref SystemState state)
{
    var generatorEntity = state.EntityManager.CreateEntity(typeof(CubeGeneratorByPrefab));
    state.EntityManager.SetComponentData(generatorEntity, new CubeGeneratorByPrefab
    {
        cubeCount = 100,
        cubeEntityProtoType = prefabEntity,
    });
}
```

在这个例子中，我们假设 `CubeGeneratorByPrefab` 是一个带有数据的组件，用于指定生成器的参数，例如生成的实体数量和预制件实体的原型等。我们首先使用 `EntityManager.CreateEntity` 方法创建一个实体，并将 `CubeGeneratorByPrefab` 组件添加到实体上。然后，我们使用 `EntityManager.SetComponentData` 方法来设置组件的数据。

值得注意的是，为了在 `OnUpdate` 方法中访问到生成器，我们需要使用 `SystemAPI.GetSingleton<T>()` 方法来获取单例组件，而不是使用 `state.EntityManager.GetComponentData<T>()` 方法。因为 `OnUpdate` 方法可能会在多个线程中同时运行，而使用 `SystemAPI.GetSingleton<T>()` 方法可以确保我们访问的是同一个单例实例。



> [!question]
> `Assets/EntitiesTutorials/Common/Scripts/Singleton.cs`



这段代码定义了一个泛型单例类 `Singleton<T>`，`T` 是 `MonoBehaviour` 的子类。

在 `Singleton<T>` 类中，我们定义了一个静态的 `instance` 变量，它表示泛型类型 `T` 的唯一实例。我们还定义了一个公共的静态属性 `Instance`，用于获取 `instance` 变量的值。

在 `Instance` 属性的 `getter` 方法中，我们首先检查 `instance` 是否为 `null`，如果是，则尝试从场景中查找 `T` 的实例。如果找不到，则创建一个新的 `GameObject`，并将 `T` 的实例添加到该 `GameObject` 上。

在 `Awake` 方法中，我们检查 `instance` 是否为 `null`。如果 `instance` 为 `null`，则将当前实例作为唯一实例，并调用 `DontDestroyOnLoad` 方法以确保实例在场景切换时不被销毁。否则，我们销毁当前实例，以确保只有一个实例存在。

使用 `Singleton<T>` 类时，我们只需要将其作为 `T` 的基类，并通过 `Singleton<T>.Instance` 属性来访问 `T` 的唯一实例。例如，我们可以通过以下方式创建一个名为 `GameManager` 的单例类：

```C#
public class GameManager : Singleton<GameManager>
{
    // ...
}
```

在代码中，我们使用了 `MonoBehaviour` 类的一些常见方法和属性，例如 `FindObjectOfType<T>` 方法和 `DontDestroyOnLoad` 方法等。`Singleton<T>` 类是一种常见的实现单例模式的方式，它适用于 Unity 引擎中需要使用单例的场景。
