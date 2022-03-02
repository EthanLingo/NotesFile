

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
![img](v2-493258c30b4241371ceb3b6bd909abbb_1440w.jpg)对变量离散化

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

> 参考[[HJB方程]]

## 最优执行问题

最优执行（optimal execution）问题是金融领域中一个重要的实际问题，我们知道，金融产品的价格是通过**市场交易**得到的。以股票为例，如果有一个股票持有者想要卖出一定数量的股票，而同时有另一方愿意以p元的价格购买，那么这笔交易就达成了，这支股票的当前价格就为p，然而这里面却存在一个问题——**没有考虑股票的交易数量**，如果卖方想要卖出股票的量很大，那么可能一个单独的买方并没有办法全部“吃”下，这时就需要其他的买方也参与进来了，如果这些买方的意愿价格小于p，那么这部分成交的股票价格就会小于p（如下图所示），从而导致了这样一种现象：**如果想要短时间卖出大量股票，其成交价格并不一定都是当前价格，会有部分股票的价格更低**，而类似地，大量买入股票也会有价格更高的情况。可以看到，这种现象使得**大规模股票交易的成本更高**，因此为了降低成本，我们需要**将大规模的交易单拆分成若干个小规模的订单**，在一定时间内根据市场情况合理地分批下单，这就是最优执行问题。

![img](v2-01785567c66b4286f8485c68b1c439e9_1440w.jpg)抛售大量的股票会产生额外的成本

上面介绍的是最优执行问题的背景和基本思想，现在具体来看这个问题，假设我们在初始的 0 时刻持有的股票数量为 $q(0)$ ，我们的目标是想要在 T 时刻之前将所持有的的股票全部卖出，而卖出股票的方式有两种：**市价单**（market order）和**限价单**（limit order），对它们不了解的同学可以看一些limit order book的相关参考资料，这里就不过多介绍了，简单地说，市价单是不在乎价格，要求立即成交的交易订单，而限价单则要在满足特定价格的情况下才可以成交，因此在交易过程中，**市价单只需要指定买入或卖出股票的数量，而限价单除了数量还需要指定交易价格**。

可以看出，其实最优执行问题可以看做一个最优控制问题，我们可以把**当前股票价格、当前持有的股票数量、已得到的现金量等**看做是状态变量，将**关于市场单以及限价单的操作**看做是控制变量，而最终的目标就是**尽量在T时刻前清空股票、同时最大化现金收益**。

接下来我们就利用HJB方程来解决该问题，这部分内容主要来自于论文[Optimal Portfolio Liquidation with Limit Orders](https://link.zhihu.com/?target=http%3A//arxiv.org/pdf/1106.3279)。

这里先说一下整体的思路，我们把实际问题化简一下，**只考虑限价单的操作**：在某一个

时刻
$$
t+\Delta t
$$
我们先将未执行的限价单撤回，重复之前的步骤继续挂单，直到卖完所有股票或者
到达最终的T时刻为止。这样只要还有股票没有卖完，我们在每一时刻都会重复地挂 单和撤单，从而不断地更新限价单价格。
有了整体思路之后，就可以对问题进行建模，具体如下:
。 股票价格 $S(t)$ : 看做是带漂移的布朗运动
$$
d S(t)=\mu d t+\sigma d B_{t}
$$
那么限价卖单价格（ask price) 可以表示为
$$
S^{a}(t)=S(t)+\delta(t)
$$
其中价差
$$
\delta(t) \geq 0
$$
。 当前持有量 $q(t)$ :
$$
q(t)=q(0)-N(t)
$$
其中
$$
N(t)
$$
是到目前t时刻为止卖出的股票数量，它是一个跳过程（jump process），比如说
可以是泊松过程，其强度为 $\lambda$ ，即单位时间内卖出股票的平均数量为 $\lambda$ ，显然 $\lambda$
应该与价差 $\delta$ 有关，这里我们认为 $\lambda$ 满足
$$
\lambda(\delta)=A e^{-k \delta}
$$
- 现金数量
$$
X(t)
$$
即截止到目前卖出股票得到的现金数，可以知道其dynamic为
$$
d X(t)=(S(t)+\delta(t)) d N(t)
$$






- 效用函数：我们目标是**在T时刻卖光股票的同时还要获得尽量多的现金**，因此效用函数为 
  $$
  \left[-e^{-\gamma X(T)+q(T)(S(T)-b)}\right]
  $$
  其中 $^{\gamma}$ 是权衡系数， $b$ 是一个常数，代表处理剩余股票的成本。可以看出这个 效用函数其实就是一个奖励函数，当最终的T时刻现金
  $$
  X(T)
  $$
  )越大或者剩余股票数 $q(T)$ 越小时，该函数的值越大。
  现在我们将这些变量对应到控制问题当中
  - 控制变量：根据设定，我们在每一时刻都要撤回已有的限价单，并挂出新的限价
  单，单子的数量等于当前持有的股票数量，因此我们唯一的控制变量的就是价差 $\delta(t)$, 不需要再额外考虑下单撤单时间、下单撤单量等变量。
  - 状态变量：已持有的现金
  $$
  X(t)
  $$
  、剩余的股票数量 $q(t)$ 以及当前的股票价格 $S(t)$
  - 优化目标：最大化效用函数，为了与上文最小化损失函数相一致，我们写成
  $$
  \min _{\delta} E \left[e^{\gamma X(T)+q(T)(S(T)-b)}\right]
  $$
  注意到该问题中只有末态损失，并没有过程损失。

  完成对应之后，我们就可以用上面的HJB方程来解决这个问题，不过还不能直接套
  用，因为之前推导时我们只考虑了状态变量的dynamic是伊藤漂移扩散过程的情况，而 这里却还有一个额外的跳过程 $q(t)$, 因此我们需要再做一点小的改动。
  回忆上一节的证明过程，价值函数为：
  $$
  V(t, x, q, s)=\min _{\delta} E\left[e^{-\gamma X(T)+q(T)(S(T)-b)}\right]
  $$
  还是同样的操作，对于最优的 $\delta^{*}$, 考虑到过程损失为0，我们有
  $$
  V(t, x, q, s)=E\left[J\left(t+d t, x(t+d t), q(t+d t), s(t+d t) ; \delta^{*}\right)\right]
  $$
  对J做展开：
  $$
  \begin{array}{c}
  J\left(t+d t, x(t+d t), q(t+d t), s(t+d t) ; \delta^{*}\right) \\
  =J\left(t, x(t), q(t), s(t) ; \delta^{*}\right)+\frac{\partial J}{\partial t} d t+\frac{\partial J}{\partial s} d s+\frac{\partial^{2} J}{\partial s^{2}} d s+\frac{\partial J}{\partial x} d x+\frac{\partial J}{\partial q} d q
  \end{array}
  $$
  前四项和之前是一样的，我们重点来分析后两项
  $$
  \frac{\partial J}{\partial x} d x+\frac{\partial J}{\partial q} d q
  $$
  根据模型设定，我们有
  $$
  d x=(S(t)+\delta(t)) d N
  $$
  和
  $$
  d q=-d N
  $$
  那么
  $$
  \begin{aligned}
  \frac{\partial J}{\partial x} d x+\frac{\partial J}{\partial q} d t &=\frac{\partial J}{\partial x}(s+\delta) d N-\frac{\partial J}{\partial q} d N \\
  &=\left[\frac{\partial J}{\partial x}(s+\delta)-\frac{\partial J}{\partial q}\right] d N
  \end{aligned}
  $$

根据多元微分学的知识，我们知道
$$
\left[\frac{\partial J}{\partial x}(S+\delta)-\frac{\partial J}{\partial q}\right]
$$
其实就是一个方向导数，我们可以将它写做
$$
\frac{\partial J}{\partial x}(s+\delta)-\frac{\partial J}{\partial q}=\frac{J\left(t, x+\Delta\left(s+\delta^{*}\right), q-\Delta, s ; \delta^{*}\right)-J\left(t, x, q, s ; \delta^{*}\right)}{\Delta}
$$
考虑到我们持有的股票数量是离散的，只能一股一股地卖，因此 $\Delta$ 只能是正整数，这
里取1，则原式可以写为
$$
\frac{\partial J}{\partial x} d x+\frac{\partial J}{\partial q} d t=\left[J\left(t, x+s+\delta^{*}, q-1, s ; \delta^{*}\right)-J\left(t, x, q, s ; \delta^{*}\right)\right] d N
$$
现在求期望，注意到随机变量
$$
J\left(t, x+s+\delta^{*}, q-1, s ; \delta^{*}\right)-J\left(t, x, q, s ; \delta^{*}\right)
$$
和 $d N$ 是相互独立的，再由跳过程
的定义有
$$
E[d N]=\lambda\left(\delta^{*}\right) d t=A e^{-k \delta^{*}} d t
$$
则
$$
\begin{aligned}
E\left[\frac{\partial J}{\partial x} d x+\frac{\partial J}{\partial q} d t\right] &=E\left[\left(J\left(t, x+s+\delta^{*}, q-1, s ; \delta^{*}\right)-J\left(t, x, q, s ; \delta^{*}\right)\right) d N\right] \\
&=E\left[J\left(t, x+s+\delta^{*}, q-1, s ; \delta^{*}\right)-J\left(t, x, q, s ; \delta^{*}\right)\right] E[d N] \\
&=\left[V\left(t, x+s+\delta^{*}, q-1, s\right)-V(t, x, q, s)\right] A e^{-k \delta^{*}} d t
\end{aligned}
$$
将这两项的期望带回到原先的展开式，有
$$
\begin{aligned}
V(t, x, q, s)=& V(t, x, q, s)+\left(\frac{\partial V}{\partial t}+\mu \frac{\partial V}{\partial s}+\frac{1}{2} \sigma^{2} \frac{\partial^{2} V}{\partial s^{2}}\right) d t \\
&+\left(\left[V\left(t, x+s+\delta^{*}, q-1, s\right)-V(t, x, q, s)\right] A e^{-k \delta^{*}}\right) d t
\end{aligned}
$$
接下来的操作就和之前一样了，通过分别构造大于等于0和小于等于0的两个不等式,
我们可以得到该问题下的HJB方程为
$$
\frac{\partial V}{\partial t}+\mu \frac{\partial V}{\partial s}+\frac{1}{2} \sigma^{2} \frac{\partial^{2} V}{\partial s^{2}}+\min _{\delta}\left\{A e^{-k \delta}[V(t, x+s+\delta, q-1, s)-V(t, x, q, s)]\right\}=0
$$
边界条件为：
$$
\left\{\begin{array}{c}
V(T, x, q, s)=e^{-\gamma x+q(s-b)} \\
V(t, x, 0, s)=e^{-\gamma x}
\end{array}\right.
$$
对这个偏微分方程进行求解，就可以得到价值函数
$$
V(t, x, q, s)
$$
进而得到当前的最优价差
$$
\delta^{*}(t)
$$
由于求解过程以及最优解的形式都比较复杂，这里就不具体写了，想看的同学可以 看论文原文。
最后简单说一下实验，我们知道，实际市场中的交易价格是离散的，因此在我们报的 价格实际上是离理论最优价格最近的tick价格; 另外，考虑到订单的优先级，频繁地挂
单和撤单会降低成交的概率，因此更新限价单的时间间隔 $\Delta t$ 不能太小，当一笔限价 单挂出之后，只有当发生交易或订单停留时间超过 $\Delta t$ 之后，我们才会更新订单。
首先我们根据历史的交易数据估计出模型中
$$
\mu, \sigma, A, k
$$
等参数，然后通过该HJB方程的解析解求出最优报价，最后按照模型给出的报价来**模拟**整个执行过程，下图是一个例子，模拟的是模型于2010年11月8日14:00-16:00，在法国安盛（AXA）股票上的交易过程。

![img](v2-739fa39f9336eff61fd4d764c37cacb4_1440w.jpg)模型的执行过程，其中粗线是模型报价，实线是市场的最佳卖价（best ask quotes），虚线是市场的最佳买价（best bid quotes）

![img](v2-9e3751be9a72fde0da700e64c19aadf9_1440w.jpg)左图是持有的股票数量，右图是现金量

## 总结

这篇文章主要介绍了HJB方程以及它在金融领域的最优执行问题上的一个应用，总的来说，HJB方程用到的还是动态规划的思想，只不过由于变量的连续性，我们需要用偏微分方程来求解；而在面对随机控制问题时，我们需要考虑到不同随机过程的特点，从而得到相应的HJB方程，例如上文的最优执行问题，由于状态变量中多了跳过程，因此HJB方程也要做出相应的改动；如果我们考虑更加复杂的模型，比如考虑市价单、交易数量、交易速率，交易费用等实际情况，只要正确地建立HJB方程，该问题也是可解的。而除了最优执行问题，只要是可以用这个框架来描述的问题，也都是可以用HJB方程来解决的。



## 参考资料

[1] [知乎文章：强化学习第4期：H-J-B方程](https://zhuanlan.zhihu.com/p/58970769)

[2] [Stochastic Control, HJB Equations in Finance](https://link.zhihu.com/?target=https%3A//pdfs.semanticscholar.org/0c65/fd0f29d3498032452a65e50e2661cc6ab97e.pdf)

[3] [知乎文章：布朗运动、伊藤引理、BS 公式（前篇）](https://zhuanlan.zhihu.com/p/38293827)

[4] [知乎文章：布朗运动、伊藤引理、BS 公式（后篇）](https://zhuanlan.zhihu.com/p/38294971)

[5] [Optimal Portfolio Liquidation with Limit Orders](https://link.zhihu.com/?target=http%3A//arxiv.org/pdf/1106.3279)