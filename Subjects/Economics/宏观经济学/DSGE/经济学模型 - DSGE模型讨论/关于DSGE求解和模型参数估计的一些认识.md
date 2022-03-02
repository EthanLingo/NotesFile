其实DSGE最难的地方不在于模型的optimality condition的推导，也不在于寻找Saddle-path。最难的还是在于参数估计，最大似然或者是贝叶斯估计。我下面一条一条地写出来一些认识，希望和大家交流。DSGE是宏观经济学的顶峰难度，不适合数学和经济学基础没有打好的同学，更加不适合自学。这个行业里面一直以来都是老师带学生的传统，基本没有自学成才的例子，至少我没听说过。所以要提醒大家，有导师的，要依靠导师，没有导师的要多跟别人交流学习。

1 . 动态规划是现代宏观的一部分数学基础，但是不是你们想象中那么重要。不要以为学高级宏观就是一直在弄Dynamic programming，这个技术虽然不简单，**但也怎么也算不上现代宏观或者DSGE的核心技术**。完全没有必要画大把的时间在这个上面，DSGE不依靠它而存在。就目前的DSGE研究来看，用dynamic programming的地方就是对Euler equation分析求解用得比较多，其他地方基本都不用。更别说Dynamic programming的数值模拟了，除了上课的时候用，真实研究里面基本不用。

2 . DSGE不是非要线性化才能搞，关键看你的目的是什么，如果你就是做模拟和impulse response，你没有必要自己动手去对数线性化，Dynare可以帮你做。但是要知道一点，我们对付“线性动力系统”的知识远远比“非线性动力系统”认识要深和宽泛。非线性动力系统对付起来很麻烦，占用大量的计算时间，并且准确性低，对初始条件非常敏感。**非线性微分方程组**里面一个重要话题就是混沌理论，用在气象学上面的一个著名例子就是“蝴蝶效应”。如果你学过研究生级别的微分方程课程，就应该知道非线性微分方程一般我们都要做泰勒级数一次展开，其实DSGE的线性化本质思想也是来自于那里。

3 . 和所有动力一样，一个线性系统必须要stable solution，我们才能预测和模拟。linear rational expectation模型求解之后找到一个stochastic difference equation system被叫做policy and transition function。这个系统是描述整个DSGE模型动态性的一个终极解释，所有endogenous variables都会沿着一个saddle-path（鞍部线） 移动。在微积分上面我们知道有一种saddle point，通过Hessian matrix的行列式检验之后可以发现，既不是最大值，也不是最小值，如图：
![Saddle_point.png](084948s4ffzi5vlmp5i55p-20210325205718505.png) 
这个红色的点，就是saddle point。但微积分教材没有说一个关键的问题: **这个saddle point是一个equilibrium。**这是一个基本的物理学认识，如果这个曲面绝对光滑，无摩擦力，那么你放一个球在红色点的地方，它会静止在那个地方不动，因为这里是力量均衡点，重力和支撑力刚好相反方向G=F，一个垂直向上，一个垂直向下。经济学的均衡思想最开始就是从物理上面学过来，因为市场供给和需求就是两种力量，如果相等了就是均衡了。

还有，看下面这个图，钟摆。钟摆有两个equilibrium，这个图只画了一个，这个垂直向下的equilibrium叫做global equilibrium。另外一个均衡点是，钟摆垂直向上，这个时候钟摆同样会静止不动，这个equilibrium就是saddle point equilibrium。它对初始条件非常敏感，已经敏感到了初始条件必须是垂直向上（刚好就是equilibrium），才能保持均衡。
![300px-Simple_gravity_pendulum.svg.png](085843sa0trisss3lalyag-20210325205717779.png) 

我上面之所讲这么多，就是要告诉你一点，DSGE的解实际上就是一个动态saddle point，所以我们叫做saddle path。它往往存在于高纬度，所以我们一般不画图来解释。saddle path有时候对初始条件敏感，有时候不太敏感，这都要看情况，这里和**李雅普诺夫**的稳定性描述有点相似，但是saddle path并没有一个准确的basin of attraction的数学描述。

4 . DSGE的求解方法很多，Blachard-Kahn是行业标准，检查单位元之外的特征值数量是否与nonpredetermined variables的数量是否相等，其实这是个基本的差分方程常识，我在之前的帖子解释了很多次了。BK方法的弱点在于出现了Singularity就没法解了，所以我们有其他方法Sims'，Klein's之类的，用泛用性很高的Schur decompostion或者QZ decomposition就解决问题了。可以说，这是DSGE里面一个特别简单的版块，除了一些技术性知识之外，没有什么对智力有挑战的地方。

5 . Dynare是作为一个行业标准而出现的，每年的Dynare年会都立足于推广DSGE和Dynare在现代宏观经济学上的使用。你可以认为Dynare是个黑盒子，但它实际上还偏不是黑盒子。因为大部分执行程序都是用Matlab编写的，如果你能看懂，那些"xxx.m"程序都是可以打开来学习的。当然你不想把DSGE做为研究方向的话， 只学习Dynare的应用就已经够难了，更别说看懂内部构造了。所以对于大多数同学来说，Dynare仍然是保持着一种黑盒子的状态，包括对我来说一样。

6 . 同时因为state-space 模型是一种泛用性极高的线性系统，里面的transition equation刚好就是DSGE模型的解(transition function)，这个极其巧妙的特点是当年Sargent发现的，同时意识到了一点，只要能写成state-space 模型，就能推导出maximum likelihood的函数形式。所以我们能用Kalman filter来数值模拟出maximum likelihood。

7 . 最大似然估计很容出现identification的问题，简单来说就是不同的两套参数，在同一种structural model的情况下回产生同一种probability distribution。这样就导致似然函数的顶端是平的。下面这个图是用Dynare做的ML估计，一个简单的新凯恩斯模型。看Sigma的log-likelihood function，顶端是平的，这就一个identification问题。所以必须要用prior来加权重，所以采用Bayesian有绝对优势。
![ML_Identi.jpg](093829177ddsnsq7u80adn-20210325205717938.jpg) 

8 . 关于Bayesian estimation，要说的就太多了。这个帖子装不下，以后再写。