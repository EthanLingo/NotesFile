---
title: 辨析C sharp之类型Array、ArrayList、List
authors: Ethan Lin
year: 2022-12-20 
tags:
  - 日期/2022-12-20 
  - 类型/笔记 
  - 类型/辨析 
  - 内容/csharp 
  - 内容/数据结构 
  - 来源/转载 
---


# 辨析C sharp之类型Array、ArrayList、List





1.Array和ArrayList的区别。

不同点：
（1）Array类型的变量在声明的同时必须进行实例化(至少得初始化数组的大小)，而ArrayList可以只是先声明。
如：
int[] array = new array[5];
或 int[] array = {1,2,3,4,5};
或 ArrayList myList = new ArrayList();
这些都是合法的，而直接使用 int[] array;是不行的。

（2） Array只能存储同构的对象，而ArrayList可以存储异构的对象。
同构的对象：指类型相同的对象，若声明为int[]的数组就只能存放整形数据,string[]只能存放字符型数据,但声明为object[]的数组除外。
异构的对象：指任何不同类型的对象（因为它里面存放的都是被装箱了的Object型对象，实际上ArrayList内部就是使用"object[] _items;"这样一个私有字段来封装对象的）。

（3） 在CLR托管对中的存放方式
Array是始终是连续存放的，而ArrayList的存放不一定连续。

（4）初始化大小
Array对象的初始化必须只定指定大小，且创建后的数组大小是固定的。

ArrayList的大小可以动态指定，其大小可以在初始化时指定，也可以不指定，也就是说该对象的空间可以任意增加。

（5） Array不能够随意添加和删除其中的项，而ArrayList可以在任意位置插入和删除项。

相同点：
（1） 都具有索引(index),即可以通过index来直接获取和修改任意项。
（2）他们所创建的对象都放在托管堆中。
（3） 都能够对自身进行枚举(因为都实现了IEnumerable接口)。

2. ArrayList和List的区别。

不同点：

（1）在编程语言中ArrayList类是.Net Framework提供的用于数据存储和检索的专用类。List 类可以简单视之为双向连结串行，以线性列的方式管理物件集合。List类是ArrayList类的泛型等效类。

（2）ArrayList可以插入不同类型的数据，而List不能。ArrayList会把所有插入其中的数据都当作为object类型来处理，这其中存在装箱与拆箱的操作，会对系统造成性能上的损耗。List需要声明其数据的对象类型，声明后插入其他类型数据就会报错，且不能通过编译。

（3）在使用ArrayList中的数据来处理问题的时候，很可能会报类型不匹配的错误，即ArrayList不是类型安全的。而List已经声明过其数据的对象类型，是类型安全的，避免了类型安全问题与装箱拆箱的性能问题。

（4）ListArray就可以被构造。而List不能被构造，但可以为List创建一个引用。

相同点：

（1）ArrayList与List都继承了IList接口，可以很方便的进行数据的添加，插入和移除，且List的大部分用法都与ArrayList相似。
————————————————
> 版权声明：本文为CSDN博主「水箭龟gd」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/weixin_57752568/article/details/118072034
