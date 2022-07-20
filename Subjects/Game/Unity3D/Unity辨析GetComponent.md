# Unity辨析GetComponent

tags: #内容/Unity #来源/转载 

```c#
MyComponment myCom=gameObject.GetComponent<MyComponment>();
 
MyComponment childCom=gameObject.GetComponentInChildren<MyComponment>();
 
MyComponment[] comS=gameObject.GetComponents<MyComponment>();
 
MyComponment[] comS1=gameObject.GetComponentsInChildren<MyComponment>();
 
MyComponment[] comSTrue=gameObject.GetComponentsInChildren<MyComponment>(true);
 
MyComponment[] comSFalse=gameObject.GetComponentsInChildren<MyComponment>(false);
```

这几句话的区别

1. `GetCompoment<T>()`从当前游戏对象获取组件T，只在当前游戏对象中获取，没得到的就返回null，不会去子物体中去寻找。

2. `GetCompomentInChildren<T>()`先从本对象中找，有就返回，没就子物体中找，知道找完为止。

3. `GetComponents<T>()`获取本游戏对象的所有T组件，不会去子物体中找。

4. `GetComponentsInChildren<T>()=GetComponentsInChildren<T>(true)`取本游戏对象及子物体的所有组件

1. `GetComponentsInChildren<T>(false)`取本游戏对象及子物体的所有组件 除开非活跃的游戏对象，不是该组件是否活跃。


> 来源：
————————————————
版权声明：本文为CSDN博主「kaixindragon」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/kaixindragon/article/details/44776451

相关：
[[Unity查找物体]]
[[Unity辨析transform与gameObject]]
[[Unity辨析GameObject.Find与Transform.Find]]