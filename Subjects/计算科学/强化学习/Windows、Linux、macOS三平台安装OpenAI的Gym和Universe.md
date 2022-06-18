tags: #来源/转载 
#教程 

[[部署环境]]
[[OpenAI]]
[[强化学习]]
[[强化学习实战]]
[[Python]]





# Windows、Linux、macOS三平台安装OpenAI的Gym和Universe




![img](https:////upload-images.jianshu.io/upload_images/1783214-6ff39928e0bc17bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/900)

OpenAI 的 Gym 和 Universe

> 作者 谢恩铭，公众号「程序员联盟」（微信号：coderhub）。
> 转载请注明出处。
> 原文：https://www.jianshu.com/p/536d300a397e

## 内容简介

------

1. OpenAI 和艾隆·马斯克
1. 什么是 Gym 和 Universe
1. 什么是 Anaconda
1. 什么是 Docker
1. Linux 安装 Gym 和 Universe
1. 写程序测试 Gym 和 Universe
1. Windows 安装 Gym 和 Universe
1. macOS 安装 Gym 和 Universe
1. 总结

## 1. OpenAI 和艾隆·马斯克

------

OpenAI 这个非盈利的人工智能研究公司在业界很有名，毕竟它是由人称「现实版钢铁侠」的 Elon Musk（艾隆·马斯克。恩，不是 马克思。大学里有人挂过「马哲」（马克思主义哲学）吗？）启动的项目。

2015 年 12 月 12 日，Elon Musk 在 Twitter 上宣布正式启动非盈利人工智能项目 OpenAI。

OpenAI 的目标是「推动数字智能的发展，同时不被财务回报所限制，从而造福整个人类」。Open 是英语「开放的」之意，AI 是 Artificial Intelligence（人工智能）的缩写。从其名字可以知悉，OpenAI 的愿景是把 AI 技术开放给全人类。OpenAI 强烈建议研究人员公开他们的研究成果，包括论文、博文、代码和专利，与世界共享。

Elon Musk 是 OpenAI 的联合创始人之一，也是特斯拉公司（Tesla，就是造电动汽车的公司，现在也涉足很多其他领域）的 CEO 兼产品架构师，又是太空探索技术公司（SpaceX，就是发射了不少火箭的那个公司）CEO 兼 CTO，还是 PayPal 公司的创始人之一，是科技界的大红人，反正就是人生开挂就对了，人类已经不能阻止马斯克了。

扯一个有趣的事：据说电影《钢铁侠》（Iron Man）是以 Elon Musk 的故事为蓝本（因为 Elon Musk 的经历很像钢铁侠，他的具体人生历程大家可以自行搜索）。扮演电影中的发明家 托尼·斯塔克（Tony Stark）的 小罗伯特.唐尼 向导演建议，为演好角色最好能和马斯克聊聊。

![img](https:////upload-images.jianshu.io/upload_images/1783214-6cbf18bd0dcc08d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/268)

Elon Musk

> 近日，OpenAI 发布公告称，Elon Musk 宣布退出董事会，原因是随着特斯拉更专注于 AI 技术，需要避免与 OpenAI 在未来可能存在的利益冲突。
> 虽然并未说明具体的「冲突要点」，但能想到的是比如人才方面的竞争，OpenAI 一开始就从 Google、Facebook 等科技巨头那里挖人，如今特斯拉将注意力放在 AI 技术之后，人才流动难免遭受非议。OpenAI 的研究员 Andrej Kapathy 跳槽到特斯拉就是一例。
> 不过，根据公告内容，此次退出董事会大多是马斯克为了避嫌。事实上，他还有半只脚留在了 OpenAI
> ：马斯克将继续担任 OpenAI 顾问，继续提供资助和建议。

OpenAI 的官网是 [https://openai.com](https://links.jianshu.com/go?to=https%3A%2F%2Fopenai.com)

可以看到 OpenAI 的官网制作很精美，给人一种很酷的感觉：

![img](https:////upload-images.jianshu.io/upload_images/1783214-ef37fa2ae91a3a75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

OpenAI 官网

据说 Elon Musk 创办 OpenAI 的一个比较主要的原因是因为他是持「AI 威胁论」的人（与他类似的还有史蒂芬.霍金 博士，等。和他持相反意见（「AI 有用论」）的有 Facebook 的 CEO 马克.扎克伯格）。Elon Musk 觉得有必要让人们都了解一下 AI （人工智能），以防止未来可能出现的「AI 灭世」。

OpenAI 已经在人工智能领域做出了不少贡献，比如2017 年夏天开发出了在 Dota 2（以前大学时我也玩过不少的 Dota 1 版本，那时候同寝室的室友们一起去开黑还是很有趣的。Dota 2 我没有玩过，因为我后来不玩游戏转而潜心学习编程了。恩恩，我还是很乖的（小编，我看你的脸皮比城墙根还厚 :P ）。现在我觉得编程比玩游戏更有趣，特别是现在的人工智能编程，也可以实现让 AI 来帮你玩游戏）中击败人类最强选手的 AI 程序：

![img](https:////upload-images.jianshu.io/upload_images/1783214-6233e4fa1c081357.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

OpenAI 开发的人工智能对战 Dota 2 顶尖玩家Dendi

关于这个轰动的大新闻的报道（内有视频）在 [https://blog.openai.com/dota-2/](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.openai.com%2Fdota-2%2F)

当时世界最强影魔（Shadow Fiend，简称 SF，一直是 Dota 里面大受欢迎的英雄，是很考验操作的英雄）使用者之一的 Dendi 操作的影魔在中路 1v1 被 OpenAI 开发的人工智能程序操作的影魔拿到了 一血（First Blood）、二血、三血... 额，直接认输了（Dendi 内心 OS ：没想到宝宝被虐了...）。

赛前 Dendi 还是抱着比较轻松的心态，结果人工智能程序非常聪明（不过一方面也是因为人工智能程序知晓游戏的一切元素，包括距离，所以可以极其精准地释放影魔的「三连压」），令他大为惊异。 而且，人工智能控制的影魔会卡位，长距离追杀，补兵，击杀对方买的运输小动物，假装抬手和取消攻击，甚至还做出了顶塔强杀这样的惊人举动。

OpenAI 在机器学习方面关注两个关键点：无监督学习（Unsupervised Learning）和强化学习（Reinforcement Learning），它的一些重要的项目基本都开源在 Github 上：[https://github.com/openai](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai)

比如：

- Gym ：这篇文章之后会介绍。[https://github.com/openai/gym](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Fgym)
- MuJoCo-py ：用 Python 来使用
  MuJoCo 这个物理引擎。[https://github.com/openai/mujoco-py](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Fmujoco-py)
- RoboSchool ：OpenAI 开源的机器人模拟软件。基于 Gym。[https://blog.openai.com/roboschool](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.openai.com%2Froboschool)
- Baselines ：基于 Gym 和 TensorFlow 实现了经典的（深度）强化学习算法。[https://github.com/openai/baselines](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Fbaselines)
- Universe ：这篇文章之后会介绍。[https://github.com/openai/universe](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Funiverse)

这篇文章我们主要讲其中的 Gym 和 Universe 两个开发环境的安装。

## 2. 什么是 Gym 和 Universe？

------

OpenAI Gym 是一个用于开发和比较 RL（Reinforcement Learning（强化学习））算法的工具包，它包括一系列不断增长、完善的环境，还提供可以用于比较和评估算法的平台。

Gym 与其他的数值计算库兼容，如 TensorFlow 或者 Theano。主要支持的是 Python 语言。

Gym 的官网是 [https://github.com/openai/gym](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Fgym)

Gym 的各种环境在这里 [https://gym.openai.com/envs](https://links.jianshu.com/go?to=https%3A%2F%2Fgym.openai.com%2Fenvs)

Gym 比较好的一点是你可以上传你自己训练环境的算法上去，也可以看到别人上传的算法，并且可以下载别人的算法代码。例如 [https://gym.openai.com/envs/CartPole-v0](https://links.jianshu.com/go?to=https%3A%2F%2Fgym.openai.com%2Fenvs%2FCartPole-v0) 就是 CartPole 这个目的是把杆子立起来的环境，里面你可以找到别人上传的算法：

![img](https:////upload-images.jianshu.io/upload_images/1783214-3821196b9ba21408.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

别人上传的算法

------

Universe 基于 Gym，是一个在全世界的游戏、网页和其他应用中，评估、训练智能代理的软件平台。

代理（agent）使用和人类类似的感官输入和控制方式，不过它看到的是像素，控制的是鼠标和键盘。

![img](https:////upload-images.jianshu.io/upload_images/1783214-f5d9b2089acdb737.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Universe 的基本原理

这使得任何需要电脑来完成的任务，都可以训练 AI 去做，并且与人类玩家较量。

Universe 包含 1000 多种不同训练环境，包括 Flash 游戏、网页任务、侠盗猎车手 这样的游戏。

Universe 是英语「宇宙」的意思，可以看出这个项目的愿景很大，旨在开发出接近通用人工智能（General Artificial Intelligence）的算法。

Universe 的官网是 [https://github.com/openai/universe](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Funiverse)（本来 [https://universe.openai.com](https://links.jianshu.com/go?to=https%3A%2F%2Funiverse.openai.com) 才是官网，但不久前这个网址变成一直会导向 Github 上的页面了，看来 Universe 项目不像 Gym 项目那么活跃）。

不过 Universe 还有个博客：[https://blog.openai.com/universe](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.openai.com%2Funiverse)

里面的文章值得一看，介绍了 Universe 的基本原理。主要说的是 Universe 的每个环境基本上都是运行在一个 Docker 容器里面，然后会通过 VNC 等方式来远程连接，等等。

待补充...

## 3. 什么是 Anaconda

------

对于 Universe 的安装和配置，官方推荐用 Anaconda。对于 Gym 的安装，我们也可以使用 Anaconda。我们也来介绍一下。

Anaconda 是非常著名的开源的 Python 发行版本，其包含了conda、Python 等 180 多个科学包及其依赖项，可以大大方便配置开发环境。

Anaconda 可以用于创建独立的 Python 开发运行环境。每个环境中的 Python Runtime（运行时）都是独立的，互不影响。这样就不用担心安装 A 的时候把
B 的环境给破坏了。

Anaconda 是英语「森蚺」（蚺 ：ran 第二声）的意思。森蚺是一种体型巨大的无毒蛇，主要栖息于南美洲，为蚺科体型最大的成员，同时也是世上最大的蛇之一。因为 Python 是英语「蟒蛇」的意思嘛，因此 Anaconda 这个 Python 的发行版本取这个名字也很好理解。一家人嘛，都是「肥硕」的蛇蛇。

Anaconda 的官网是 [https://www.anaconda.com](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.anaconda.com)

![img](https:////upload-images.jianshu.io/upload_images/1783214-0930d1ce8360dc57.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Anaconda 官网

Anaconda 附带默认安装的软件有著名的 Jupyter Notebook （官网 [http://jupyter.org](https://links.jianshu.com/go?to=http%3A%2F%2Fjupyter.org) ）这个 Python 的交互式笔记本，支持运行40 多种编程语言。Jupyter Notebook 的本质是一个Web 应用程序，便于创建和共享文学化程序文档，支持实时代码，数学方程，可视化和 Markdown，还可以插入图片，视频，音频，等等。

![img](https:////upload-images.jianshu.io/upload_images/1783214-24adddf9c4ec7687.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

大家如果学习 Python 的话，一定要用一下 Jupyter Notebook，太强大。Github 上不少人也是直接上传他们的 Jupyter Notebook 的文件上去，在 Github 可以直接解析被大家看到内容。例如：

![img](https:////upload-images.jianshu.io/upload_images/1783214-719d22b7a229925d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Jupyter Notebook 的文件在 Github 上的示例

Anaconda 非常强大，与 Python 的另一个软件 VirtualEnv（官网 [https://virtualenv.pypa.io](https://links.jianshu.com/go?to=https%3A%2F%2Fvirtualenv.pypa.io)）比较类似，都可以创建 Python 的虚拟环境。但是 Anaconda 更加高大上，看网站的专业程度差异即可知悉。

## 4. 什么是 Docker

------

对于 Universe 的安装和配置，也会用到 Docker。对于 Gym 的安装，不需要用到 Docker。因为 Universe 的环境基本都是运行在一个 Docker 的容器里的。

Docker 的官网是 [https://www.docker.com](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.docker.com)

![img](https:////upload-images.jianshu.io/upload_images/1783214-19f55370e9401ca7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 官网

Docker 是非常著名的轻量级虚拟化技术，我们这篇文章就不过多介绍 Docker 了，毕竟网上 Docker 的教程比比皆是。Docker 是近年来非常流行的技术，建议大家有空学习一下。Docker 官网的英文教程当然是最好的：[https://docs.docker.com/get-started](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.docker.com%2Fget-started)

Docker 原生支持 Linux，Docker 的实现高度依赖 Linux kernel 的 cgroup，namespace 等特性和接口，这些 Windows 和 macOS 没有。简单的解决方法之一就是开一个虚拟机跑 Linux，然后把 Docker 跑在虚拟机的 Linux 之上。

这也是为什么你会在安装 Windows 版的 Docker 时会看到也要安装 VirtualBox 这个虚拟机软件的原因（macOS 版本则用的是另一个虚拟机软件，不是 VirtualBox。好像是 [Hyperkit](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fmoby%2Fhyperkit) ）。下面我们演示 Windows 安装 Gym 和 Universe 时会讲 。

Docker 在线的容器平台 Docker Hub （看到 Hub 是不是联想到了 Github ？ hub 是英语「中心」的意思）：[https://hub.docker.com](https://links.jianshu.com/go?to=https%3A%2F%2Fhub.docker.com)

你可以创建一个 Docker 账户来登录，登录之后看到类似这样：

![img](https:////upload-images.jianshu.io/upload_images/1783214-68cc91049fc2aaef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker Hub

Docker Hub 有点像一个 Docker 版的 Github，但是和 Github 在上面托管代码不同，Docker Hub 托管的是 Docker 的容器镜像。你可以上传自己制作的容器镜像，别人可以用 docker pull 命令来取得，然后直接使用，非常方便。

你可以管理你自己创建的 Docker 私人仓库（有点类似 Github 的那种仓库）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-75fc2f314b650f38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker Repository

你可以在安装了 Docker 之后，在 Docker 的终端里用 `docker pull` 命令来下载别人公开在 Docker Hub 上的容器镜像，比如 Explore 这个菜单进去可以看到一些著名的公开容器镜像：

![img](https:////upload-images.jianshu.io/upload_images/1783214-84196684e9307145.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 公开容器镜像1

![img](https:////upload-images.jianshu.io/upload_images/1783214-363ac8ea281d9bc0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 公开容器镜像2

![img](https:////upload-images.jianshu.io/upload_images/1783214-20735c2930016676.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 公开容器镜像3

可以看到非常多著名的项目都有 Docker 公开的容器镜像，比如 Ubuntu，Go 语言，为我们部署开发环境提供了诸多便利。

比如你只要用 `docker pull ubuntu` 命令即可获得 Ubuntu 开发环境：

![img](https:////upload-images.jianshu.io/upload_images/1783214-2d825904cc3f88bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Ubuntu 的官方容器镜像

你也可以用左上角的搜索栏去搜索你想要的容器镜像，比如我搜索 gym，会搜出 OpenAI Gym 的镜像：

![img](https:////upload-images.jianshu.io/upload_images/1783214-d216666896604622.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Gym 的容器镜像的搜索结果

点击第一个写了 openai-gym 的镜像进去：

![img](https:////upload-images.jianshu.io/upload_images/1783214-2f427808abd86a72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

OpenAI Gym 的容器镜像

一般 STARS（类似 Github 上的 Stars 数目，表示「收藏」）和 PULLS（被拉取的次数，就是别人用 `docker pull`来下载此镜像的次数） 数目最多的是比较对的镜像：

![img](https:////upload-images.jianshu.io/upload_images/1783214-38e07ffdd7a50788.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/210)

STARS 和 PULLS

Docker 真的很强大且有趣。作为程序员一定要学习一下。

## 5. Linux 安装 Gym 和 Universe

------

我们以 Ubuntu 这个 Linux 发行版作为演示环境。毕竟这个操作系统是比较常用的，也是 TensorFlow 的官方默认 Linux 环境。

首先，我们要安装一些软件：

首先，我们用 cd 命令来进入我们的家目录：

```
cd
```

对于 Ubuntu 16.04，请先运行以下程序，以确保 apt 软件包列表是最新的：

```
sudo apt-get update
```

接着我们来安装一些软件：

```
sudo apt-get install golang python3-dev python-dev libcupti-dev libjpeg-turbo8-dev make tmux htop chromium-browser git cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
```

------

如果是 Ubuntu 14.04，则略有不同，请依次运行以下命令：

```
sudo add-apt-repository ppa:ubuntu-lxc/lxd-stable
```

上面的命令式为了添加 Go 语言的最新版到 apt 的软件列表中。

```
sudo apt-get update
```

上面的命令是更新 apt 软件包列表。

然后，与 Ubuntu 16.04 类似，也运行下面的命令来安装软件：

```
sudo apt-get install golang python3-dev python-dev libcupti-dev libjpeg-turbo8-dev make tmux htop chromium-browser git cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
```

安装时，询问是否安装，请输入「y」（yes 的首字母），然后按下 回车键（Enter）来开始安装。

#### 安装 Anaconda 和基本使用

------

接下来，我们安装 Anaconda，以便用 Anaconda 来创建与系统环境独立开来的 Anaconda 虚拟环境。我们之后的开发环境都会在这个虚拟环境里安装配置。

目前，Anaconda 的 Python 3.5 版本与 Universe 项目配合最好。如果用 Anaconda 的最新版本，也许不能很好地安装 Universe。

我们可以用 wget 命令（如果没有安装 wget，请使用 `sudo apt install wget` 来安装。不过 Ubuntu 里一般自带了）来获取 Anaconda 的 Python 3.5 版本：

```
wget https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh
```

这个 Anaconda 安装程序有 456 MB，因此下载时间视你的网速而定，需要等一会。你可以去泡杯咖啡，或者热一只烤鸡。

下载完之后，我们来安装 Anaconda，可以用 Bash 这个 Shell 软件来安装，当然如果你是 zsh 或其他 Shell 软件也可以用其他命令来安装 ：

```
bash Anaconda3-4.2.0-Linux-x86_64.sh
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-e4393ebe431db03c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

安装 Anaconda 的提示信息

提示信息说「Please press ENTER to continue」，也就是「请按下 回车键 以继续」，所以我们按下回车键。

接着安装程序会显示 Anaconda 的 License 就是一些证书和条款之类的信息：

![img](https:////upload-images.jianshu.io/upload_images/1783214-e90e7b28eeb25323.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

证书和使用条款，可翻页不看

不用看，直接用 空格键 翻页，然后翻到最后，看到显示这样一句话：

![img](https:////upload-images.jianshu.io/upload_images/1783214-7a083715420274be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

询问是否同意使用条款什么的

「Do you approve the license terms」，也就是「是否同意证书条款」 ，输入「yes」，

![img](https:////upload-images.jianshu.io/upload_images/1783214-dcb4ffc980815007.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

输入 yes 表示同意，然后按 回车

然后 回车。回车之后，又出现了下面的提示：

![img](https:////upload-images.jianshu.io/upload_images/1783214-35137752aa089105.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

确认 Anaconda 的安装路径

就是告诉你：Anaconda 的程序将会默认安装在你的家目录下的 anaconda3 目录中（我的情况是在 /home/mooc/anaconda3，因为我的用户名是 mooc ）。输入 回车 表示确认安装在默认目录中，如果你在提示符 >>> 后面输入其他路径，则会安装在你指定的其他路径下。

我们按 回车（ENTER）选择默认的路径来安装即可。

按下 回车 之后，就开始安装 Anaconda 了（包含一些基础软件环境），会花一些时间：

![img](https:////upload-images.jianshu.io/upload_images/1783214-163747e321fdb8b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Anaconda 安装中

稍等片时，安装完成，显示如下信息：

![img](https:////upload-images.jianshu.io/upload_images/1783214-bdca97b1109d92e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

确认是否将 Anaconda 的子目录 bin 加入系统 PATH 环境变量

输入「yes」的话，安装程序就会做以下操作：

在你的 Shell 的配置文件中，比如如果你的 Shell 是 Bash 的话，就会在 ~/.bashrc 文件中加入下面这句命令：

```
export PATH="/home/$USER/anaconda3/bin:$PATH"
```

就是把 Anaconda 的安装目录下的 bin 目录的路径（ /home/$USER/anaconda3/bin ）添加到 PATH 环境变量的最前面。

然后会做

```
source ~/.bashrc
```

使改动立即生效。

如果输入「no」的话，表示不需要安装程序帮你自动添加，之后可以自己添加：

![img](https:////upload-images.jianshu.io/upload_images/1783214-7c4ce511ff744d46.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

输入「no」，回车

我比较喜欢自己添加，这样我可以把 Anaconda 的 bin 目录的路径加入到 PATH 环境变量的最后，而不是最前。这样可以避免在命令行中输入 python 时调用的是 Anaconda 中的 python 程序。

如果你的默认 Shell 是 Bash 的话，就用文本编辑器在 ~/.bashrc 中添加下面这句命令：

```
export PATH="$PATH:/home/$USER/anaconda3/bin"
```

就是把 Anaconda 的安装目录下的 bin 目录的路径（ /home/$USER/anaconda3/bin ）添加到 PATH 环境变量的最后面。

保存，退出编辑器，然后在命令行输入：

```
source ~/.bashrc
```

使改动立即生效。

然后用

```
echo $PATH
```

来显示 PATH 环境变量的值，可以看到 /home/![USER/anaconda3/bin（](math-20210325152812171)USER 就是你的当前用户，比如我是 mooc ）这个路径已经添加在 PATH 变量的最后了：

![img](https:////upload-images.jianshu.io/upload_images/1783214-6da792011f9b34cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

/home/$USER/anaconda3/bin 已经添加在 PATH 变量的最后

如果你的 Shell 是 zsh，那么请改动你的 ~/.zshrc 文件。其他的 Shell 程序也类似。

这样，我们的 Anaconda 就安装配置好了。接下来，我们可以用 Anaconda 来创建一个虚拟环境，可以起名叫 universe（当然，你也可以取其他名字）：

```
conda create --name universe python=3.5 anaconda
```

回车后，会让我们确认是否要安装列出的软件到这个虚拟环境中：

![img](https:////upload-images.jianshu.io/upload_images/1783214-95c8a6be1a8a7360.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

询问是否安装列出的软件到虚拟环境中

默认是「y」，表示 yes，就是同意。我们按下 回车 即可。

它就开始下载安装那些软件到虚拟环境中了：

![img](https:////upload-images.jianshu.io/upload_images/1783214-714558ae9381da90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

安装软件到虚拟环境中

下载安装会花一段时间，依网速而定。这时候你可以喝一喝咖啡，或者吃一下之前热的烤鸡。

经过一定时间的等待，虚拟环境创建完毕：

![img](https:////upload-images.jianshu.io/upload_images/1783214-d471cfbeaa0c660d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

虚拟环境创建完毕

然后，我们可以随时用以下命令来激活并进入环境中：

```
source activate universe
```

activate 是英语「激活」的意思。

用以下命令可以退出虚拟环境：

```
source deactivate universe
```

deactivate 是英语「灭活」的意思。

这里的 universe 是我们创建的虚拟环境的名字，你的情况可能不是叫这个名字，那么请根据你的虚拟环境的名字来更改命令。

你可以运行下面的命令来看看你有哪些虚拟环境：

```
conda env list
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-a794d8b10a4ab352.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

conda env list 命令显示所有虚拟环境

可以看到默认 Anaconda 有个环境，名字叫 root，就是 Anaconda 安装的所在。这个环境默认是不激活的。

看到我们创建的 universe 那个环境了吗？目前它没有被激活（相当于「选中并进入」），因此星号（*）表示的当前的虚拟环境还是在 root 上。

如果我们用

```
source activate universe
```

命令来进入 universe 这个虚拟环境，那么命令行的提示符会变样：

![img](https:////upload-images.jianshu.io/upload_images/1783214-d6565ea6a5fdef92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

命令行提示符前面多了 (universe) 字样，表示目前在此虚拟环境中

此时，我们再用

```
conda env list
```

来列出所有的虚拟环境：

![img](https:////upload-images.jianshu.io/upload_images/1783214-2b98436ca5652503.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

星号指在 universe 的上面，表示 universe 是被激活的虚拟环境

可以看到目前星号（*）由原先的 root 变到了 universe 上，说明 universe 是目前被激活的虚拟环境。

如果你用

```
source deactivate universe
```

来退出 universe 这个虚拟环境，则命令行提示符又变回原来的样子：

![img](https:////upload-images.jianshu.io/upload_images/1783214-ddb036b3f3dc3ca6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

退出 universe 虚拟环境

可以看到命令行提示符的 (universe) 前缀消失，说明我们已经不在 universe 这个虚拟环境中了。

当然了，说是虚拟环境中，其实所在的真实目录还是本系统的目录，你可以用 cd 命令去切换到各个目录，只不过你的 Python 的开发环境的所有软件和参数什么的都是用的此虚拟环境的了，而不是系统的了。

比如你如果再进入 universe 虚拟环境，并且输入 python 命令，可以看到它显示的 Python 的解释器是 Anaconda 版本的：

![img](https:////upload-images.jianshu.io/upload_images/1783214-0497579a00ebd850.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

虚拟环境中的 Python 解释器和操作系统的不一样

如果用

```
conda list
```

可以列出当前虚拟环境信息：

![img](https:////upload-images.jianshu.io/upload_images/1783214-50d61a7e2f8ab2ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

conda list 命令会列出当前虚拟环境的信息 1

![img](https:////upload-images.jianshu.io/upload_images/1783214-e166ded19626853b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

conda list 命令会列出当前虚拟环境的信息 2

如果要删除虚拟环境，使用下面的命令：

```
conda remove --name <env name> --all
```

其中 <env name> 表示要删除的虚拟环境的名字，比如我们创建的 universe。

要在虚拟环境中安装软件，用下面的命令：

```
conda install xxx
```

xxx 表示要安装的软件名称。

好的，那么，既然我们已经用 Anaconda 创建了我们的 虚拟环境，起名叫 universe，那么现在我们继续配置我们的开发环境，在 universe 这个虚拟环境中安装我们所要用的软件。

首先，我们要确保自己位于创建的虚拟环境中：

```
source activate universe
```

然后，安装一些额外的软件：

```
conda install pip six libgcc swig
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-5bf5ee9ce62d22ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

询问是否安装或升级

按 回车，表示同意安装或升级软件。

然后我们再安装 OpenCV ：

```
conda install opencv
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-d5b95bc6783926aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

询问是否安装

按 回车，表示同意安装。

#### 安装 Docker

------

接着我们来安装 Docker 这个软件：

```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

如果是 Ubuntu 14.04，则还需要运行下面的命令：

```
sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
```

接着，我们运行如下命令：

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

再运行下面的命令：

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

再做一次 apt 列表的升级：

```
sudo apt-get update
```

接着，就可以安装 Docker 了：

```
sudo apt-get install docker-ce
```

被询问是否安装时，输入「y」，再按 回车。

安装完 Docker，我们来测试一下安装是否成功。

首先，我们启动 Docker 服务：

```
sudo service docker start
```

运行以下命令来让 Docker 给我们输出一些信息：

```
sudo docker run hello-world
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-dd7ff7f61cb0b7c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 输出 "Hello from Docker !"，表示安装成功

可以看到上面我们都是以 root 的身份运行 Docker 的命令。为了让我们之后每次运行 Docker 不需要用 root 身份而只需要用我们的普通用户身份，我们可以这样做：

```
sudo groupadd docker
```

上面的命令是为了创建一个用户组，叫做 docker。

然后，我们再把我们当前所在的用户添加到 docker 这个用户组里：

```
sudo usermod -aG docker $USER
```

接着，重启一下电脑：

```
sudo reboot
```

重启以后，加入你遇到 Docker 的连接问题，可以尝试依次运行下面的几句命令来解决：

```
sudo groupadd docker

sudo gpasswd -a ${USER} docker

sudo service docker restart   

sudo reboot
```

至此，Docker 安装完毕。

#### 安装 Gym

接着，我们安装 OpenAI Gym。

首先，先确认你还在 universe 这个虚拟环境里：

![img](https:////upload-images.jianshu.io/upload_images/1783214-d6565ea6a5fdef92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

命令行提示符前面有 (universe) 字样，表示目前在此虚拟环境中

然后我们用 git 来获取 Gym 的代码，依次运行下面两句命令：

```
cd ~

git clone https://github.com/openai/gym.git
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-8337397dff71e031.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

获取 Gym 代码库

进入 gym 目录，然后安装 Gym。依次运行下面两句命令：

```
cd ~/gym

pip install -e '.[all]'
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-bcf0141658bec22f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

安装 Gym

Gym 的安装大家也可以参考下官方的 Github 页面：[https://github.com/openai/gym](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Fgym)

目前的最新版的 Gym 的那个 MuJoCo 的模块有些问题，似乎安装不上，MuJoCo 本身也比较特殊，需要一些额外配置。

> MuJoCo 是 Multi-Joint dynamics with Contact 的缩写。表示「有接触的多关节动力」是用于机器人、生物力学、动画等需要快速精确仿真领域的物理引擎。
> 官网：[http://mujoco.org](https://links.jianshu.com/go?to=http%3A%2F%2Fmujoco.org)

所以不出意外地话，上面的命令

```
pip install -e '.[all]'
```

会出错：

![img](https:////upload-images.jianshu.io/upload_images/1783214-713f8c2763e72759.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

安装错误：问题出在 MuJoCo 上

比较简单的规避错误的方法就是在 gym 目录下的
setup.py 这个文件里去掉 MuJoCo 的安装选项：

比如说用 vim 或 atom 文本编辑器（随便你用什么文本编辑器）来打开 `~/gym/setup.py` 这个文件：

```
vim  ~/gym/setup.py
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-b78cc6fce4562947.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

注释掉 setup.py 文件中和 MuJoCo 有关的安装选项

如上图所示，我们可以暂时把和 MuJoCo 相关的安装选项都注释掉。把

```
'mujoco': ['mujoco_py>=1.50', 'imageio'],
'robotics': ['mujoco_py>=1.50', 'imageio'],
```

这两句注释掉，不让它被安装，将其改为：

```
#'mujoco': ['mujoco_py>=1.50', 'imageio'],
#'robotics': ['mujoco_py>=1.50', 'imageio'],
```

保存，退出 setup.py 文件的编辑。

然后，重新运行以下命令：

```
pip install -e '.[all]'
```

这次就可以安装成功了，安装的是 Gym 的最新版本。

Gym 官方的 Github 上说如果你之后还是需要安装 MuJoCo 的话，可以尝试运行：

```
pip install -e '.[mujoco]'
```

来单独安装。这里我们不理会 MuJoCo，因为暂时用不到。

#### 安装 Universe

------

安装完了 Gym，我们终于可以进入 Linux 中安装 Gym 和 Universe 之旅的最后一站了：安装 Universe。

和安装 Gym 类似，我们首先用 git 来获取 Universe 的代码（请确认你始终位于你用 Anaconda 创建的虚拟环境中），依次运行下面两句命令：

```
cd ~

git clone https://github.com/openai/universe.git
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-8363e1fc1ef7de2b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

获取 Universe 代码库

然后进入 universe 目录，安装 Universe。依次运行下面两句命令：

```
cd ~/universe

pip install -e .
```

安装 Universe 成功。

## 6. 写程序测试 Gym 和 Universe

------

我们可以写几个 Python 的程序来测试一下 Gym 和 Universe。

比如我们可以创建一个文件，叫 test_universe1.py。

然后在里面写入以下代码：

```
import gym
import universe  # register the universe environments
from universe import wrappers
 
env = gym.make('gym-core.PongDeterministic-v0')
env = wrappers.experimental.SafeActionSpace(env)
env.configure(remotes=1)
 
observation_n = env.reset()
 
while True:
  action_n =  [env.action_space.sample() for ob in observation_n]
  observation_n, reward_n, done_n, info = env.step(action_n)
  env.render()
```

上面的程序会启动 Pong（乒乓球）这个游戏。

保存这个文件。然后在命令行里运行以下命令：

```
python test_universe1.py
```

但是不出意外的话，会有一个错误（略坑...）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-0c4170f2619ceed7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

模块 'gym.benchmarks' 找不到

我看了 Universe 的 Github 上的 Issue 里的问题汇报，发现是 Gym 的 0.9.6 版本里把 benchmarks 这个包给去了：[https://github.com/openai/universe/issues/228](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fopenai%2Funiverse%2Fissues%2F228) 。我晕...

所以我们可以卸载 Gym，重新安装，但是是指定安装 0.9.5 版本。

```
cd ~/gym

pip uninstall gym

pip install gym==0.9.5
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-84da8ffd66ae65d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

卸载 Gym 的最新版本，安装 0.9.5 版本

> 希望 OpenAI 之后能解决这个问题...

大家也可以在环境里安装 [TensorFlow](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.tensorflow.org) 这样的机器学习库，来进行强化学习的学习和测试：

安装 CPU 版本的 TensorFlow：

```
pip install tensorflow
```

或 安装 GPU 版本的 TensorFlow：

```
pip install tensorflow-gpu
```

现在我们再运行：

```
python test_universe1.py
```

就可以启动环境了（第一次启动环境时 Docker 需要下载一些文件，需要等一会）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-7d53c7f13572c168.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/346)

运行 Universe 里面的游戏 Pong

刚才运行了 Pong 这个简单的游戏，我们也可以来演示一个复杂一些的游戏，比如 Universe 的官方 Github 上的例子 DuskDrive 这个赛车游戏 。

我们创建一个新的文件，可以起名叫 test_universe2.py。在里面写入如下代码：

```
import gym
import universe  # register the universe environments

env = gym.make('flashgames.DuskDrive-v0')
env.configure(remotes=1)  # automatically creates a local docker container
observation_n = env.reset()

while True:
  action_n = [[('KeyEvent', 'ArrowUp', True)] for ob in observation_n]  # your agent here
  observation_n, reward_n, done_n, info = env.step(action_n)
  env.render()
```

运行它：

```
python test_universe2.py
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-b60998c8191ef968.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

运行 Universe 里面的游戏 DuskDrive

当然，我们还可以写代码来测试其他各种各样的环境，比如再测试一个 Neon Race（霓虹赛车）的环境，加入一些小小的代码修改，让它略微聪明些：

我们创建一个新的文件，可以起名叫 test_universe3.py。在里面写入如下代码：

```
# -*- coding: UTF-8 -*-

"""
测试 Gym 和 Universe 环境是否正确安装
"""

import random
import gym
import universe

env = gym.make('flashgames.NeonRace-v0')  # 创建 NeonRace 的环境
env.configure(remotes=1)  # 自动创建一个本地的 Docker 容器
observation_n = env.reset()  # 重置环境，并且返回初始的 Observation

# 左转和右转
goleft = [('KeyEvent', 'ArrowUp', True), ('KeyEvent', 'ArrowLeft', True),
        ('KeyEvent', 'ArrowRight', False)]
goright = [('KeyEvent', 'ArrowUp', True), ('KeyEvent', 'ArrowLeft', False),
         ('KeyEvent', 'ArrowRight', True)]

# 向前加速
boostforward = [('KeyEvent', 'ArrowUp', True), ('KeyEvent', 'ArrowRight', False),
       ('KeyEvent', 'ArrowLeft', False), ('KeyEvent', 'n', True)]

sum_reward = 0
turn = 0
rewards = []
buffer_size = 100
action = boostforward

while True:
    turn -= 1
    if turn <= 0:
        action = boostforward
        turn = 0
    # 根据速度来选择 action
    action_n = [action for ob in observation_n]

    # 实行 action，返回细分的多个参数
    observation_n, reward_n, done_n, info = env.step(action_n)

    sum_reward += reward_n[0]

    rewards += [reward_n[0]]
    # 如果卡住了，尝试向某一个方向开一会
    if len(rewards) >= buffer_size:
        mean = sum(rewards) / len(rewards)

        if mean == 0:
            turn = 25
            if random.random() < 0.5:
                action = goleft
            else:
                action = goright

        rewards = []

    env.render()
```

运行它：

```
python test_universe3.py
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-bd8883d565b215b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

运行 Universe 里面的游戏 NeonRace

当然了，你也可以写一个小程序单独测试一下 Gym。我们创建一个新的文件，可以起名叫 test_gym.py。在里面写入如下代码：

```
# -*- coding: UTF-8 -*-

import gym

env = gym.make('CartPole-v0')

for i_episode in range(100):
    observation = env.reset() 
    for t in range(100):
        env.render() # 更新动画
        action = env.action_space.sample()
        observation, reward, done, info = env.step(action) # 推进一步
        if done:
            env.reset() 
            continue
```

运行它：

```
python test_gym.py
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-76c5059b4a7d8e35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

运行 Gym 里面的游戏 CartPole

很有趣吧，更多环境等待你去发现、去实验。你也可以配合一些强化学习的算法来训练你的环境，然后让代理（agent）有智能，可以玩这些游戏比人更厉害。

## 7. Windows 安装 Gym 和 Universe

------

Gym 和 Universe 官方没有原生的 Windows 的支持。

当然了，也不是说 Windows 就不能安装 Gym 和 Universe。

不过得通过 Docker 来安装。首先，我们下载安装 Docker。

#### 安装 Windows 版 Docker

进入 Docker 的官网：[https://www.docker.com](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.docker.com)

![img](https:////upload-images.jianshu.io/upload_images/1783214-fac2debc28ca538e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 官网

点击上面菜单中的 Product（产品），进入 Product 页面：

![img](https:////upload-images.jianshu.io/upload_images/1783214-86eaeeea75b5dfc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

进入 Product（产品）页面

可以看到「Get Docker Community Edition」，也就是「获取 Docker 的社区版」，免费的。当然了，如果你是土豪，也可以点击「Get Docker Enterprise Edition」，获取 Docker 的企业版，是付费的。

我们进入 Docker 社区版页面：[https://www.docker.com/community-edition](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.docker.com%2Fcommunity-edition)

点击 Download（下载）菜单，可以看到：

![img](https:////upload-images.jianshu.io/upload_images/1783214-b2fa22b7089c1f77.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 社区版 Download 页面

我们要下载 Windows 版，因此点击 DOCKER CE FOR WINDOWS的「Download from Docker Store」，会进入：[https://store.docker.com/editions/community/docker-ce-desktop-windows](https://links.jianshu.com/go?to=https%3A%2F%2Fstore.docker.com%2Feditions%2Fcommunity%2Fdocker-ce-desktop-windows)

![img](https:////upload-images.jianshu.io/upload_images/1783214-81d69c07f04360d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker Community Edition for Windows

不过，我们看到有提示信息：「Requires Microsoft Windows 10 Professional or Enterprise 64-bit. For previous versions get [Docker Toolbox](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.docker.com%2Ftoolbox%2Foverview%2F).
」，意思是「Windows 的 Docker 社区版需要 Windows 10 的64 位专家版或者企业版操作系统。如果你是其他版本，请下载 [Docker Toolbox] 来安装 Docker」。

要求还挺高啊。满足条件的朋友们可以下载 Docker Community Edition for Windows，点击「Get Docker」按钮即可。

我演示用的 Windows 环境是 Win7，因此我只能下载 Docker Toolbox。当然了，如果你是 Win 10 的系统，也可以安装 Docker Toolbox 的。

点击「Docker Toolbox」那个地方，

![img](https:////upload-images.jianshu.io/upload_images/1783214-3c78d9b91a5f8bd3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/114)

Docker Toolbox

进入以下页面：[https://docs.docker.com/toolbox/overview/](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.docker.com%2Ftoolbox%2Foverview%2F)

![img](https:////upload-images.jianshu.io/upload_images/1783214-5fde9ef1326e6d65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker Toolbox 下载页面

拉到下面，看到「Toolbox for Windows」：

![img](https:////upload-images.jianshu.io/upload_images/1783214-cdbc3d655eb664bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/496)

Docker Toolbox for Windows

点击「Get Docker Toolbox for Windows」：

![img](https:////upload-images.jianshu.io/upload_images/1783214-62e0a44325e81ab1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

选择另存为

就会开始下载 DockerToolbox.exe 这个可执行程序，大小大概 200 多 MB，稍等一会，下载之后会像这样：

![img](https:////upload-images.jianshu.io/upload_images/1783214-759f3759ed30a71c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/163)

DockerToolbox.exe

双击 DockerToolbox.exe，进入安装：

![img](https:////upload-images.jianshu.io/upload_images/1783214-2d234a1688ed45fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/642)

开始安装 Docker Toolbox

点击 Next（下一步）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-ca0542bc0474ceea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/506)

选择 Full installation（完整安装），勾选全部

选择 Full installation（完整安装），勾选全部。再点击 Next（下一步）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-b742d99492f023e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/501)

全部选择

全部选择，记得要勾选「Install VirtualBox with NDIS5 driver」。点击 Next（下一步）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-cf2108861673f837.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/498)

确认安装信息

确认安装信息，点击 Install（安装）：

![img](https:////upload-images.jianshu.io/upload_images/1783214-653d41e7e6f22884.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/241)

安装完成，多出两个桌面快捷方式

等它安装完成。会多出两个桌面快捷方式，如上图所示：

- Kitematic ：Docker 容器的管理器，是可以让我们连接到 Docker 容器网站（Docker Hub）的一个图形界面程序。如果你有 Docker 帐号，可以登录。Kitematic 的官网是 [https://kitematic.com](https://links.jianshu.com/go?to=https%3A%2F%2Fkitematic.com)
- Docker Quickstart Terminal ：我们需要的 Docker 的终端程序。

你可以双击 Docker Quickstart Terminal，会打开一个终端：

![img](https:////upload-images.jianshu.io/upload_images/1783214-da03e3313cc5ba3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/666)

Docker Quickstart Terminal

可以看到我们的可爱的 Docker 的吉祥物：鲸鱼。

这个终端就类似一个 Linux 的终端，你可以在里面运行 Linux 里的一些常用命令，比如 ls，mkdir，cd，cp，等等。

我们首先可以开启这个终端的「快速编辑模式」，这样就可以从外部复制文本进入了：

鼠标右键点击 Docker Quickstart Terminal 的窗口的左上角，点击「属性」，进入配置：

![img](https:////upload-images.jianshu.io/upload_images/1783214-5a895b2d833798bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/438)

设置 Docker Quickstart Terminal 的属性，勾选「快速编辑模式」

然后点击「确定」。就可以方便地复制黏贴文本到 Docker Quickstart Terminal 里了。

我们在终端里输入下面的命令来下载 Universe 的代码

```
git clone https://github.com/openai/universe.git
```

> Windows 下 Gym 和 Universe 的安装 待续... 貌似最新版的 Gym 和 Universe 在 Docker 里提供的镜像会有那个 MuJoCo 安装通不过的问题。

#### 安装 Anaconda

------

#### 安装 Gym

------

#### 安装 Universe

------

安装 Universe 完毕。

我们可以用之前在 Linux 里的测试文件（可以在 6. 写程序测试 Gym 和 Universe 那里找到测试的那些 Python 文件的代码，因为比较长，我就不再贴了）来测试一下 Gym 和 Universe 。确保你还是在 universe 这个虚拟环境里，然后运行 ：

```
python test_gym.py
```

和

```
python test_universe1.py
```

和

```
python test_universe2.py
```

和

```
python test_universe3.py
```

如果效果和之前在 Ubuntu 这个 Linux 发行版里运行的结果一样，那么我们的 Gym 和 Universe 就是 OK 了。

## 8. macOS 安装 Gym 和 Universe

------

苹果的 macOS 是肯定可以安装 Gym 和 Universe 的，因为 OpenAI 说他们就是在 macOS 上开发 Gym 和 Universe 的。

在 macOS 上安装 Gym 和 Universe 的过程和 Linux 下比较类似。

#### 安装 macOS 版 Docker

------

首先我们需要下载安装 Docker，进入 Docker 官网：[https://www.docker.com](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.docker.com)

进入 Community Edition（社区版） ，然后下载 macOS 版的 Docker 的 社区版：

![img](https:////upload-images.jianshu.io/upload_images/1783214-43aae124c5fa3185.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 社区版的 macOS 版本

再进入：

[https://store.docker.com/editions/community/docker-ce-desktop-mac](https://links.jianshu.com/go?to=https%3A%2F%2Fstore.docker.com%2Feditions%2Fcommunity%2Fdocker-ce-desktop-mac)

![img](https:////upload-images.jianshu.io/upload_images/1783214-0c26ac8107f69740.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

macOS 版的 Docker 社区版下载页面

点击 Get Docker 按钮，开始下载 Docker ：

![img](https:////upload-images.jianshu.io/upload_images/1783214-0780e9e5b6a6770b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/896)

下载 Docker 的 dmg 文件，用于在 macOS 安装

下载完后就和安装一般软件一样安装 Docker，然后启动 Docker，保证显示的是「Docker is running」（表示 Docker 正在运行）的绿色字样：

![img](https:////upload-images.jianshu.io/upload_images/1783214-5705b1cc3656fa0c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/780)

未登录 Docker 账户的样子

![img](https:////upload-images.jianshu.io/upload_images/1783214-16acd16428ebac76.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/440)

登录 Docker 账户后的样子

登录或不登录 Docker 账户都行。

然后在终端里运行：

```
docker ps
```

和

```
docker images
```

就会分别显示你目前的 Docker 的进程和镜像。

![img](https:////upload-images.jianshu.io/upload_images/1783214-2879666203aeb128.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Docker 的进程和镜像

由于目前我还没有创建任何 Docker 的进程和镜像，因此这两个命令显示都是空的列表。

安装完 Docker，我们接着安装 Anaconda。

#### 安装 macOS 版 Anaconda

------

我们进入 Anaconda 的官网：[https://anaconda.org](https://links.jianshu.com/go?to=https%3A%2F%2Fanaconda.org)

点击「Download Anaconda」，再进入 macOS 版的下载页面：[https://www.anaconda.com/download/#macos](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.anaconda.com%2Fdownload%2F%23macos)

![img](https:////upload-images.jianshu.io/upload_images/1783214-fbf35afeb0208e0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Mac 版 Anaconda

点击那个 Python 3.x 版本的 Download 下载。目前最新是 Python 3.6 版的 Anaconda。

所以你的 macOS 里还需要安装 Python 3.6 版本，可以去 Python 官网：[https://www.python.org](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.python.org) 下载安装 Python 3.6 的 macOS 版本：

![img](https:////upload-images.jianshu.io/upload_images/1783214-c8d41538d92be119.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

Python 3.6 版本的 macOS 版

[https://www.python.org/downloads/release/python-364](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.python.org%2Fdownloads%2Frelease%2Fpython-364)

安装完 Python 3.6 版本后，记得看一下你的 PATH 环境变量，确保 Python 3.6 的路径在其中，在你的 macOS 的终端 Terminal 里运行下面的命令查看 PATH 环境变量：

```
echo $PATH
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-2a0ee4d81e002d67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

PATH 环境变量中 Python 版本正确

可以看到我的 Python 3.6 是在 PATH 环境变量里的。如果不在，可以在你的 Shell 的配置文件（如果你的 Shell 是 Bash，则是 ~/.bashrc 。如果你的 Shell 是 zsh，则是 ~/.zshrc）里加入：

```
export PATH="$PATH:/Library/Frameworks/Python.framework/Versions/3.6/bin"
```

保存配置文件，然后再运行以下命令使改动立即生效：

```
source ~/.bashrc
```

如果你用的是 Bash 这个 Shell。或者：

```
source ~/.zshrc
```

如果你用的是 zsh 这个 Shell。

Python 3.6 安装配置好之后，我们下载Python 3.x 版的那个 Anaconda，之后就和在 Mac 安装普通软件一样，安装 Anaconda。

安装 Anaconda 之后，你的 PATH 文件里又会多出一个路径。如果不在，那就和上面添加 Python 3.6 的路径一样，在你的 Shell 的配置文件里加入你的 Anaconda 所在的路径的 bin 目录的路径，比如我的情况是这样的（因为我的用户名是 enming ）：

```
export PATH="$PATH:/Users/enming/anaconda3/bin"
```

你得把上面的 enming 替换成你自己的用户名。

保存配置文件，然后再运行以下命令使改动立即生效：

```
source ~/.bashrc
```

如果你用的是 Bash 这个 Shell。或者：

```
source ~/.zshrc
```

如果你用的是 zsh 这个 Shell。

你的 PATH 环境变量里就会有 Anaconda 的路径了：

![img](https:////upload-images.jianshu.io/upload_images/1783214-aaea05a6f19e7a8d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

PATH 环境变量里已经有 Anaconda 的路径

此时，你在终端中输入

```
conda --version
```

就会输出 Anaconda 的版本，例如：

![img](https:////upload-images.jianshu.io/upload_images/1783214-fe9437619e954206.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/738)

输出 Anaconda 版本

因为我们的 Universe 和 Python 3.5 版本的 Anaconda 才配合良好，因此我们要用 Python 3.5 版本的 Anaconda 来创建虚拟环境：

[https://docs.anaconda.com/anaconda/faq#how-do-i-get-anaconda-with-python-3-5](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.anaconda.com%2Fanaconda%2Ffaq%23how-do-i-get-anaconda-with-python-3-5)

![img](https:////upload-images.jianshu.io/upload_images/1783214-b475ee5037c856ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

如何安装基于 Python 3.5 的 Anaconda

运行下面的命令，在Anaconda 里安装 Python 3.5 ：

```
conda install python=3.5
```

如果问你是不是要安装列出的软件，按 回车 继续。

安装完之后，我们可以依次运行以下的两个命令来创建一个 Anaconda 的虚拟环境，取名叫 universe，用 Python 3.5 版本：

```
cd

conda create --name universe python=3.5 anaconda
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-04aaec033ead3286.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

创建一个Anaconda 的虚拟环境，取名 universe，用 Python 3.5

询问是否安装所列出的软件时，按 回车。虚拟环境就会被创建好了。接下来我们可以来进入虚拟环境，来安装我们的 Gym 和 Universe。

#### 安装 Gym

------

在终端输入 `source activate universe` 命令来进入刚才创建的名为 universe 的 Anaconda 的虚拟环境。

运行下面的命令：

```
brew install cmake boost boost-python sdl2 swig wget
```

来安装一些需要的软件。

进入家目录中，用 git 来获取 Gym 的代码。依次运行下面的命令：

```
cd

git clone https://github.com/openai/gym.git
```

之前在 Linux 里面安装 Gym 和 Universe 时说的 Gym 的 MuJoCo 组件安装不上的问题，比较简单的规避错误的方法就是在 gym 目录下的 setup.py 这个文件里去掉 MuJoCo 的安装选项：

比如说用 vim 或 atom 文本编辑器（随便你用什么文本编辑器）来打开 `~/gym/setup.py` 这个文件：

```
vim  ~/gym/setup.py
```

![img](https:////upload-images.jianshu.io/upload_images/1783214-b78cc6fce4562947.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

注释掉 setup.py 文件中和 MuJoCo 有关的安装选项

如上图所示，我们可以暂时把和 MuJoCo 相关的安装选项都注释掉。把

```
'mujoco': ['mujoco_py>=1.50', 'imageio'],
'robotics': ['mujoco_py>=1.50', 'imageio'],
```

这两句注释掉，不让它被安装，将其改为：

```
#'mujoco': ['mujoco_py>=1.50', 'imageio'],
#'robotics': ['mujoco_py>=1.50', 'imageio'],
```

保存，退出 setup.py 文件的编辑。

然后，依次运行下面的命令：

```
cd ~/gym

pip install -e '.[all]'
```

但是还是之前在 Linux 里面安装 Gym 和 Universe 时说的那个新版 Gym 移除了模块 'gym.benchmarks' 的问题。

用上面的命令 `pip install -e '.[all]'` 安装完 Gym 最新版的所有组件（除了 MuJoCo）之后，需要先卸载 Gym，再安装 Gym 0.9.5 版本才能规避那个。

依次运行下面的命令：

```
cd ~/gym

pip uninstall gym

pip install gym==0.9.5
```

这样就可以了。

#### 安装 Universe

------

在终端输入 `source activate universe` 命令来确保位于刚才创建的名为 universe 的 Anaconda 的虚拟环境。

依次运行下面的命令：

```
xcode-select --install

pip install numpy incremental

brew install golang libjpeg-turbo
```

来安装一些需要的软件。

接着，进入家目录中，用 git 来获取 Universe 的代码。依次运行下面的命令：

```
cd

git clone https://github.com/openai/universe.git
```

然后安装 Universe，依次运行下面的命令：

```
cd ~/universe

pip install -e .
```

安装 Universe 完毕。

然后安装一些额外的软件：

```
conda install pip six libgcc swig
```

我们再安装 OpenCV ：

```
conda install opencv
```

系统会询问是否安装软件，按下回车即可进行安装。

大家也可以在环境里安装 [TensorFlow](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.tensorflow.org) 这样的机器学习库，来进行强化学习的学习和测试：

安装 CPU 版本的 TensorFlow：

```
pip install tensorflow
```

或 安装 GPU 版本的 TensorFlow：

```
pip install tensorflow-gpu
```

我们可以用之前在 Linux 里的测试文件（可以在文章上面的 **6. 写程序测试 Gym 和 Universe** 那里找到测试的那些 Python 文件的代码。因为代码比较多，我就不再贴了，请自己去这篇文章里找，就在 Linux 安装 Gym 和 Universe 的下面一些）来测试一下 Gym 和 Universe 。确保你还是在 universe 这个虚拟环境里，然后运行 ：

```
python test_gym.py
```

和

```
python test_universe1.py
```

和

```
python test_universe2.py
```

和

```
python test_universe3.py
```

如果效果和之前在 Ubuntu 里运行的结果一样，那么我们的 Gym 和 Universe 就是 OK 了。

## 9. 总结

------

1. 这篇文章花了我很久才写完，截了非常多的图，很不容易，请尊重原创劳动成果，转载请注明作者和出处，并放置原文链接。谢谢！
1. OpenAI 对科技界做出的贡献还是很大的，开源了很多用于人工智能的代码库。希望 OpenAI 这个非盈利机构继续为人类做贡献。
1. Gym 和 Universe 在 Linux 和 macOS 上安装的过程比较类似，毕竟一个是 Linux，一个是修改过的 Unix，比较相近。在 Windows 上的安装则比较折腾，而且在 Windows 上用命令行实在是比较难受。
1. 这篇文章我会一直更新的。希望大家提出建议，指出我的错谬，说说安装过程中遇到的问题，我会改进文章。谢谢！

------

> 我是 [谢恩铭](https://www.jianshu.com/u/44339a8a9afa)，公众号「程序员联盟」（微信号：coderhub）运营者，慕课网精英讲师 [Oscar 老师](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.imooc.com%2Fu%2F1289460)，终生学习者。
> 热爱生活，喜欢游泳，略懂烹饪。
> 人生格言：「向着标杆直跑」



作者：程序员联盟
链接：https://www.jianshu.com/p/536d300a397e/
来源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。