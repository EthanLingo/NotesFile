# 查看macos的电池损耗

tags: #日期/2022-10-04 #类型/笔记 #类型/解决 #来源/转载 

> 来源：[如何查询Mac电池损耗？(Mac使用小技巧，有空会更新） - 知乎](https://zhuanlan.zhihu.com/p/261725163)

首先Mac系统搜索终端，

在终端粘贴下面命令：

ioreg -rn AppleSmartBattery | grep -i capacity

回车。

你会见到下面文字：

![](https://pic4.zhimg.com/80/v2-c40c89197778ac0d6d7f25bafdfe105b_1440w.webp)

其中，Maxcapacity是你的电池目前的最大可用容量。Designcapacity是电池设计容量，也就是电池全新时候的容量。比如我的Mac电池的最大可用容量是4640，电池设计容量是5770，那么我的电池损耗是4640➗5770=0.8041,也就是80%左右。最后这个过程需要你手动计算。