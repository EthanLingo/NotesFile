



tags: #日期/2023-08-11 #类型/笔记 #内容/Unity #内容/DOTS #类型/AI问答笔记 


> [!question]
> 如何结合 Unity Input System 与 DOTS，给一个例子

> [!AI'answer]

以下是一个简单的示例代码，展示了如何将新的Input System与ECS系统结合使用：

首先，创建一个`InputData`组件用于存储输入状态：

```csharp
public struct InputData : IComponentData
{
    public float2 move;
    public float2 look;
    public bool fire;
}
```

接下来，在原有的`SimpleController_UsingActionAsset`类中，将输入状态写入`InputData`组件：

```csharp
public class SimpleController_UsingActionAsset : MonoBehaviour, IConvertGameObjectToEntity
{
    // ...其他代码...

    public void Update()
    {
        var look = m_Controls.gameplay.look.ReadValue<Vector2>();
        var move = m_Controls.gameplay.move.ReadValue<Vector2>();
        var fire = m_Controls.gameplay.fire.triggered;

        EntityManager entityManager = World.DefaultGameObjectInjectionWorld.EntityManager;
        Entity entity = GetComponent<GameObjectEntity>().Entity;

        entityManager.SetComponentData(entity, new InputData
        {
            move = move,
            look = look,
            fire = fire
        });
    }

    public void Convert(Entity entity, EntityManager dstManager, GameObjectConversionSystem conversionSystem)
    {
        dstManager.AddComponentData(entity, new InputData());
    }
}
```

最后，创建一个新的ECS系统，并在`OnUpdate`方法中读取`InputData`组件的状态：

```csharp
public class PlayerControlSystem : SystemBase
{
    protected override void OnUpdate()
    {
        float deltaTime = Time.DeltaTime;

        Entities.ForEach((ref Translation translation, ref Rotation rotation, in InputData inputData) =>
        {
            // 在这里根据 inputData.move 和 inputData.look 实现移动和旋转逻辑
            // 在这里根据 inputData.fire 实现射击逻辑
        }).Run();
    }
}
```

这个示例展示了如何将输入状态从`SimpleController_UsingActionAsset`类传递到ECS系统。在ECS系统中，你可以根据`InputData`组件的状态来执行移动、旋转和射击操作。请注意，这个示例仅作为一个起点，你可能需要根据实际项目需求进行调整。