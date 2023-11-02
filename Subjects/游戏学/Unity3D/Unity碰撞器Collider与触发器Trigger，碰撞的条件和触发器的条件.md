---
title: Unity碰撞器Collider与触发器Trigger，碰撞的条件和触发器的条件
authors: Ethan Lin
year:
tags:
  - 内容/Unity 
  - 来源/转载 
  - 传播/禁止 
---


# Unity碰撞器Collider与触发器Trigger，碰撞的条件和触发器的条件







一：产生碰撞的条件

1：双方都要有碰撞器。

2：运动的一方一定要有刚体，另一方有无刚体无所谓。

注：如果运动的一方无刚体，它去碰撞静止的刚体，相当于没有装上。



二：接触的两种方式

1：Collision碰撞，造成物理碰撞，可以在碰撞时执行OnCollision事件。

2：Trigger触发，取消所有的物理碰撞，可以在触发时执行OnTrigger事件。

注：两个物体接触不可能同时产生碰撞+接触，最多产生一种。但是可以AB产生碰撞，AC产生触发。



三：产生不同方式接触的条件

1：Collision碰撞：二碰撞、一刚体

（1）：双方都有碰撞体

（2）：运动的一方必须有刚体

（3）：双方不可同时勾选Kinematic运动学。

（4）：双方都不可勾选Trigger触发器。

2：Trigger触发：二碰撞、一刚体、一勾选IsTrigger

（1）：双方都有碰撞体

（2）：运动的一方必须是刚体

（3）：至少一方勾选IsTrigger触发器



四：碰撞或接触后事件细分为：Enter、Stay、Exit

1：Enter事件表示两物体接触瞬间，会执行一次。

2：Stay事件表示两物体持续接触，会不断执行。

3：Exit事件当两物体分开瞬间，会执行一次。

>  作者：Mask_小文 https://www.bilibili.com/read/cv11848407/ 出处：bilibili。原作者表示禁止转载。

