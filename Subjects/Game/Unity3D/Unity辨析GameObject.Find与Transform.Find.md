# Unity辨析GameObject.Find与Transform.Find


---
title: Unity辨析GameObject.Find与Transform.Find
authors: Ethan Lin
year:
tags:
  - 内容/Unity 
---



在普通情况下，GameObject.Find以及Transform.Find和Transform.FindChild是可以做到相同的功能，但是他们有本质上的区别，望新手谨记：


GameObject.Find是遍历整个当前场景，挨个查找，效率偏低，非特殊情况一般不要使用

  

Transform.Find是只查找自己本身以及自己的子对象，效率比较高，用途比较大

  

Transform.FindChild是跟Transform.Find一样的用法，但是官方不建议继续使用，用Transform.Find代替之

  

那这么说，是不是代码里面就可以经常反复的使用Transform.Find呢？   
答案肯定是否定的，因为即使效率太高，也是会有性能消耗的   

正确的用法，如果在一个类里面会多次用到某一个对象，建议用一个变量保存起来