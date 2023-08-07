# DOTS学习笔记



tags: #日期/2023-04-22 #类型/AI问答笔记 #内容/DOTS 



> [!attention]
> 以下由AI回答，有些地方掺入了个人笔记与理解。仅供参考，不保证正确性！


# 手写笔记系列

## 查询

#### ComponentLookup

对于方法`ComponentLookup.TryGetComponent()`。首先新建一个针对查询某个组件之实例`AAAComponentLookup`，然后调用该实例，使用该方法`TryGetComponent`。该方法之形参1是某个要查询的具体的实体；形参2用`out`标记，将查询到的结果传给该形参。

# AI问答系列

# 基础知识问答

## Entities实体


#### `Entities.With` 系列的主要方法


> [!question] 
> `Entities.With` 系列的主要方法及其区别？


1.  `WithAll`: 这个方法用于选择具有所有指定组件的实体。它接受一个或多个组件类型作为参数，并返回一个过滤器，您可以使用该过滤器来选择具有所有指定组件的实体。例如，`Entities.WithAll(typeof(Position), typeof(Velocity))` 选择所有具有 `Position` 和 `Velocity` 组件的实体。
2.  `WithAny`: 这个方法用于选择具有任何指定组件的实体。它接受一个或多个组件类型作为参数，并返回一个过滤器，您可以使用该过滤器来选择具有任何指定组件的实体。例如，`Entities.WithAny(typeof(Damage), typeof(Health))` 选择所有具有 `Damage` 或 `Health` 组件的实体。
3.  `WithNone`: 这个方法用于选择没有指定组件的实体。它接受一个或多个组件类型作为参数，并返回一个过滤器，您可以使用该过滤器来选择没有指定组件的实体。例如，`Entities.WithNone(typeof(Dead))` 选择所有没有 `Dead` 组件的实体。
4.  `With`: 这个方法用于选择具有指定组件的实体。它接受一个组件类型和一个组件类型的值作为参数，并返回一个过滤器，您可以使用该过滤器来选择具有指定组件和值的实体。例如，`Entities.With(typeof(Health), new Health { Value = 100 })` 选择所有具有 `Health` 组件并且值为 100 的实体。
5. `WithReadOnly` 方法接受一个实体查询过滤器作为参数，并返回一个只读实体和组件数据视图。只读视图仅允许读取实体和组件数据，而不允许修改它们。这使得作业可以在不锁定共享数据的情况下并行执行，从而提高了性能。
> [!example]
```C#
using Unity.Entities;

public struct Position : IComponentData
{
    public float x;
    public float y;
    public float z;
}

public class MyJobSystem : SystemBase
{
    protected override void OnUpdate()
    {
        Entities
            .WithAll<Position>()
            .WithReadOnly(this)
            .ForEach((ref Position position) =>
            {
                // 读取实体和组件数据
                float x = position.x;
                float y = position.y;
                float z = position.z;

                // 在作业中不允许修改实体和组件数据
                // position.x = 0;
                // position.y = 0;
                // position.z = 0;
            })
            .Schedule();
    }
}
```

总之，这些方法的区别在于它们所选择的实体的组件和属性。

#### TransformUsageFlags

> [!question] 
> `TransformUsageFlags`有哪些枚举值？分别表示什么意思？

`TransformUsageFlags`是一个枚举，它定义了在Unity ECS中用于指定实体转换应该如何被应用的标志。以下是该枚举的所有值以及它们的含义：

- `None`: 不应用任何转换标志。
- `Position`: 应用实体的位置转换。
- `Rotation`: 应用实体的旋转转换。
- `Scale`: 应用实体的缩放转换。
- `ScaleXY`: 应用实体的X轴和Y轴缩放转换，但不应用Z轴缩放转换。
- `ScaleXZ`: 应用实体的X轴和Z轴缩放转换，但不应用Y轴缩放转换。
- `ScaleYZ`: 应用实体的Y轴和Z轴缩放转换，但不应用X轴缩放转换。
- `ScaleXYZ`: 应用实体的X轴、Y轴和Z轴缩放转换。

这些标志可以通过按位或（`|`）操作组合在一起，以表示需要应用的转换类型。例如，将`Position`和`Rotation`组合在一起，可以将实体的位置和旋转应用到它的转换中：

```
var flags = TransformUsageFlags.Position | TransformUsageFlags.Rotation;
var entity = GetEntity(flags);
```


## Query


#### 辨析`configQuery.GetSingleton`、`state.EntityManager.GetComponentObject`

> [!question]
> `configQuery.GetSingleton<Config>();`与` state.EntityManager.GetComponentObject<Managed>(state.SystemHandle);`有什么不同？

`configQuery.GetSingleton<Config>()`和`state.EntityManager.GetComponentObject<Managed>(state.SystemHandle)`这两个函数在使用上有很大的不同。

首先，`configQuery.GetSingleton<Config>()`是从一个EntityQuery中获取一个指定组件类型的单例组件，它返回的是一个组件类型的实例。而`state.EntityManager.GetComponentObject<Managed>(state.SystemHandle)`是从实体管理器中获取一个指定组件类型的组件，它返回的是组件所在的Unity对象。

其次，这两个函数的使用场景也不同。`configQuery.GetSingleton<Config>()`通常用于获取一个单例组件，比如游戏中的规则配置。而`state.EntityManager.GetComponentObject<Managed>(state.SystemHandle)`通常用于获取一个实体的Unity对象，以便在Unity中进行操作。比如，如果需要在实体上添加一个脚本组件，就可以使用这个函数来获取实体所在的Unity对象，并在Unity对象上添加脚本组件。

最后，这两个函数的调用方式也不同。`configQuery.GetSingleton<Config>()`是在EntityQuery的上下文中调用的，需要先创建一个EntityQuery对象，然后使用该对象的方法来获取组件。而`state.EntityManager.GetComponentObject<Managed>(state.SystemHandle)`是在实体管理器中直接调用的，可以直接从实体管理器中获取组件。

总之，`configQuery.GetSingleton<Config>()`和`state.EntityManager.GetComponentObject<Managed>(state.SystemHandle)`这两个函数在使用上有很大的不同。前者是从EntityQuery中获取单例组件实例，后者是从实体管理器中获取组件所在的Unity对象。它们的使用场景和调用方式也不同。

### 查询条件检索方法 `WithAll` 等方法

`WithAll`方法：查询同时拥有指定组件的实体。相当于求交集；

`WithAny`方法：查询具有任何一个指定组件的实体。相当于求并集；

`Without`方法：查询不拥有指定组件的实体。相当于求并集然后取反；

`WithNone`方法：查询不拥有指定任何一个组件的实体。相当于求交集然后取反；


## System系统



#### `state.Dependency`


> [!question] 
> `state.Dependency`是什么？


`state.Dependency`是一个`JobHandle`类型的变量，用于表示该系统的依赖关系。在Unity ECS框架中，每个系统都可以拥有一个或多个依赖关系，用于确保系统在执行时满足一定的执行顺序。当一个系统完成执行后，它会返回一个`JobHandle`类型的值，表示它的执行状态。其他系统可以使用这个值作为它们的依赖关系，以确保它们在当前系统执行完成之前不会开始执行。因此，在上述代码中，当`CreateGenerateAgentEntityJob`方法创建并调度执行作业后，将作业返回的`JobHandle`值赋值给`state.Dependency`变量，表示该系统在执行时依赖于这个作业的完成状态。


## `Flags`标记


#### `RequireMatchingQueriesForUpdate`

> [!question]
> `RequireMatchingQueriesForUpdate` 是什么？


`RequireMatchingQueriesForUpdate`是一个用于确定系统是否应该运行的标志。当一个系统有这个标志时，它只会在与其查询完全匹配的实体上运行，否则它将被跳过，不会执行任何操作。

具体地说，每个ECS系统都通过一个查询（Query）来确定它应该处理哪些实体。该查询定义了系统应该包含哪些组件以及它们的值。`RequireMatchingQueriesForUpdate`标志告诉系统只有在所有实体的组件与查询完全匹配时才应该运行。否则，系统将跳过该帧的更新。

这个标志对于优化性能非常有用，因为它可以避免系统处理不必要的实体。例如，如果您有一个处理敌人AI的系统，当这个标志被启用时，它只会在那些具有所有必需组件（如“位置”和“生命值”）的敌人实体上运行。这样，系统就不会浪费时间在没有必要组件的实体上进行计算。

需要注意的是，使用`RequireMatchingQueriesForUpdate`标志可能会增加代码复杂度，因为您需要确保所有实体都具有必需的组件。但是，这个标志在正确使用时可以显著提高系统性能。


#### `RequireForUpdate`

> [!question] 
> `RequireForUpdate` 是什么？


`RequireForUpdate` 是 Unity DOTS 中的一个标记（Flag），用于控制系统（System）在何时执行更新。

在 Unity DOTS 中，系统可以通过实现 `ISystemBase` 接口来定义自己的逻辑。系统在每一帧中被调用多次，以更新游戏状态。但有些情况下，系统不需要在每一帧都更新，例如只在某些条件满足时才需要执行更新操作。这时，可以使用 `RequireForUpdate` 标记来控制系统的更新时机。

具体来说，系统可以在 `OnCreate()` 方法中调用 `World.GetOrCreateSystem<EntityManager>().AddEntityToEntityQueries(this, requireForUpdate)` 方法来将自己添加到需要更新的系统列表中。然后，在需要更新时可以调用 `EntityManager.AddComponentData()` 方法向特定的实体（`Entity`）添加 `RequireForUpdate` 标记，以通知系统在下一帧中执行更新操作。

需要注意的是，`RequireForUpdate` 标记只有在实体发生变化时才会触发更新。因此，如果需要在某些条件满足时立即更新系统，可以使用 `World.EntityManager.CompleteAllJobs()` 方法强制完成所有作业（Jobs），以确保 `RequireForUpdate` 标记在下一帧中得到更新。

总之，`RequireForUpdate` 标记可以帮助开发者更加灵活地控制系统的更新时机，从而提高游戏的性能和效率。 是 Unity DOTS 中的一个标记（Flag），用于控制系统（System）在何时执行更新。

在 Unity DOTS 中，系统可以通过实现 ISystemBase 接口来定义自己的逻辑。系统在每一帧中被调用多次，以更新游戏状态。但有些情况下，系统不需要在每一帧都更新，例如只在某些条件满足时才需要执行更新操作。这时，可以使用 `RequireForUpdate` 标记来控制系统的更新时机。

具体来说，系统可以在 `OnCreate()` 方法中调用 `World.GetOrCreateSystem<EntityManager>().AddEntityToEntityQueries(this, requireForUpdate)` 方法来将自己添加到需要更新的系统列表中。然后，在需要更新时可以调用 `EntityManager.AddComponentData()` 方法向特定的实体（Entity）添加 `RequireForUpdate` 标记，以通知系统在下一帧中执行更新操作。

需要注意的是，`RequireForUpdate` 标记只有在实体发生变化时才会触发更新。因此，如果需要在某些条件满足时立即更新系统，可以使用 `World.EntityManager.CompleteAllJobs()` 方法强制完成所有作业（Jobs），以确保 `RequireForUpdate` 标记在下一帧中得到更新。

总之，`RequireForUpdate` 标记可以帮助开发者更加灵活地控制系统的更新时机，从而提高游戏的性能和效率。



## Physics

#### PhysicsStep

`PhysicsStep`是Unity.Entities中的一个组件，用于指定物理世界的模拟参数。

在Unity.Entities中，组件是数据的基本单位，用于存储实体的状态和属性。`PhysicsStep`是一种组件，它包含了物理世界模拟的各种参数，例如模拟步长、求解器迭代次数、重力等。通过在物理世界的实体中添加`PhysicsStep`组件，可以控制物理世界的模拟参数，从而实现更加精确的物理模拟。

`PhysicsStep`组件包含以下属性：
- `SolverIterationCount`：求解器迭代次数。
- `SolverStabilizationHeuristicSettings`：求解器稳定性启发式设置。
- `Gravity`：物理世界的重力。
- `SimulationType`：物理模拟类型，默认为`UnityPhysics`。
- `SimulationType`属性指定了物理模拟的类型，可以是`UnityPhysics`或`HavokPhysics`。`SolverIterationCount`属性指定了求解器的迭代次数，`SolverStabilizationHeuristicSettings`属性则指定了求解器的稳定性启发式设置。`Gravity`属性指定了物理世界的重力。

总之，`PhysicsStep`是一种组件，用于指定物理世界的模拟参数。使用`PhysicsStep`组件可以控制物理世界的模拟参数，从而实现更加精确的物理模拟。


## 未归类的问答


#### `EntityCommandBuffer`

> [!question] 
> `EntityCommandBuffer` 是什么？


`EntityCommandBuffer` 是 Unity DOTS 中的一个用于管理实体（Entity）和组件（Component）的缓冲区，可以在 Jobs 中用于高效地修改实体和组件。

在 Unity DOTS 中，Jobs 是一种在多线程环境下执行的任务，可以用于高效地处理大量的数据。但是，由于实体和组件的修改必须在主线程中进行，因此在 Jobs 中直接修改实体和组件会导致错误。

`EntityCommandBuffer` 能够解决这个问题。它是一个缓冲区，可以在 Jobs 中记录修改实体和组件的指令，而不是直接执行这些操作。在 Jobs 执行完成后，可以将 `EntityCommandBuffer` 中记录的指令应用到实体和组件上，从而实现对实体和组件的修改。

具体来说，`EntityCommandBuffer` 可以用于添加、移除和修改实体和组件等操作。例如，可以使用 `EntityCommandBuffer.CreateEntity()` 方法创建新的实体，使用 `EntityCommandBuffer.AddComponent()` 方法向实体添加组件，使用 `EntityCommandBuffer.RemoveComponent()` 方法移除实体的组件等。在 Jobs 执行完成后，可以调用 `EntityCommandBuffer.Playback()` 方法将记录的指令应用到实体和组件上。

需要注意的是，`EntityCommandBuffer` 仅能在 Jobs 中使用，不能在主线程中使用。此外，`EntityCommandBuffer` 在执行 `PlayBack()` 方法后会被清空，因此需要在每次使用前重新创建。

总之，`EntityCommandBuffer` 是 Unity DOTS 中一个非常有用的工具，可以帮助开发者在 Jobs 中高效地修改实体和组件，从而提高游戏的性能和效率。


#### `Allocator`

> [!question] 
> 什么是 `Allocator`？

`Allocator` 是 Unity 中用于分配和管理内存的一个系统，它可以帮助开发者在游戏中高效地使用内存。

在 Unity 中，`Allocator` 提供了几种不同的内存分配器，可以根据不同的使用场景选择合适的分配器。以下是常用的 `Allocator`：

1.  `Allocator.Temp`：用于在当前帧中分配临时内存空间，该内存空间会在当前帧结束时自动释放。
    
2.  `Allocator.TempJob`：用于在 Jobs 中临时分配内存空间，该内存空间会在 Jobs 执行完成后自动释放。
    
3.  `Allocator.Persistent`：用于分配游戏中的持久化内存空间，该内存空间会一直存在直到手动释放。
    
4.  `Allocator.None`：不分配任何内存空间，用于在不需要分配内存的情况下创建 `NativeArray` 或 `NativeHashMap` 等数据结构。
    

使用 `Allocator` 可以帮助开发者在游戏中更加高效地分配和管理内存。例如，在 Jobs 中使用 `Allocator.TempJob` 分配临时内存空间，可以避免多线程访问同一内存空间的问题，从而提高游戏的性能和效率。

需要注意的是，`Allocator` 分配的内存空间需要手动释放，否则可能会导致内存泄漏和游戏崩溃。因此，开发者需要在使用完内存空间后及时调用相关的释放方法，例如 `NativeArray.Dispose()` 或 `NativeHashMap.Dispose()` 等。

总之，`Allocator` 是 Unity 中一个非常重要的内存管理系统，可以帮助开发者更加高效地使用内存，从而提高游戏的性能和效率。


## DOTS 与 OOP 适应问答

### 关于复用、扩展



#### 如何传递参数以便于复用

> [!question]
> 传统的OOP中，为其他项目提供的通用功能，可以通过函数或者类传递属性或者参数值实现。那么在DOTS中，有没有类似的做法呢？例如我实现了一个系统【随机生成实体】。该系统有一些参数：【生成数量】、【生成位置】、【生成范围】、【散布的分布】等。如果在OOP的编程模式中，我可以设计一个函数，然后把这些参数用函数形参提供接口，给其他项目代入具体参数使用。那么在DOTS中，有没有类似的办法呢？


在DOTS中，您可以通过创建一个包含参数的组件来实现类似的功能。以下是一个示例，说明如何在DOTS中为随机生成实体的系统提供参数：

1. 首先，创建一个包含参数的组件：

```csharp
public struct RandomSpawnConfig : IComponentData
{
    public int SpawnCount;
    public float3 SpawnPosition;
    public float SpawnRange;
    // 其他参数，例如散布的分布
}
```

2. 在随机生成实体的系统中，从`RandomSpawnConfig`组件中获取参数：

```csharp
public class RandomSpawnSystem : SystemBase
{
    protected override void OnUpdate()
    {
        // 获取RandomSpawnConfig组件
        var config = GetSingleton<RandomSpawnConfig>();

        // 使用参数生成实体
        // ...
    }
}
```

3. 在其他项目中，您可以创建一个实体并添加`RandomSpawnConfig`组件，然后设置参数：

```csharp
var entityManager = World.DefaultGameObjectInjectionWorld.EntityManager;
var configEntity = entityManager.CreateEntity();
entityManager.AddComponentData(configEntity, new RandomSpawnConfig
{
    SpawnCount = 10,
    SpawnPosition = new float3(0, 0, 0),
    SpawnRange = 50
    // 设置其他参数
});
```

通过这种方法，您可以在DOTS中为系统提供参数，并在其他项目中根据需要设置这些参数。这与传统的OOP编程模式中的函数参数类似。


#### 复用、封装程序

> [!question]
> 对于开发好的DOTS的比较常用的功能代码。我需要怎么进行封装以便于其他项目引用这些功能？换句话说，在DOTS中，怎么类似传统的OOP开发模式那样继承并且扩展功能、代码？


在DOTS中，由于其数据驱动的设计，继承和OOP模式并不直接适用。但是，您可以通过以下方法封装和重用您的DOTS功能代码：

1. 将常用的功能代码放入独立的C#类库项目中。这样，您可以将其编译为一个DLL，并在其他项目中引用该DLL。

2. 把相关的组件、系统和数据结构放在同一个命名空间下。这样可以更好地组织代码，便于在其他项目中引用。

3. 对于可复用的系统，您可以使用接口或抽象类来定义其行为。然后在具体的实现中，针对不同项目的需求，实现这些接口或继承抽象类。这样可以在一定程度上模拟OOP的继承特性。

4. 使用组合而非继承。在DOTS中，您可以通过组合不同的组件来实现功能的扩展。例如，如果您有一个通用的移动系统，您可以将其与其他组件（如攻击、防御等）组合在一起，以实现更复杂的行为。

5. 使用事件或消息传递系统来解耦系统之间的依赖关系。这样，您可以轻松地在不同项目中重用和扩展功能。

通过以上方法，您可以在DOTS中封装和重用功能代码，同时保持高性能和灵活性。虽然这与传统的OOP开发模式有所不同，但在ECS架构中仍然可以实现代码的重用和扩展。


#### 事件、消息传递


> [!question]
> DOTS中，如何使用事件或者消息传递实现在不同的项目中重用与扩展功能呢？


在DOTS中，您可以使用Unity的事件系统或自定义消息传递系统来实现功能的重用和扩展。以下是使用事件系统的一种方法：

1. 首先，创建一个事件结构，用于存储事件数据。例如：

```csharp
public struct MyEvent : IComponentData
{
    public int SomeData;
}
```

2. 在需要触发事件的系统中，创建一个实体并添加MyEvent组件。例如：

```csharp
public class TriggerEventSystem : SystemBase
{
    protected override void OnUpdate()
    {
        // 在某个条件下触发事件
        if (SomeCondition)
        {
            var eventEntity = EntityManager.CreateEntity();
            EntityManager.AddComponentData(eventEntity, new MyEvent { SomeData = 123 });
        }
    }
}
```

3. 在需要响应事件的系统中，监听MyEvent组件。例如：

```csharp
public class HandleEventSystem : SystemBase
{
    protected override void OnUpdate()
    {
        Entities.ForEach((Entity entity, ref MyEvent myEvent) =>
        {
            // 处理事件数据
            Debug.Log("Event triggered with data: " + myEvent.SomeData);

            // 移除事件组件，避免重复触发
            EntityManager.RemoveComponent<MyEvent>(entity);
        }).Schedule();
    }
}
```

通过这种方法，您可以在不同的项目中重用和扩展功能，同时保持ECS架构的性能优势。请注意，在实际项目中，您可能需要根据具体需求调整事件系统的实现。