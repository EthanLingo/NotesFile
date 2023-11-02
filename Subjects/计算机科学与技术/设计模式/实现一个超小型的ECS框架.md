---
title: 实现一个超小型的ECS框架
authors: Ethan Lin
year: 2023-05-28 
tags:
  - 日期/2023-05-28 
  - 类型/AI问答笔记 
  - 类型/笔记 
  - 类型/实战 
  - 内容/csharp 
  - 内容/编程 
  - 内容/设计模式 
  - 内容/ECS框架 
---


# 实现一个超小型的ECS框架




# CSharp篇

> [!attention]
> 以下由AI回答，不保证正确性！


> [!question] 
> 如何基于C sharp设计一个极为简易的ECS框架实现？

如果你想要自己设计一个极为简易的ECS框架实现，可以按照以下步骤：

1. 定义实体(Entity)：实体是一个抽象的概念，可以理解为游戏中的物体或角色。每个实体可以由多个组件组成。

2. 定义组件(Component)：组件是实体的属性或状态。比如位置、速度、血量等。每个组件应该是一个独立的数据结构，不应该有任何与其他组件或实体相关的引用。

3. 定义系统(System)：系统是处理组件数据的逻辑单元。每个系统应该只负责处理一种类型的组件，以保证系统的单一职责原则。系统可以在游戏循环中被调用，以更新组件的数据或执行其他逻辑。

4. 定义世界(World)：世界是实体、组件和系统的容器。世界可以包含多个实体，并且每个实体可以拥有不同的组件。世界还可以包含多个系统，以处理不同类型的组件。在游戏循环中，世界可以更新所有系统，以更新组件数据或执行其他逻辑。

5. 定义组件存储(Component Storage)：组件存储是用于存储组件数据的数据结构。可以使用数组、链表、哈希表或其他数据结构来实现。每个组件存储应该只存储一种类型的组件，并且应该支持快速的查找和遍历操作。

6. 定义实体管理器(Entity Manager)：实体管理器是用于管理实体和组件存储的类。实体管理器可以创建新实体、销毁实体、添加组件、删除组件等操作。实体管理器还可以提供查询接口，以查询拥有特定组件的实体。

7. 实现系统执行逻辑：在系统的执行逻辑中，首先需要获取该系统所处理的组件存储。然后遍历所有拥有该组件的实体，以执行所需的逻辑。在执行逻辑时，应该尽量避免频繁的内存分配和释放操作，以提高性能。

以下是一个简单的示例代码，演示如何手动实现一个简单的ECS框架：

```C#
public class Entity
{
    public int id;
}

public abstract class Component
{
    public Entity entity;
}

public class PositionComponent : Component
{
    public float x;
    public float y;
}

public abstract class System
{
    public abstract void Update();
}

public class MovementSystem : System
{
    private ComponentStorage<PositionComponent> positionStorage;

    public MovementSystem(ComponentStorage<PositionComponent> positionStorage)
    {
        this.positionStorage = positionStorage;
    }

    public override void Update()
    {
        foreach (PositionComponent position in positionStorage.Components)
        {
            position.x += 1.0f;
            position.y += 1.0f;
        }
    }
}

public class ComponentStorage<T> where T : Component
{
    public List<T> Components = new List<T>();
}

public class EntityManager
{
    private int nextId = 0;
    private Dictionary<int, Entity> entities = new Dictionary<int, Entity>();
    private Dictionary<Type, object> componentStorages = new Dictionary<Type, object>();
    
    public Entity CreateEntity()
    {
        Entity entity = new Entity { id = nextId++ };
        entities.Add(entity.id, entity);
        return entity;
    }
    
    public void DestroyEntity(Entity entity)
    {
       foreach (var componentStorage in componentStorages.Values)
        {
            Type type = componentStorage.GetType().GetGenericArguments()[0];
            MethodInfo removeMethod = componentStorage.GetType().GetMethod("Remove");
            removeMethod.Invoke(componentStorage, new object[] { entity });
        }

        entities.Remove(entity.id);
    }

    public void AddComponent<T>(Entity entity, T component) where T : Component
    {
        if (!componentStorages.ContainsKey(typeof(T)))
        {
            componentStorages.Add(typeof(T), new ComponentStorage<T>());
        }

        ComponentStorage<T> componentStorage = (ComponentStorage<T>)componentStorages[typeof(T)];
        component.entity = entity;
        componentStorage.Components.Add(component);
    }

    public void RemoveComponent<T>(Entity entity) where T : Component
    {
        if (componentStorages.ContainsKey(typeof(T)))
        {
            ComponentStorage<T> componentStorage = (ComponentStorage<T>)componentStorages[typeof(T)];
            componentStorage.Components.RemoveAll(c => c.entity.id == entity.id);
        }
    }

    public List<T> GetComponents<T>() where T : Component
    {
        if (componentStorages.ContainsKey(typeof(T)))
        {
            ComponentStorage<T> componentStorage = (ComponentStorage<T>)componentStorages[typeof(T)];
            return componentStorage.Components;
        }

        return new List<T>();
    }

    public List<Entity> GetEntitiesWithComponents(params Type[] componentTypes)
   {
        List<Entity> entitiesWithComponents = new List<Entity>();

        foreach (Entity entity in entities.Values)
        {
            bool hasAllComponents = true;

            foreach (Type componentType in componentTypes)
            {
                if (!componentStorages.ContainsKey(componentType) || !componentStorages[componentType].GetType().GetGenericArguments()[0].IsAssignableFrom(componentType))
                {
                    hasAllComponents = false;
                    break;
                }
            }

            if (hasAllComponents)
            {
                entitiesWithComponents.Add(entity);
            }
        }

        return entitiesWithComponents;
    }
}

public class Game
{
    private EntityManager entityManager = new EntityManager();
    private MovementSystem movementSystem;

    public void Init()
    {
        Entity entity = entityManager.CreateEntity();
        PositionComponent position = new PositionComponent { x = 0.0f, y = 0.0f };
        entityManager.AddComponent(entity, position);

        ComponentStorage<PositionComponent> positionStorage = new ComponentStorage<PositionComponent>();
        positionStorage.Components.Add(position);

        movementSystem = new MovementSystem(positionStorage);
    }

    public void Update()
    {
        movementSystem.Update();
    }
}

```

在这个简单的示例中，我们定义了实体(Entity)、组件(Component)、系统(System)、组件存储(Component Storage)和实体管理器(Entity Manager)。我们创建了一个游戏(Game)类，并在其中初始化了一个实体和一个MovementSystem。在Update()方法中，我们调用MovementSystem的Update()方法，以更新实体的位置。

虽然这个示例非常简单，但它演示了如何手动实现一个基本的ECS框架。需要注意的是，这只是一个非常基础的实现，实际上一个完整的ECS框架需要更多的细节处理和优化，以实现更好的性能和可扩展性。


> [!question] 
> 如果涉及到读写组件时发生冲突怎么办？


在ECS框架中，由于组件数据被分离到不同的存储中，多个系统可能同时访问相同的组件存储，从而可能发生读写冲突。为了避免冲突，可以采取以下措施：

1. 禁止在系统中修改组件数据：系统应该只读取组件数据，而不应该修改它们。如果系统需要修改组件数据，可以将修改请求发送到组件存储或实体管理器，并在适当的时候进行处理。

2. 加锁：如果系统需要修改组件数据，可以在访问组件存储时加锁，以避免其他系统同时访问。例如，可以使用C#中的lock语句或Monitor类来实现简单的锁定机制。

3. 分离读写：如果多个系统需要同时访问相同的组件存储，可以使用读写锁或信号量等机制来分离读操作和写操作。例如，可以使用C#中的ReaderWriterLockSlim类来实现。

4. 使用版本号：每个组件可以维护一个版本号，以标识组件数据的修改版本。当组件数据被修改时，版本号也应该相应地增加。在读取组件数据时，系统可以读取组件的版本号并保存它们。如果在读取期间组件数据发生了修改，系统可以检查版本号是否发生了变化，以判断组件数据是否有效。

需要注意的是，以上措施并不是互斥的，可以根据实际情况选择合适的方法。同时，需要根据具体的ECS框架实现方式和使用场景，进行相应的优化和调整，以保证性能和可靠性。

以下是根据上述问题改进后的代码，其中使用了读写锁机制来避免读写冲突：

```C#
public class Entity
{
    public int id;
}

public abstract class Component
{
    public Entity entity;
    public int version = 0;
}

public class PositionComponent : Component
{
    public float x;
    public float y;
}

public abstract class System
{
    public abstract void Update();
}

public class MovementSystem : System
{
    private ComponentStorage<PositionComponent> positionStorage;
    private ReaderWriterLockSlim positionStorageLock;

    public MovementSystem(ComponentStorage<PositionComponent> positionStorage)
    {
        this.positionStorage = positionStorage;
        this.positionStorageLock = new ReaderWriterLockSlim();
    }

    public override void Update()
    {
        positionStorageLock.EnterReadLock();
        try
        {
            foreach (PositionComponent position in positionStorage.Components)
            {
                // 读取组件数据，不修改
                Console.WriteLine($"Position of entity {position.entity.id}: ({position.x}, {position.y})");
            }
        }
        finally
        {
            positionStorageLock.ExitReadLock();
        }

        // 修改组件数据
        positionStorageLock.EnterWriteLock();
        try
        {
            foreach (PositionComponent position in positionStorage.Components)
            {
                position.x += 1.0f;
                position.y += 1.0f;
                position.version++;
            }
        }
        finally
        {
            positionStorageLock.ExitWriteLock();
        }
    }
}

public class ComponentStorage<T> where T : Component
{
    public List<T> Components = new List<T>();
    private ReaderWriterLockSlim componentsLock = new ReaderWriterLockSlim();

    public void Add(T component)
    {
        componentsLock.EnterWriteLock();
        try
        {
            Components.Add(component);
        }
        finally
        {
            componentsLock.ExitWriteLock();
        }
    }

    public void Remove(T component)
    {
        componentsLock.EnterWriteLock();
        try
        {
            Components.Remove(component);
        }
        finally
        {
            componentsLock.ExitWriteLock();
        }
    }

    public bool TryGetComponent(Entity entity, out T component)
    {
        componentsLock.EnterReadLock();
        try
        {
            component = Components.Find(c => c.entity == entity) as T;
            return (component != null);
        }
        finally
        {
            componentsLock.ExitReadLock();
        }
    }

    public List<T> GetAllComponents()
    {
        componentsLock.EnterReadLock();
        try
        {
            return new List<T>(Components);
        }
        finally
        {
            componentsLock.ExitReadLock();
        }
    }
}

public class EntityManager
{
    private int nextId = 0;
    private Dictionary<int, Entity> entities = new Dictionary<int, Entity>();
    private Dictionary<Type, object> componentStorages = new Dictionary<Type, object>();
    private ReaderWriterLockSlim entitiesLock = new ReaderWriterLockSlim();

    public Entity CreateEntity()
    {
        Entity entity = new Entity { id = nextId++ };
        entitiesLock.EnterWriteLock();
        try
        {
            entities.Add(entity.id, entity);
        }
        finally
        {
            entitiesLock.ExitWriteLock();
        }
        return entity;
    }

    public void DestroyEntity(Entity entity)
    {
        foreach (var componentStorage in componentStorages.Values)
        {
            Type type = componentStorage.GetType().GetGenericArguments()[0];
            MethodInfo removeMethod = componentStorage.GetType().GetMethod("Remove");
            object[] parameters = new object[] { null };
            removeMethod.Invoke(componentStorage, new object[] { entity });
        }

        entitiesLock.EnterWriteLock();
        try
        {
            entities.Remove(entity.id);
        }
        finally
        {
            entitiesLock.ExitWriteLock();
        }
    }

    public void AddComponent<T>(Entity entity, T component) where T : Component
    {
        if (!componentStorages.ContainsKey(typeof(T)))
        {
            componentStorages.Add(typeof(T), new ComponentStorage<T>());
        }

        ComponentStorage<T> componentStorage = (ComponentStorage<T>)componentStorages[typeof(T)];
        component.entity = entity;
        componentStorage.Add(component);
    }

    public void RemoveComponent<T>(Entity entity) where T : Component
    {
        if (componentStorages.ContainsKey(typeof(T)))
        {
            ComponentStorage<T> componentStorage = (ComponentStorage<T>)componentStorages[typeof(T)];
            T component;
            if (componentStorage.TryGetComponent(entity, out component))
            {
                componentStorage.Remove(component);
            }
        }
    }

    public List<T> GetComponents<T>() where T : Component
    {
        if (componentStorages.ContainsKey(typeof(T)))
        {
            ComponentStorage<T> componentStorage = (ComponentStorage<T>)componentStorages[typeof(T)];
            return componentStorage.GetAllComponents();
        }

        return new List<T>();
    }

    public List<Entity> GetEntitiesWithComponents(params Type[] componentTypes)
    {
        List<Entity> entitiesWithComponents = new List<Entity>();

        entitiesLock.EnterReadLock();
        try
        {
            foreach (Entity entity in entities.Values)
            {
                bool hasAllComponents = true;

                foreach (Type componentType in componentTypes)
                {
                    if (!componentStorages.ContainsKey(componentType) || !componentStorages[componentType].GetType().GetGenericArguments()[0].IsAssignableFrom(componentType))
                    {
                        hasAllComponents = false;
                        break;
                    }
                }

                if (hasAllComponents)
                {
                    entitiesWithComponents.Add(entity);
                }
            }
        }
        finally
        {
            entitiesLock.ExitReadLock();
           }

    public List<Entity> GetAllEntities()
    {
        entitiesLock.EnterReadLock();
        try
        {
            return new List<Entity>(entities.Values);
        }
        finally
        {
            entitiesLock.ExitReadLock();
        }
    }
}
```

在以上代码中，添加了一个`ReaderWriterLockSlim`类型的读写锁来保证多个系统同时访问相同的组件存储时不会发生读写冲突。在`MovementSystem`中，使用读锁来读取组件数据，使用写锁来修改组件数据。在`ComponentStorage`和`EntityManager`中，也使用了读写锁来保护组件存储和实体管理器的读写操作。这样可以保证系统的并发性能和可靠性。