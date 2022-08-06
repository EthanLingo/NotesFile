# Unity查找物体

tags: #内容/Unity #来源/转载 



# GameObject.Find

`GameObject.Find()`

优点：

使用简单方便

不会因为重名而报错，同时查找的是自上而下的第一个物体

缺点：

不能查找被隐藏的物体，否则出现“空引用异常”，这是很多新人在查找出现空引用bug的原因。

全局查找(遍历查找)，查找效率低，很消耗性能。

代码演示：

```c#
using System.Collections;

using System.Collections.Generic;

using UnityEngine;

public class GameObjectFind : MonoBehaviour {

private GameObject thing;

void Start () {

thing = GameObject.Find("C4");

thing.name = "thing";
}

}
```



# Transform.Find

`Transform.Find()`，通过Transform组件查找子物体。

用这个方法查找物体时，根节点一定要处于“显示”状态，不能被隐藏。

用它查找孙物体及孙孙物体，一定要使用“绝对路径”，否则出现“空引用异常”。

代码演示：

```
using System.Collections;

using System.Collections.Generic;

using UnityEngine;

public class TransformFind : MonoBehaviour {

private Transform m_Transform;

private GameObject one;

private GameObject two;

void Start () {

m_Transform = gameObject.GetComponent();

one = m_Transform.Find("D2").gameObject;

two = m_Transform.Find("D2/D3").gameObject;

Debug.Log(one.name);

Debug.Log(two.name);

}

}
```





# GameObject.FindGameObjectWithTag

GameObject.FindGameObjectWithTag()和GameObject.FindGameObjectsWithTag()，通过Tag标签查找物体。

GameObject.FindGameObjectsWithTag()：通过Tag标签查找到一组物体，返回一个数组。

GameObject.FindGameObjectWithTag()：查找到这类tag标签，自上而下第一个物体。

代码演示：

```c#
using System.Collections;

using System.Collections.Generic;

using UnityEngine;

public class TagFind : MonoBehaviour {

private GameObject thing;

private GameObject[] things;

void Start () {

things = GameObject.FindGameObjectsWithTag("Player");

thing = GameObject.FindGameObjectWithTag("Player");

Debug.Log(things.Length);

Debug.Log(thing.name);

}

}
```



# FindObjectsOfType

`FindObjectsOfType()`

FindObjectsOfTypeAll()：返回指定类型的对象列表。

代码演示：

```c#
using System.Collections;

using System.Collections.Generic;

using UnityEngine;

public class FindObjectOfType : MonoBehaviour {

private GameObject[] things;

private GameObject thing;

void Start () {

things = FindObjectsOfType();

thing = FindObjectOfType();

Debug.Log("第一个" + thing.name);

for(int i = 0; i < things.Length; i++)

{

Debug.Log(things[i].name);

}

}

}
```





————————————————

> 版权声明：本文为CSDN博主「苏白衣」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_29774037/article/details/113685717
