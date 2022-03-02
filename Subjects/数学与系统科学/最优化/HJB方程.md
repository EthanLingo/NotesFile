

## HJB方程与最优执行问题



[转载自原文链接https://zhuanlan.zhihu.com/p/161632470](https://zhuanlan.zhihu.com/p/161632470)

## 最优控制问题

首先，我们通过一个简单的例子来理解最优控制问题中的设定
一辆汽车在地面上行驶，在时刻t，其位置为 $s(t)$ 、速度为 $v(t)$ 、加速度为 $a(t)$ ，我们可 以通过转方向盘、桌油门/刹车的方式来实现对于汽车的控制。而我们的目标是：通过 控制方向盘、油门和刹车，我们需要使得汽车在最终的T时刻离目的地尽可能近，同
时还要令耗油量较小。
从这个例子可以看出，最优控制问题中的变量分为两种:

1. 状态变量：即反映物体当前状态的变量（例如汽车的位置、速度和加速度），这 种变量是关于时间的变量，因此可以将其记为 $x(t)$
2. 控制变量：即可以人为控制的变量（例如转方向盘、踩油门、刹车），这种变量 也是关于时间的变量，因此可以将其记为 $u(t)$
我们知道控制变量可以引起状态变量的变化，我们称为dynamic，其一般形式为:
$$
\frac{d x(t)}{d t}=a(t, x(t), u(t))
$$
而最优控制问题的目标就是要最大化奖励，或者说最小化损失，损失可以分为两部 分，一部分是过程损失（例如行驶过程中的耗油量），另一部分是终态损失（例如最
终与目的地之间的距离），我们可以将两者分别记为
$$
f(t, x(t), u(t))
$$
和
$$
h(x(T))
$$
那么最优控制问题就可以表示为:
$$
\min _{u} \int_{0}^{T} f(t, x(t), u(t)) d t+h(x(T))
$$

## 动态规划求解

HJB方程采用的是动态规划的思想，因此在正式引入HJB方程之前，我们先简要地介绍
一下如何利用经典动态规划来求解这个最优控制的问题。
动规的原理想必大家都很熟悉了，这里不再责述。考虑到问题中的变量都是连续的， 为了能够求解，首先将 $x(t)$ 和 $u(t)$ 对于时间t离散化，得到序列 $x_{t}$ 和 $u_{t}$, 然后再将 $x_{t}$
和 $u_{t}$ 的取值离散化（比如分别为
$$
x^{1}, \ldots, x^{n}
$$
和
$$
u^{1}, \ldots, u^{m}
$$
），如下图所示。而 $x_{t}$ 和 $u_{t}$ 的关系就变为
$$
x_{t+1}=x_{t}+a\left(t, x_{t}, u_{t}\right)
$$
![img](v2-493258c30b4241371ceb3b6bd909abbb_1440w-20210619111831082.jpg)对变量离散化

在这样一番离散化处理之后，我们就可以很容易地运用动态规划来求解出最优的控制
序列，直接上常规操作，定义价值函数
$$
V\left(t, x_{t}\right)=\min _{u}\left[\sum_{t}^{T} f\left(t, x_{t}, u_{t}\right)+h\left(x_{T}\right)\right]
$$
其含义是从指定的时间和状态出发，最小损失为多少。而按照动态规划的思想，我
们知道t和t+1时刻的价值函数V满足关系
$$
V\left(t, x_{t}\right)=\min _{u_{t}}\left[f\left(t, x_{t}, u_{t}\right)+V\left(t+1, x_{t}+a\left(t, x_{T}, u_{t}\right)\right)\right]
$$
而在末时刻T我们有
$$
V\left(T, x_{T}\right)=h\left(x_{T}\right)
$$
因此只要按照
$$
T-1, T-2, \ldots, 0
$$
的顺序，依次求出 $x_{t}$ 所有取值下的
$$
V\left(t, x_{t}\right)
$$
就可以计算出最小的损失，而沿着最小损失路径的
$$
\left\{u_{t}^{*}\right\}_{t=0, \ldots, T-1}
$$
就是最优控制序列，这样我们就通过经典的动态规划方法求出了离散化后的最优控制
问题。

## HJB方程



前面我们介绍了如何用动规来求解最优控制问题的离散化版本，可是我们知道现实中 的状态和控制变量大多是很复杂的，这就使得如果想要比较精确地求解的话，其离散 化取值的数量需要很大，这就大大增加了复杂度，那么有没有办法直接对原始的连续 问题进行求解呢? 接下来介绍的Hamilton-Jacobi-Bellman方程就解决了这个问题。
现在让我们回到连续版本的最优控制问题当中，状态和控制变量变为函数 $x(t)$ 和 $u(t)$ 我们的求解思路还是动态规划，因此仍然可以定义价值函数：
$$
V(t, x(t))=\min _{u}\left[\int_{t}^{T} f(s, x(s), u(s)) d s+h(x(T))\right]
$$
则根据价值函数的定义，我们有：
$$
\begin{aligned}
V(t, x(t)) &=\min _{u}\left[\int_{t}^{t+d t} f(s,(x(s), u(s)) d s+V(t+d t, x(t+d t))]\right.\\
& \leq \int_{t}^{t+d t} f(s,(x(s), u(s)) d s+V(t+d t, x(t+d t))
\end{aligned}
$$
该不等式对于任意的函数 $u$ 都成立，现在我们对
$$
V(t+d t, x(t+d t))
$$
作泰勒展开，有
$$
V(t+d t, x(t+d t))=V(t, x(t))+\frac{\partial V(t, x(t))}{\partial t} d t+\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t} d t+o(d t)
$$
将它代入，再在不等式两边同时除以 $d t$, 有
$$
0 \leq \frac{\partial V(t, x(t))}{\partial t}+\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t}+\frac{1}{d t} \int_{t}^{t+d t} f(s, x(s), u(s)) d s+\frac{o(d t)}{d t}
$$
令 $d t$ 趋于0，有
$$
\lim _{d t \rightarrow 0} \frac{1}{d t} \int_{t}^{t+d t} f(s,(x(s), u(s)) d s=f(t, x(t), u(t))
$$
则不等式可以写做
$$
0 \leq \frac{\partial V(t, x(t))}{\partial t}+\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t}+f(t, x(t), u(t))
$$
因为不等式对于任意 $u$ 都成立，因此我们有
$$
0 \leq \frac{\partial V(t, x(t))}{\partial t}+\min _{u}\left[\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t}+f(t, x(t), u(t))\right]
$$
另一方面，一定存在一个 $u_{\epsilon} \quad\left(\right.$ 例如最优的 $u^{*}$ ), 对于任意
$$
\epsilon > 0
$$
满足
$$
V(t, x(t))+\epsilon d t \geq \int_{t}^{t+d t} f\left(s,\left(x(s), u_{\epsilon}(s)\right) d s+V(t+d t, x(t+d t))\right.
$$
那么对该式做同样的一系列操作后，可以得到
$$
\epsilon \geq \frac{\partial V(t, x(t))}{\partial t}+\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t}+f\left(t, x(t), u_{\epsilon}(t)\right)
$$
计算不等式右侧的最小值，并令
$$
\epsilon \rightarrow 0
$$
可以得到
$$
0 \geq \frac{\partial V(t, x(t))}{\partial t}+\min _{u}\left[\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t}+f(t, x(t), u(t))\right]
$$
两个不等式都需要满足，因此下面的等式一定成立
$$
0=\frac{\partial V(t, x(t))}{\partial t}+\min _{u}\left[\frac{\partial V(t, x(t))}{\partial x} \frac{d x(t)}{d t}+f(t, x(t), u(t))\right]
$$
将dynamic公式
$$
\frac{d x(t)}{d t}=a(t, x(t), u(t))
$$
代入，可以得到最终的HJB方程
$$
\frac{\partial V(t, x(t))}{\partial t}+\min _{u}\left[\frac{\partial V(t, x(t))}{\partial x} a(t, x(t), u(t))+f(t, x(t), u(t))\right]=0
$$
我们将
$$
\frac{\partial V(t, x(t))}{\partial t}
$$
和
$$
\frac{\partial V(t, x(t))}{\partial x}
$$
分别记为 $\nabla_{t} V$ 和
$$
\nabla_{x} V
$$
并设哈密顿量
$$
H(t, x(t), u(t))=\nabla_{x} V(t, x(x)) \cdot a(t, x(t), u(t))+f(t, x(t), u(t))
$$


则HJB方程可以写做:
$$
\nabla_{t} V\left(t, x(t)+\min _{u}[H(t, x(t), u(t))]=0\right.
$$
可以看出该方程其实就是一个偏微分方程，加上边界条件
$$
V(T, x(T))=h(x(T))
$$
后，求解该方程，就可得到价值函数
$$
V(t, x(t))
$$
的表达式，进而求出最优控制函数 $u^\star$ 的表达式，这样我们就通过HJB方程得到了该最优控制解的解析形式。

对于比较简单的最优控制问题，例如dynamic和损失函数分别是线性和二次函数的情况（一般称作Linear-Quadratic Regulator），该偏微分方程可以得到解析解，但是如果函数形式比较复杂的话，可能就无法求出解析解了，这样就只能靠数值方法来求解方程，也就又回到了之前的离散化情况之中。

## 随机版本的HJB方程

我们前面讨论的都是确定（deterministic）情况下的最优控制问题，即dynamic的形式为 


$$
d x(t)=a(t, x(t), u(t)) d t
$$

然而在很多时候dynamic并不是确定的（如金融问题），因此我们接下来推导一下随 机（stochastic）版本的HJB方程。
在随机情况下，假定dynamic是一个伊藤漂移扩散过程（Itō drift-diffusion process）,
其形式为：
$$
\left\{\begin{array}{l}
d x(t)=\mu(t, x(t), u(t)) d t+\sigma(t, x(t), u(t)) d B_{t}, t \in[s, T] \\
x(s)=y
\end{array}\right.
$$
其中
$$
(s, y) \in[0, T) \times R
$$
$B_{t}$ 是布朗运动 (Brownian motion) 。
为了讨论方便，我们定义
$$
J(s, y ; u(\cdot))=\int_{s}^{T} f(t, x(t), u(t)) d t+h(x(T))
$$
其中 $u(\cdot)$ 代表在$[0,T]$
范围内的一个控制函数，由于引入了随机性，则价值函数可以写做：
$$
V(s, y)=\min _{u} E [J(s, y, u(\cdot))]
$$
那么我们有等式:
$$
V(s, y)=\min _{u}\left\{ E \left[\int_{s}^{s+d s} f(t, x(t), u(t)) d t\right]+V(s+d s, x(s+d s))\right\}
$$
令 $u^{*}$ 是满足上面最小式的函数，即有
$$
V(s, y)= E \left[J\left(s, y ; u^{*}\right)\right]
$$
而由于价值函数的最优性，u" 同样也满足
$$
\begin{aligned}
V(s+d s, x(s+d s)) &=\min _{u} E [J(s+d s, x(s+d s), u(\cdot))] \\
&= E \left[J\left(s+d s, x(s+d s) ; u^{*}\right)\right]
\end{aligned}
$$
该式可以用反证法证明：如果 $u^{*}$ 对于
$$
V(s+d s, x(s+d s))
$$
不是最优的，则存在 $u^{\prime}$, 有
$$
E \left[J\left(s+d s, x(s+d s) ; u^{\prime}\right)\right]< E \left[J\left(s+d s, x(s+d s) ; u^{*}\right)\right]
$$
那么我们可以构造一个函数
$$
u^{\prime \prime}(t)=\left\{\begin{array}{ll}
u^{*}(t) & \text { if } t<s+d s \\
u^{\prime}(t) & \text { if } t \geq s+d s
\end{array}\right.
$$
这样就有
$$
E \left[J\left(s, y ; u^{\prime \prime}\right)\right]< E \left[J\left(s, y ; u^{*}\right)\right]
$$
这就与 $u^{*}$ 最优相矛盾，命题得证。
这样之前等式就可以写为：
$$
\begin{aligned}
V(s, y) &= E \left[\int_{s}^{s+d s} f\left(t,\left(x(t), u^{*}(t)\right) d t+V(s+d s, x(s+d s))\right]\right.\\
&= E \left[\int_{s}^{s+d s} f\left(t,\left(x(t), u^{*}(t)\right) d t+J\left(s+d s, x(s+d s) ; u^{*}\right)\right]\right.
\end{aligned}
$$
类似地，现在需要展开
$$
J\left(s+d s, x(s+d s) ; u^{*}\right)
$$
项，不过考虑到 $x(t)$ 是一个随机过程，这里不能直接做一阶泰勒展开，而是需要使用
伊藤引理（Itō's lemma），对它不了解的同学可以看相关资料，我这里推荐[3]和[4]。
通过伊藤引理可知：
$$
\begin{aligned}
J\left(s+d s, x(s+d s) ; u^{*}\right) &=J\left(s, y ; u^{*}\right)+\frac{\partial J}{\partial t} d s+\frac{\partial J}{\partial x} d x+\frac{1}{2} \frac{\partial^{2} J}{\partial x^{2}}(d x)^{2} \\
&=J\left(t, y, u^{*}\right)+\left(\frac{\partial J}{\partial t}+\frac{\partial J}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} J}{\partial x^{2}} \sigma^{2}\right) d s+\frac{\partial J}{\partial x} \sigma d B
\end{aligned}
$$
先看最后一项，则考虑到随机变量
$$
\frac{\partial J}{\partial x} \sigma
$$
和 $d B$ 相互独立，则期望
$$
E \left[\frac{\partial J}{\partial x} \sigma d B\right]= E \left[\frac{\partial J}{\partial x} \sigma\right] E [d B]=0
$$
而对于
$$
\frac{\partial J}{\partial t} d s
$$
项，有:
$$
E \left[\frac{\partial J}{\partial t} d s\right]=\frac{\partial E [J]}{\partial t} d s=\frac{\partial V}{\partial t} d s
$$
其它微分项也类似，因此有
$$
E \left[J\left(s+d s, x(s+d s) ; u^{*}\right)\right]=V(s, y)+\left(\frac{\partial V}{\partial t}+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right) d s
$$
将其代入上面的等式，有
$$
\begin{aligned}
V(s, y)=& E \left[\int_{s}^{s+d s} f\left(t,\left(x(t), u^{*}(t)\right) d t\right]\right.\\
&+V(s, y)+\left(\frac{\partial V}{\partial t}+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right) d s
\end{aligned}
$$
根据 $u^{*}$ 最优的性质可知，对于任意函数 $u$ ，有
$$
\begin{aligned}
V(s, y) \leq E &\left[\int_{s}^{s+d s} f(t,(x(t), u(t)) d t]\right.\\
&+V(s, y)+\left(\frac{\partial V}{\partial t}+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right) d s
\end{aligned}
$$
类似于上一节的操作，不等式两边都消去
$$
V(s, y)
$$
并都除以 $d s ，$ 且令
$$
d s \rightarrow 0
$$
则有
$$
0 \leq \frac{\partial V}{\partial t}+\left[f(s, y, u(s))+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right]
$$
该不等式对于任意 $u$ 都成立，则有
$$
0 \leq \frac{\partial V}{\partial t}+\min _{u}\left[f(s, y, u(s))+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right]
$$
另一方面，由于存在函数 $u^{*}$, 满足等式:
$$
0=\frac{\partial V}{\partial t}+\left[f\left(s, y, u^{*}(s)\right)+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right]
$$
那么就有
$$
0 \geq \frac{\partial V}{\partial t}+\min _{u}\left[f(s, y, u(s))+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right]
$$
两个不等式都成立，那么唯一的可能就是取等号，则有：
$$
0=\frac{\partial V}{\partial t}+\min _{u}\left[f(s, y, u(s))+\frac{\partial V}{\partial x} \mu+\frac{1}{2} \frac{\partial^{2} V}{\partial x^{2}} \sigma^{2}\right]
$$
将省略掉的自变量加上，重新整理一下，则有：
$$
\frac{\partial V(t, x)}{\partial t}+\min _{u}\left[f(t, x, u(t))+\frac{\partial V(t, x)}{\partial x} \mu(t, x, u(t))+\frac{1}{2} \frac{\partial^{2} V(t, x)}{\partial x^{2}} \sigma^{2}(t, x, u(t))\right]=0
$$
加上边界条件
$$
V(T, x(T))=h(x(T))
$$
 ，这就是随机控制问题的HJB方程。



## 应用例子

> 参考[[最优执行问题基于HJB方程]]



## 总结

这篇文章主要介绍了HJB方程，总的来说，HJB方程用到的还是动态规划的思想，只不过由于变量的连续性，我们需要用偏微分方程来求解；而在面对随机控制问题时，我们需要考虑到不同随机过程的特点，从而得到相应的HJB方程，例如上文的最优执行问题，由于状态变量中多了跳过程，因此HJB方程也要做出相应的改动；如果我们考虑更加复杂的模型，比如考虑市价单、交易数量、交易速率，交易费用等实际情况，只要正确地建立HJB方程，该问题也是可解的。而除了最优执行问题，只要是可以用这个框架来描述的问题，也都是可以用HJB方程来解决的。



## 参考资料

[1] [知乎文章：强化学习第4期：H-J-B方程](https://zhuanlan.zhihu.com/p/58970769)

[2] [Stochastic Control, HJB Equations in Finance](https://link.zhihu.com/?target=https%3A//pdfs.semanticscholar.org/0c65/fd0f29d3498032452a65e50e2661cc6ab97e.pdf)

[3] [知乎文章：布朗运动、伊藤引理、BS 公式（前篇）](https://zhuanlan.zhihu.com/p/38293827)

[4] [知乎文章：布朗运动、伊藤引理、BS 公式（后篇）](https://zhuanlan.zhihu.com/p/38294971)

[5] [Optimal Portfolio Liquidation with Limit Orders](https://link.zhihu.com/?target=http%3A//arxiv.org/pdf/1106.3279)