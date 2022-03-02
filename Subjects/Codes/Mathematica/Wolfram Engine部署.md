
#来源/转载 
#指南 


[[Wolfram Engine]]
[[部署Wolfram Engine]]
[[部署]]





# Mathematica白嫖全过程

## 在线使用

[https://www.wolframalpha.com/input/](https://www.wolframalpha.com/input/)

-   优势: 方便
-   缺陷: 算力不够

## 安装记录

官方提供了个人非商用engine, 因此可以直接选择白嫖

-   官网注册账户并且绑定邮箱(我也绑定了手机号) [https://www.wolfram.com](https://www.wolfram.com/)
    
-   下载. 建议用linux版本, 因为win版本下载得到的只是一个小小的下载器, 后面会一直报网络错误 [https://www.wolfram.com/engine/](https://www.wolfram.com/engine/)
    
-   安装. 一定要`root`权限, 否则失败  
    `sudo ./WolframEngine_12.2.0_LIN_CN.sh`
    
-   其实安装好了之后到这一步几就可以用了, 在终端输入  
    `wolframscript`  
    根据提示, 输入自己的账号密码就可以激活, 问题是这样用起来没有图形界面
    

## 搭配jupyter

这是WolframLanguageForJupyter提供的说明  
[https://github.com/WolframResearch/WolframLanguageForJupyter](https://github.com/WolframResearch/WolframLanguageForJupyter)

配合`jupyter`就等于有了图形界面, 如果只是简单计算, 不需要图形界面, 可以跳过这一步

下面以`ubuntu`系统为例,

1.  jupyter的安装,  
    安装pip  
    `sudo apt install python3-pip`  
    安装jupyter  
    `pip install jupyter -i https://pypi.tuna.tsinghua.edu.cn/simple --trusted-host pypi.tuna.tsinghua.edu.cn`
    
2.  配置,
    
    ```
    git clone https://github.com/WolframResearch/WolframLanguageForJupyter.git
    
    cd WolframLanguageForJupyter
    
    ./configure-jupyter.wls add
    ```
    
    如果没安装`git`的话, 下载这个 [https://github.com/WolframResearch/WolframLanguageForJupyter/archive/refs/tags/v0.9.2.zip](https://github.com/WolframResearch/WolframLanguageForJupyter/archive/refs/tags/v0.9.2.zip) 再解压, 也是一样的.
    
3.  爽快运行
    
    终端输入`jupyter notebook`
    

## 安装之后

查看激活码的办法

官网的方案  
[https://reference.wolfram.com/language/workflow/FindYourActivationKey.html](https://reference.wolfram.com/language/workflow/FindYourActivationKey.html)  
比较简单的有两个方案:

1.  终端运行`wolframscript`, 然后在输入行中输入  
    `$ActivationKey`  
    就可以得到结果
    
2.  登入账号之后, 点击 [https://www.wolframcloud.com/users/user-current/activationkeys](https://www.wolframcloud.com/users/user-current/activationkeys)
    

## 一些wolframscript测试

计算三维有界奇异积分项

∫02∫02∫021xy+xz+yzdxdydz∫02​∫02​∫02​xy+xz+yz1​dxdydz

该积分用Python的第三方包Sympy暂时没算出结果, 当然也许是个人使用方法的问题, 但是用Mathematica可以想到轻松算出答案.

```java
Integrate[1/(x*y+y*z+x*z),{x,0,2},{y,0,2},{z,0,2}]

得到的积分值为

2pi(pi- 6 i Log[2]) - 6polyLog[2,4]

或

6(2(Log[2])^2+PolyLog[2,1/4])
```

---

小技巧, 在命令行后面加上 `// Texform` 可以美化成`Mathjax`公式输出

例如

```j
1/(2x) // TeXForm
```

会得到

12x2x1​

---

本文来源 [https://kz16.top/mma.html](https://kz16.top/mma.html)  
主页地址 [https://kz16.top/](https://kz16.top/)  
仅供参考，部分漏洞在所难免  
欢迎转载，转载请指明来源，  
请勿用于商业