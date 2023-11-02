---
title: Unity如何创建、实现和调用扩展方法
authors: Ethan Lin
year: 2022-11-25 
tags:
  - 日期/2022-11-25 
  - 类型/笔记 
  - 内容/Unity 
  - 类型/解决 
---


# Unity如何创建、实现和调用扩展方法







## 如何创建、实现和调用扩展方法

ExtensionMethods

`

```C#
using UnityEngine; using System.Collections; //创建一个包含所有扩展方法的类 //是很常见的做法。此类必须是静态类。 public static class ExtensionMethods { //扩展方法即使像普通方法一样使用， //也必须声明为静态。请注意，第一个 //参数具有“this”关键字，后跟一个 Transform //变量。此变量表示扩展方法会成为 //哪个类的一部分。 public static void ResetTransformation(this Transform trans) {
        trans.position = Vector3.zero;
        trans.localRotation = Quaternion.identity;
        trans.localScale = new Vector3(1, 1, 1);
    }
}
```




SomeClass


```C#
using UnityEngine; using System.Collections; public class SomeClass : MonoBehaviour 
{ void Start () { //请注意，即使方法声明中 //有一个参数，也不会将任何参数传递给 //此扩展方法。调用此方法的 //Transform 对象会自动作为 //第一个参数传入。 transform.ResetTransformation();
}
}
```

