---
title: Unity辨析transform与gameObject
authors: Ethan Lin
year:
tags:
  - 内容/Unity 
  - 来源/转载 
---


# Unity辨析transform与gameObject






**Transform**是一个类，用来描述物体的位置，大小，旋转等等信息。  
**transform**是Transform类的对象，依附于每一个物体。也是当前游戏对象的一个组件(每个对象都会有这个组件)

## **transform与gameObject**

1. 二者的含义  
        transform :  当前游戏对象的transform组件  
   　  gameobject ：当前游戏对象的实例

2. 两者的联系和区别  
        - 在unity中每个游戏对象都是一个gameobject. monodevelop中的gameobject就代表着本脚本所依附的对象. 每个gameobject都包含各种各样的组件，但从这点可以看出transform是gameobject的一个组件，控制着gameobject的位置，缩放，和旋转，而且每个gameobject都有而且必有一个transform组件  
        - gameobject.find用来获取场景中那个我们需要查找的对象(object).  而transform.find方法则是获取当前对象的子对象下我们需要获取的目标对象位置信息。  
        - 注意:  在update() 中尽量不使用Find() 方法，影响性能.     

3. gameobject.transform与transform.gameobject

        - gameobject.transform,是获取当前游戏对象的transform组件.  
            所以在start函数中 gameobject.transform 和this.transform,指向的都是同一个对象。即：gameobject.transform == this.transform == transform

        - transform.gameobject:可以这么理解为：获取当前transform组件所在的gameobect  
           所以在start()函数中transform.gameobject == this.gameobject == gameobect

 　　**所以他们可以无限的引用下去**

意思就是：gameobject.transform == this.transform == gameobject.transform.gameobject.tranform == tranform.gameobect.transform

> 相关：
> [[Unity辨析GetComponent]]
> [[Unity辨析GameObject.Find与Transform.Find]]
> [[Unity查找物体]]
