---
title: Unity辨析gameObject、transform、GameObject、Transform
authors: Ethan Lin
year: 2022-08-06 
tags:
  - 日期/2022-08-06 
  - 类型/笔记 
  - 来源/转载 
  - 内容/Unity 
  - 类型/辨析 
---


# Unity辨析gameObject、transform、GameObject、Transform





## GameObject 与 gameObject：
Gameobject是一个类型，所有的游戏物件都是这个类型的对象。   
gameobject是一个对象， 就跟java里面的this一样， 指的是这个脚本所附着的游戏物件。

## Transform 与 transform：
Transform是一个类，用来描述物体的位置，大小，旋转等等信息。 
transform是Transform类的对象，依附于每一个物体。也是当前游戏对象的一个组件(每个对象都会有这个组件)。

## gameobject 与 transform：
- 二者的含义：
transform : 当前游戏对象的transform组件。
gameobject ：当前游戏对象的实例。
- 两者的联系和区别：
	* 在unity中每个游戏对象都是一个gameobject。gameobject就代表着本脚本所依附的对象。 每个gameobject都包含各种各样的组件，但从这点可以看出transform是gameobject的一个组件，控制着gameobject的位置，缩放，和旋转，而且每个gameobject都有而且必有一个transform组件。
	* gameobject.find用来获取场景中那个我们需要查找的对象（object）。而transform.find方法则是获取当前对象的子对象下我们需要获取的目标对象位置信息。


————————————————

> 版权声明：本文为CSDN博主「LNGOD」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：[Unity transform 和 gameObject的关系与区别](https://blog.csdn.net/qq_36946274/article/details/81200954)
> 

