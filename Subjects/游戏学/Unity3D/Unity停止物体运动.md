---
title: Unity停止物体运动
authors: Ethan Lin
year:
tags:
  - 内容/Unity 
  - 来源/转载 
---


# Unity停止物体运动





代码如下：
```c#
[SerializeField]
private GameObjecct m_Soccer;

m_Soccer.GetComponent<Rigidbody>().constraints = RigidbodyConstraints.FreezeAll;//第一步，让刚体停下来(“冻结”位移、旋转)
m_Soccer.GetComponent<Rigidbody>().constraints = RigidbodyConstraints.None;//第二步，让刚体能被后续控制做运动

//注：RigidbodyConstraints这个枚举对应刚体的某个方向上的位移或者旋转增量为零（None除外，不加限制），有时间的可以测一测
```

最近又有点心得，得到另一个方法：
```c#
m_Soccer.GetComponent<Rigidbody>().velocity = Vector3.zero;//运动速度为0，自然也就不运动了，这里的velocity是一个矢量
```

又研究出了一个方法：
```c#
void Update () {
        if (Input.GetKey(KeyCode.Q))
        {
            GetComponent<Rigidbody>().Sleep();//停止运动
        }
        else
        {
            GetComponent<Rigidbody>().WakeUp();//开始运动
        }
	}
```

呃，好像还忘了一个，补上：
```c#
//按下Q键切换运动状态
if (Input.GetKeyDown(KeyCode.Q))
        {
            GetComponent<Rigidbody>().isKinematic = !GetComponent<Rigidbody>().isKinematic;
        }
        //isKinematic ：是否遵循运动学，为true后可以自定义运动轨迹。
```

————————————————
> 版权声明：本文为CSDN博主「_thought」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
[原文链接：](https://blog.csdn.net/lm_mt/article/details/72734449)