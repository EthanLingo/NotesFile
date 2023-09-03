# DOTS 学习笔记



tags: #日期/2023-04-22 #类型/AI问答笔记 #内容/DOTS 



> [!attention]
> 以下由AI回答，有些地方掺入了个人笔记与理解。仅供参考，不保证正确性！


# 手写笔记系列

## 查询

#### ComponentLookup

对于方法`ComponentLookup.TryGetComponent()`。首先新建一个针对查询某个组件之实例`AAAComponentLookup`，然后调用该实例，使用该方法`TryGetComponent`。该方法之形参1是某个要查询的具体的实体；形参2用`out`标记，将查询到的结果传给该形参。


# 一些知识点

#### 为什么不单独用JobSystem，而是要结合DOTS使用？

![[2139D90E-A2BB-406C-B54B-C6F48537D5B4.jpeg]]



#### 从运行模式（runtime）创建 Entities 对象代码

![[0D0941A8-418D-4D81-8261-2E844E4D192D_1_201_a.jpeg]]

# AI问答系列

# 基础知识问答

## Entities实体


#### `Entities.With` 系列的主要方法


> [!question] 
> `Entities.With` 系列的主要方法及其区别？

> [!AI'answer]

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

> [!AI'answer]

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


## Component 组件

#### 嵌套组件

> [!question]
> 如何在一个大组件内嵌套许多的小组件？例如大组件名称为【设置项】，其中包含小组件【生成设置项】、【地图设置项】、【个体属性设置项】、【游戏场景设置项】等等。如果用嵌套组件的方法，会不会影响性能？

> [!AI'answer]

在 DOTS 1.0 中，您可以使用组件嵌套来实现这一目标。您可以创建一个大组件（例如 SettingsComponent），然后在其内部包含其他小组件。以下是一个示例：

```csharp
using Unity.Entities;

public struct SettingsComponent : IComponentData
{
    public GenerationSettingsComponent GenerationSettings;
    public MapSettingsComponent MapSettings;
    public EntityAttributeSettingsComponent EntityAttributeSettings;
    public GameSceneSettingsComponent GameSceneSettings;
}

public struct GenerationSettingsComponent : IComponentData
{
    // 在这里添加生成设置项的属性
}

public struct MapSettingsComponent : IComponentData
{
    // 在这里添加地图设置项的属性
}

public struct EntityAttributeSettingsComponent : IComponentData
{
    // 在这里添加个体属性设置项的属性
}

public struct GameSceneSettingsComponent : IComponentData
{
    // 在这里添加游戏场景设置项的属性
}
```

在这个示例中，我们创建了一个名为 `SettingsComponent` 的大组件，它包含了其他四个小组件。每个小组件都可以包含其特定设置项的属性。这样，您可以在一个大组件中组织和管理多个小组件，以提高代码的可读性和可维护性。

嵌套组件在某种程度上可能会影响性能，但这主要取决于您如何使用和访问这些组件。在 DOTS 架构中，性能主要受以下因素影响：

1. 数据布局：DOTS 通过将相关数据紧密排列在一起来实现高效的内存访问。如果嵌套组件导致数据布局不再紧密排列，这可能会影响性能。

2. 访问模式：在 DOTS 中，以线性方式访问内存通常会带来更好的性能。如果嵌套组件导致您需要频繁地跳过某些数据或以非线性方式访问内存，这可能会影响性能。

3. 数据大小：较大的组件可能导致较慢的内存访问和缓存不命中。如果嵌套组件导致您的组件变得过大，这可能会影响性能。

然而，在许多情况下，组件嵌套的性能影响可能是可以接受的，尤其是在提高代码可读性和可维护性方面。在使用嵌套组件时，请确保您仍然遵循 DOTS 的最佳实践，以实现高性能的数据访问和处理。


#### 管理多个组件

> [!question]
> 有没有保证性能的前提下更好管理多个组件的方案？

> [!AI'answer]

在保证性能的前提下，您可以考虑使用以下策略来更好地管理多个组件：

1. 组件分组：将相关组件放在一起，并为它们创建专门的命名空间。这样可以让您更容易地在项目中查找和管理这些组件。

```csharp
namespace MyGame.Settings
{
    public struct GenerationSettingsComponent : IComponentData { /* ... */ }
    public struct MapSettingsComponent : IComponentData { /* ... */ }
    // ...
}
```

2. 使用系统来管理组件间的关系：在 DOTS 中，系统（System）负责处理和操作实体及其组件。您可以创建一个或多个系统来处理和维护组件之间的关系，从而避免将组件嵌套在一起。

```csharp
public class SettingsSystem : SystemBase
{
    protected override void OnUpdate()
    {
        // 在这里处理和维护组件之间的关系
    }
}
```

3. 使用共享组件：共享组件允许您将数据存储在一个组件中，并在多个实体之间共享。这可以减少数据冗余，并简化组件管理。但请注意，共享组件可能会影响内存访问的局部性，因此在性能敏感的场景中要谨慎使用。

```csharp
public struct SharedSettingsComponent : ISharedComponentData
{
    public GenerationSettingsComponent GenerationSettings;
    public MapSettingsComponent MapSettings;
    // ...
}
```

总之，在保证性能的前提下，您可以使用上述策略来更好地管理多个组件。请根据您的项目需求选择最适合您的方法。


## Query 查询


#### 辨析`configQuery.GetSingleton`、`state.EntityManager.GetComponentObject`

> [!question]
> `configQuery.GetSingleton<Config>();`与` state.EntityManager.GetComponentObject<Managed>(state.SystemHandle);`有什么不同？

> [!AI'answer]

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

> [!AI'answer]

`state.Dependency`是一个`JobHandle`类型的变量，用于表示该系统的依赖关系。在Unity ECS框架中，每个系统都可以拥有一个或多个依赖关系，用于确保系统在执行时满足一定的执行顺序。当一个系统完成执行后，它会返回一个`JobHandle`类型的值，表示它的执行状态。其他系统可以使用这个值作为它们的依赖关系，以确保它们在当前系统执行完成之前不会开始执行。因此，在上述代码中，当`CreateGenerateAgentEntityJob`方法创建并调度执行作业后，将作业返回的`JobHandle`值赋值给`state.Dependency`变量，表示该系统在执行时依赖于这个作业的完成状态。


## `Flags`标记


#### `RequireMatchingQueriesForUpdate`

> [!question]
> `RequireMatchingQueriesForUpdate` 是什么？

> [!AI'answer]

`RequireMatchingQueriesForUpdate`是一个用于确定系统是否应该运行的标志。当一个系统有这个标志时，它只会在与其查询完全匹配的实体上运行，否则它将被跳过，不会执行任何操作。

具体地说，每个ECS系统都通过一个查询（Query）来确定它应该处理哪些实体。该查询定义了系统应该包含哪些组件以及它们的值。`RequireMatchingQueriesForUpdate`标志告诉系统只有在所有实体的组件与查询完全匹配时才应该运行。否则，系统将跳过该帧的更新。

这个标志对于优化性能非常有用，因为它可以避免系统处理不必要的实体。例如，如果您有一个处理敌人AI的系统，当这个标志被启用时，它只会在那些具有所有必需组件（如“位置”和“生命值”）的敌人实体上运行。这样，系统就不会浪费时间在没有必要组件的实体上进行计算。

需要注意的是，使用`RequireMatchingQueriesForUpdate`标志可能会增加代码复杂度，因为您需要确保所有实体都具有必需的组件。但是，这个标志在正确使用时可以显著提高系统性能。


#### `RequireForUpdate`

> [!question] 
> `RequireForUpdate` 是什么？

> [!AI'answer]

`RequireForUpdate` 是 Unity DOTS 中的一个标记（Flag），用于控制系统（System）在何时执行更新。

在 Unity DOTS 中，系统可以通过实现 `ISystemBase` 接口来定义自己的逻辑。系统在每一帧中被调用多次，以更新游戏状态。但有些情况下，系统不需要在每一帧都更新，例如只在某些条件满足时才需要执行更新操作。这时，可以使用 `RequireForUpdate` 标记来控制系统的更新时机。

具体来说，系统可以在 `OnCreate()` 方法中调用 `World.GetOrCreateSystem<EntityManager>().AddEntityToEntityQueries(this, requireForUpdate)` 方法来将自己添加到需要更新的系统列表中。然后，在需要更新时可以调用 `EntityManager.AddComponentData()` 方法向特定的实体（`Entity`）添加 `RequireForUpdate` 标记，以通知系统在下一帧中执行更新操作。

需要注意的是，`RequireForUpdate` 标记只有在实体发生变化时才会触发更新。因此，如果需要在某些条件满足时立即更新系统，可以使用 `World.EntityManager.CompleteAllJobs()` 方法强制完成所有作业（Jobs），以确保 `RequireForUpdate` 标记在下一帧中得到更新。

总之，`RequireForUpdate` 标记可以帮助开发者更加灵活地控制系统的更新时机，从而提高游戏的性能和效率。 是 Unity DOTS 中的一个标记（Flag），用于控制系统（System）在何时执行更新。

在 Unity DOTS 中，系统可以通过实现 ISystemBase 接口来定义自己的逻辑。系统在每一帧中被调用多次，以更新游戏状态。但有些情况下，系统不需要在每一帧都更新，例如只在某些条件满足时才需要执行更新操作。这时，可以使用 `RequireForUpdate` 标记来控制系统的更新时机。

具体来说，系统可以在 `OnCreate()` 方法中调用 `World.GetOrCreateSystem<EntityManager>().AddEntityToEntityQueries(this, requireForUpdate)` 方法来将自己添加到需要更新的系统列表中。然后，在需要更新时可以调用 `EntityManager.AddComponentData()` 方法向特定的实体（Entity）添加 `RequireForUpdate` 标记，以通知系统在下一帧中执行更新操作。

需要注意的是，`RequireForUpdate` 标记只有在实体发生变化时才会触发更新。因此，如果需要在某些条件满足时立即更新系统，可以使用 `World.EntityManager.CompleteAllJobs()` 方法强制完成所有作业（Jobs），以确保 `RequireForUpdate` 标记在下一帧中得到更新。

总之，`RequireForUpdate` 标记可以帮助开发者更加灵活地控制系统的更新时机，从而提高游戏的性能和效率。


> [!question]
> 为什么state.RequireForUpdate常常写在OnCreate方法内呢？

> [!AI'answer]

`state.RequireForUpdate`通常写在`OnCreate`方法内，因为`OnCreate`在系统创建时仅执行一次。这是一个很好的时机来设置系统所需的组件，因为它可以确保在系统开始执行之前，已经定义了所需的组件条件。

将`state.RequireForUpdate`放在`OnCreate`中可以提高性能，因为您只需在系统创建时设置一次组件条件，而不是在每次系统执行时进行检查。这样可以减少不必要的运行时开销，并确保系统在整个生命周期中始终遵循相同的组件条件。


##### `state.Enabled`与`state.RequireForUpdate&lt<>()`的区别？

> [!question]
> `state.Enabled`与`state.RequireForUpdate<>()`的区别？

> [!AI'answer]

关于`state.Enabled`和`state.RequireForUpdate<>()`的区别，这两者通常在Unity DOTS的Entity Component System (ECS)中使用。

`state.Enabled`用于控制系统的启用或禁用状态。当您需要暂停或恢复系统的执行时，您可以使用`state.Enabled`。例如，您可以将`state.Enabled`设置为`false`以停止系统的执行，或将其设置为`true`以恢复执行。这对于在游戏中实现暂停功能或根据游戏逻辑启用/禁用某些系统非常有用。

`state.RequireForUpdate<>()`用于定义系统执行所需的组件。这是一种声明式方法，用于指定系统在执行时需要哪些组件。当实体具有满足`RequireForUpdate`条件的组件时，系统将对该实体执行。这样可以确保系统仅在需要的组件可用时运行，从而提高性能。

总之，`state.Enabled`用于控制系统的启用/禁用状态，而`state.RequireForUpdate<>()`用于定义系统执行所需的组件。这两者在ECS中起着不同的作用，并有助于实现高性能的游戏逻辑。

`state.RequireForUpdate`可以间接地达到禁用系统的效果。当您使用`state.RequireForUpdate`定义系统所需的组件时，如果某个实体没有满足条件的组件，那么系统将不会对该实体执行。因此，如果没有实体具有满足`RequireForUpdate`条件的组件，系统实际上将不执行任何操作。

这种方法可以让您通过控制组件的存在来控制系统的执行，而不是直接启用或禁用系统。这可以作为一种有效地控制系统行为的方法，但请注意，这种方法可能不如直接使用`state.Enabled`那么直观。

##### `RequireForUpdate`触发条件

> [!question]
> `RequireForUpdate<A>()`触发条件是什么？


> [!AI'answer]

`RequireForUpdate<A>()`是在具有组件A的实体上触发更新的情况下才进行更新。只有当组件A的数值发生变化时，才会触发系统更新。这意味着只有拥有组件A的实体上的组件A的数值发生变化时，系统才会执行更新操作。如果具有A的实体上的其他组件的数值发生变化，系统将不会触发更新。

在DOTS中，如果有多个语句`RequireForUpdate<X>()`，只要有一个满足更新条件，系统就会执行更新操作。

要实现同时满足多个条件才进行更新，你可以使用`RequireForAll`方法。这个方法可以接受一个参数列表，包含需要满足的所有条件。只有当所有条件都满足时，系统才会进行更新。


## `SystemAPI.GetSingleton`系列

> [!question]
> `var a =  SystemAPI.GetSingletonRW<A>().ValueRW;`与`ref var a = ref SystemAPI.GetSingletonRW<A>().ValueRW;`与`var a = SystemAPI.GetSingleton<A>();`这三者有什么区别？

让我来解释一下这三者之间的区别：

1. `var a = SystemAPI.GetSingletonRW<A>().ValueRW;`：这行代码使用`GetSingletonRW`方法获取类型为A的单例组件的可读写引用，并将其赋值给变量a。这意味着你可以直接通过变量a来读取和修改该单例组件的值。

1. `ref var a = ref SystemAPI.GetSingletonRW<A>().ValueRW;`：这行代码也使用`GetSingletonRW`方法获取类型为A的单例组件的可读写引用。不同之处在于它使用了`ref`关键字来声明引用。这意味着你可以通过变量a来读取和修改单例组件的值，并且对a的修改会直接反映在单例组件上。

1. `var a = SystemAPI.GetSingleton<A>();`：这行代码使用`GetSingleton`方法获取类型为A的单例组件的只读引用，并将其赋值给变量a。这意味着你只能通过变量a读取单例组件的值，而无法直接进行修改。

综上所述，第一种方式允许你读取和修改单例组件的值，第二种方式也允许你读取和修改单例组件的值，并且修改会直接反映在单例组件上，而第三种方式只能读取单例组件的值而无法修改。

希望这回答了你的问题！如果还有其他疑问，请随时提问。

## `GetSingleton`与`RequireForUpdate`

##### `GetSingleton`需要使用`RequireForUpdate`

> [!question]

当我使用`GetSingleton`的时候，软件提示我：「To use the result of a '`GetSingleton<A>`' call in the function, '`OnCreate`' must include a '`RequireForUpdate`' call」。但是使用`GetSingletonRW`的时候没有提示。所以为什么`GetSingletonRW`不需要使用`RequireForUpdate`，但是`GetSingleton`需要使用`RequireForUpdate`呢？


> [!AI'answer]

`GetSingletonRW`和`GetSingleton`方法用于获取单例组件的引用。它们在使用上有一些细微的区别，其中一个关键区别是它们对系统更新的要求。

`GetSingletonRW`方法返回一个可读写引用，允许你直接修改单例组件的值。由于它提供了对单例组件的读写访问权限，因此在使用`GetSingletonRW`时，不需要在`OnCreate`方法中包含`RequireForUpdate`调用。

而`GetSingleton`方法返回一个只读引用，只能用于读取单例组件的值而不能进行修改。由于只读引用不会对系统的更新产生影响，因此在使用`GetSingleton`时，需要在`OnCreate`方法中包含至少一个`RequireForUpdate`调用。

`RequireForUpdate`调用指示系统在更新期间追踪和更新相关的组件。当使用`GetSingleton`获取单例组件的只读引用时，系统需要知道与该单例组件相关的组件类型，以便进行正确的更新。

所以，为了解决「To use the result of a '`GetSingleton<A>`' call in the function, '`OnCreate`' must include a '`RequireForUpdate`' call」的警告提示，你需要在`OnCreate`方法中添加`RequireForUpdate`调用，以指定与你使用的单例组件相关的组件类型。



## Physics

#### PhysicsStep

> [!AI'answer]

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

> [!AI'answer]

`EntityCommandBuffer` 是 Unity DOTS 中的一个用于管理实体（Entity）和组件（Component）的缓冲区，可以在 Jobs 中用于高效地修改实体和组件。

在 Unity DOTS 中，Jobs 是一种在多线程环境下执行的任务，可以用于高效地处理大量的数据。但是，由于实体和组件的修改必须在主线程中进行，因此在 Jobs 中直接修改实体和组件会导致错误。

`EntityCommandBuffer` 能够解决这个问题。它是一个缓冲区，可以在 Jobs 中记录修改实体和组件的指令，而不是直接执行这些操作。在 Jobs 执行完成后，可以将 `EntityCommandBuffer` 中记录的指令应用到实体和组件上，从而实现对实体和组件的修改。

具体来说，`EntityCommandBuffer` 可以用于添加、移除和修改实体和组件等操作。例如，可以使用 `EntityCommandBuffer.CreateEntity()` 方法创建新的实体，使用 `EntityCommandBuffer.AddComponent()` 方法向实体添加组件，使用 `EntityCommandBuffer.RemoveComponent()` 方法移除实体的组件等。在 Jobs 执行完成后，可以调用 `EntityCommandBuffer.Playback()` 方法将记录的指令应用到实体和组件上。

需要注意的是，`EntityCommandBuffer` 仅能在 Jobs 中使用，不能在主线程中使用。此外，`EntityCommandBuffer` 在执行 `PlayBack()` 方法后会被清空，因此需要在每次使用前重新创建。

总之，`EntityCommandBuffer` 是 Unity DOTS 中一个非常有用的工具，可以帮助开发者在 Jobs 中高效地修改实体和组件，从而提高游戏的性能和效率。


#### `Allocator`

> [!question] 
> 什么是 `Allocator`？

> [!AI'answer]

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



###### 如何传递参数以便于复用

> [!question] 
> 传统的OOP中，为其他项目提供的通用功能，可以通过函数或者类传递属性或者参数值实现。那么在DOTS中，有没有类似的做法呢？例如我实现了一个系统【随机生成实体】。该系统有一些参数：【生成数量】、【生成位置】、【生成范围】、【散布的分布】等。如果在OOP的编程模式中，我可以设计一个函数，然后把这些参数用函数形参提供接口，给其他项目代入具体参数使用。那么在DOTS中，有没有类似的办法呢？

> [!AI'answer]

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


###### 复用、封装程序

> [!question]
> 对于开发好的DOTS的比较常用的功能代码。我需要怎么进行封装以便于其他项目引用这些功能？换句话说，在DOTS中，怎么类似传统的OOP开发模式那样继承并且扩展功能、代码？

> [!AI'answer]

在DOTS中，由于其数据驱动的设计，继承和OOP模式并不直接适用。但是，您可以通过以下方法封装和重用您的DOTS功能代码：

1. 将常用的功能代码放入独立的C#类库项目中。这样，您可以将其编译为一个DLL，并在其他项目中引用该DLL。

2. 把相关的组件、系统和数据结构放在同一个命名空间下。这样可以更好地组织代码，便于在其他项目中引用。

3. 对于可复用的系统，您可以使用接口或抽象类来定义其行为。然后在具体的实现中，针对不同项目的需求，实现这些接口或继承抽象类。这样可以在一定程度上模拟OOP的继承特性。

4. 使用组合而非继承。在DOTS中，您可以通过组合不同的组件来实现功能的扩展。例如，如果您有一个通用的移动系统，您可以将其与其他组件（如攻击、防御等）组合在一起，以实现更复杂的行为。

5. 使用事件或消息传递系统来解耦系统之间的依赖关系。这样，您可以轻松地在不同项目中重用和扩展功能。

通过以上方法，您可以在DOTS中封装和重用功能代码，同时保持高性能和灵活性。虽然这与传统的OOP开发模式有所不同，但在ECS架构中仍然可以实现代码的重用和扩展。


###### 事件、消息传递


> [!question]
> DOTS中，如何使用事件或者消息传递实现在不同的项目中重用与扩展功能呢？

> [!AI'answer]

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

###### 混合两种开发模式

> [!question]
> DOTS如何与传统的OOP开发模式混用？可以举个例子吗？例如需要高性能的地方用DOTS，传统的一些例如游戏交互、游戏暂停、UI用传统方法。但是怎么混用呢？

> [!AI'answer]

在Unity项目中，您可以将DOTS（数据驱动技术栈）与传统的OOP（面向对象编程）模式混合使用。以下是一些建议，帮助您在项目中实现这种混合：

1. 逐步迁移：您可以逐步将OOP代码迁移到DOTS架构。在迁移过程中，您可以保留OOP组件和ECS系统共存的部分，直到整个项目完成迁移。

2. 使用GameObjectEntity：使用`GameObjectEntity`组件，您可以将现有的GameObject转换为具有ECS组件的实体。这样，您可以在ECS系统中处理这些实体，同时仍然使用传统的OOP方法。

3. 使用EntityCommandBuffer：使用`EntityCommandBuffer`，您可以将ECS系统中的更改应用于主线程上的实体。这样，您可以确保在主线程上处理的OOP组件与ECS系统中的数据保持同步。

4. 划分关注点：在项目中明确划分使用OOP和DOTS的部分。对于性能关键的部分，如游戏逻辑和物理模拟，使用DOTS。对于其他部分，如UI和游戏管理，您可以继续使用OOP。

5. 使用Hybrid Renderer：使用Hybrid Renderer，您可以在ECS系统中处理渲染，同时允许传统的OOP组件与ECS组件共享渲染数据。

通过遵循这些建议，您可以在项目中实现DOTS与传统OOP开发模式的混合使用。在迁移过程中，您可能需要根据项目的具体需求进行一些调整。

以下是一个简单的示例，展示了如何在项目中混合使用DOTS和传统OOP方法：

1. 高性能需求（使用DOTS）：假设您的游戏中有大量的移动物体，这些物体需要根据一定的规则进行移动。在这种情况下，您可以使用DOTS来实现高性能的移动逻辑。

首先，创建一个ECS组件，用于存储物体的移动速度：

```csharp
using Unity.Entities;

public struct MoveSpeed : IComponentData
{
    public float Value;
}
```

接着，创建一个ECS系统来处理物体的移动逻辑：

```csharp
using Unity.Entities;
using Unity.Transforms;
using Unity.Mathematics;

public class MoveSystem : SystemBase
{
    protected override void OnUpdate()
    {
        float deltaTime = Time.DeltaTime;
        Entities.ForEach((ref Translation translation, in MoveSpeed moveSpeed) =>
        {
            translation.Value += new float3(moveSpeed.Value * deltaTime, 0, 0);
        }).ScheduleParallel();
    }
}
```

2. 传统游戏交互、游戏暂停和GUI（使用OOP方法）：对于游戏交互、游戏暂停和GUI等功能，您可以继续使用传统的OOP方法。

例如，创建一个游戏管理器，用于处理游戏暂停和恢复：

```csharp
using UnityEngine;

public class GameManager : MonoBehaviour
{
    public bool IsGamePaused { get; private set; }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.P))
        {
            if (IsGamePaused)
            {
                ResumeGame();
            }
            else
            {
                PauseGame();
            }
        }
    }

    private void PauseGame()
    {
        Time.timeScale = 0;
        IsGamePaused = true;
    }

    private void ResumeGame()
    {
        Time.timeScale = 1;
        IsGamePaused = false;
    }
}
```

在这个示例中，我们使用了DOTS来处理性能关键的移动逻辑，而使用传统的OOP方法来处理游戏交互、游戏暂停和GUI。这样，您可以充分利用DOTS的性能优势，同时保留OOP方法的易用性。希望这个示例能帮助您理解如何在项目中混合使用DOTS和传统OOP方法。


### DOTS 与 Unity Input System 结合使用


[[结合 Unity Input System 与 DOTS]]


### CSV 数据 导入 DOTS

> [!question]
> 如何把csv数据表转换成DOTS里的数据？

> [!AI'answer]

要将CSV数据表转换为DOTS中的数据，您需要执行以下步骤：

1. 读取CSV文件：首先，您需要使用适当的方法从CSV文件中读取数据。您可以使用C#中的`StreamReader`或者第三方库（如CsvHelper）来读取CSV文件，并将其解析为适当的数据结构。

1. 创建组件和实体：根据CSV数据的结构，您需要创建适当的组件类型来表示每行数据的属性。然后，您可以使用ECS的API来创建实体，并将解析的数据存储到相应的组件中。

1. 存储实体和组件：您可以使用ECS的`EntityManager`来创建实体，并将组件添加到这些实体中。根据您的需求，您可以选择将数据存储在共享组件中，以便多个系统可以访问和修改数据。

以下是一个简单的示例，演示如何将CSV数据表转换为DOTS中的数据：

```csharp
using System.IO;
using Unity.Entities;
using Unity.Mathematics;
using UnityEngine;

public struct CSVDataComponent : IComponentData
{
    public int id;
    public float value;
}

public class CSVDataConversionSystem : SystemBase
{
    protected override void OnUpdate()
    {
        // 读取CSV文件
        string path = "path/to/csv/file.csv";
        string[] lines = File.ReadAllLines(path);

        // 创建实体和组件
        EntityManager entityManager = World.DefaultGameObjectInjectionWorld.EntityManager;

        for (int i = 1; i < lines.Length; i++) // 从第二行开始，跳过标题行
        {
            string[] data = lines[i].Split(',');

            int id = int.Parse(data[0]);
            float value = float.Parse(data[1]);

            // 创建实体
            Entity entity = entityManager.CreateEntity(typeof(CSVDataComponent));

            // 添加组件并设置数据
            entityManager.AddComponentData(entity, new CSVDataComponent
            {
                id = id,
                value = value
            });
        }
    }
}
```

在这个示例中，我们假设CSV文件的第一列是ID，第二列是值。`CSVDataComponent`是一个用于存储ID和值的组件。

`CSVDataConversionSystem`是一个ECS系统，它读取CSV文件并将数据转换为DOTS中的实体和组件。在`OnUpdate`方法中，我们使用`StreamReader`读取CSV文件的每一行，并将解析的数据存储在适当的组件中。然后，我们使用`EntityManager`创建实体，并将组件添加到这些实体中。

请注意，这只是一个简单的示例，您可能需要根据您的CSV数据的结构和需求进行适当的修改和扩展。

希望这个示例能够帮助您将CSV数据表转换为DOTS中的数据！如果您有其他问题，请随时提问。