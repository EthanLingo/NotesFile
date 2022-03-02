文章目录

写在开头：
一、MuJoCo环境介绍：
二、系统平台介绍：
三、安装 MuJoCo：
3.1 获取许可证
3.2 下载源文件
四、安装 mujoco-py
五、最后解决方案：
写在开头：

本文写在笔者学习了强化学习算法 DQN，PG 和 DDPG 之后
之所以要安装 MuJoCo，是为了尝试 PPO 算法
之前尝试安装 RLBench 去验证学过的几个算法的时候，花费了整整 3 天没有成功，一把辛酸泪～
所以这次看到 MuJoCo 这个环境也是和机器人相关，想再次尝试一下
希望我踩过的坑可以帮助同道中人少一点痛苦
也希望成功安装 RLBench 的朋友可以指点迷津～
一、MuJoCo环境介绍：

MuJoCo 是目前机器人强化学习中最流行的仿真器之一
MuJoCo官网：http://mujoco.org/


二、系统平台介绍：

macOS Catalina
系统版本：10.15.6（2020年7月17日升级的系统）
虚拟环境用 Anaconda 搭建
Python 3.7.7（官方要求 3.6+）
写程序 IDLE 用的是 PyCharm
三、安装 MuJoCo：

3.1 获取许可证

登陆官网获取许可证：https://www.roboti.us/license.html

30 天试用版本：

我是 OS 系统，点击 OSX 下载文件 getid_osx
直接点击运行，默认是用文本编辑器打开，但是打不开的～
尝试在终端里面用 ./getid_osx 打开
显示Permission denied
解决方案一：
chmod -x getid_osx
大家可以尝试一下
不过我的结果还是打不开，依然是显示Permission denied
解决方案二：
chmod -f 711 getid_osx
成功打开，获取了电脑 id
在网站上输入，立刻就收到了邮件，里面有两个附件：
LICENSE.txt和mjkey.txt
另外还有个：个人版

官网上有一段提示：
NOTE: Activation is local and the software does not contact our server. Therefore activation keys cannot be deactivated. Please use the 30-day trial to test the software on the computer you intend to use long-term, before registering it here. This is particularly important for students because they can only register one computer.
意思就是慎重选择要安装的电脑，这东西是绑定电脑的。尤其是学生党要注意，虽然有 1 年的免费使用，但是千万别装错电脑！
3.2 下载源文件

Linux 请选择：
https://www.roboti.us/download/mujoco200_linux.zip

OS 系统请选择：
https://www.roboti.us/download/mujoco200_macos.zip

注意，这里的目录设置很重要！如果搞不清楚的话，请选择默认安装路径，以免出错！

在终端中mkdir ~/.mujoco 创建安装目录
然后把下载的程序文件解压，移动到该目录下mv mujoco200_macos ~/.mujoco/mujoco200
将邮件里面得到的 key 放到目录下mv mjkey.txt ~/.mujoco/mjkey.txt，多拷贝一份到~/.mujoco/mujoco200/bin，否则后面测试可能出问题
最终的目录如下：

四、安装 mujoco-py

这里开始出现大量的坑啊～～～
官方文档介绍直接使用 pip3 install -U 'mujoco-py<2.1,>=2.0' 即可，但是运行后：

一长串报错：
ERROR: Failed building wheel for mujoco-py 
Failed to build mujoco-py 
ERROR: Could not build wheels for mujoco-py which use PEP 517 and cannot be installed directly
1
2
3
网上解决方案一：
pip install --no-use-pep517 'mujoco-py<2.1,>=2.0'
1
试了下不行～～～

网上解决方案二：
pip install mujoco_py==2.0.2.8
1
安装成功，这个方案是安装了一个旧版本的 mujoco_py

在 PyCharm 运行测试代码：
import mujoco_py
import os
mj_path, _ = mujoco_py.utils.discover_mujoco()
xml_path = os.path.join(mj_path, 'model', 'humanoid.xml')
model = mujoco_py.load_model_from_path(xml_path)
sim = mujoco_py.MjSim(model)

print(sim.data.qpos)
# [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]

sim.step()
print(sim.data.qpos)
# [-2.09531783e-19  2.72130735e-05  6.14480786e-22 -3.45474715e-06
#   7.42993721e-06 -1.40711141e-04 -3.04253586e-04 -2.07559344e-04
#   8.50646247e-05 -3.45474715e-06  7.42993721e-06 -1.40711141e-04
#  -3.04253586e-04 -2.07559344e-04 -8.50646247e-05  1.11317030e-04
#  -7.03465386e-05 -2.22862221e-05 -1.11317030e-04  7.03465386e-05
#  -2.22862221e-05]
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
报错：
RuntimeError: Could not find GCC executable.  
HINT: On OS X, install GCC with `brew install gcc`. or `port install gcc`.
1
2
貌似是缺少了 gcc

brew install gcc
1
结果发现：

Warning: gcc 9.3.0_1 is already installed and up-to-date
1
看来我已经装了，但是程序没有找到

网上解决方案一：
有人认为这个是 OS 10.15 的 SDK 出了问题
所以要改用旧的 10.14 的 SDK，具体步骤参考以下链接：
https://github.com/openai/mujoco-py/issues/463
首先进入文件夹：
/Library/Developer/CommandLineTools/SDKs
1
发现以下 3 个文件夹

首先，把 MacOSX.sdk 改成 MacOSX_orig.sdk
然后，右键点击 MacOSX10.14.sdk，选择复制
然后，该目录下面出现个副本，把该副本改名为 MacOSX.sdk
形成以下目录：

很遗憾，报错依然存在～～～

网上解决方案二：
brew uninstall gcc@9
brew uninstall gcc
brew install gcc@8
1
2
3
就是用老版本的 gcc，原因嘛我估计是前面安装了旧版本的mujoco_py，所以不识别 gcc 9

再次运行测试代码，报新的错：
aise CompileError(msg) 
distutils.errors.CompileError: command '/usr/local/bin/gcc-8' failed with exit status 1
1
2
貌似是编译错误

网上解决方案三：
打开 mujoco_py 文件夹下面的 builder.py 文件，找到下面这段代码进行修改：
c_compilers = ['/usr/local/bin/gcc-6',  
              '/usr/local/bin/gcc-7',  
              '/usr/local/bin/gcc-8',   
              '/usr/local/bin/gcc-9', # 添加这一句
              '/opt/local/bin/gcc-mp-6',
1
2
3
4
5
于是重新安装 gcc
brew install gcc
这次可以找到 gcc 9 了，但是依然报错：

raise CompileError(msg) 
distutils.errors.CompileError: command '/usr/local/bin/gcc-9' failed with exit status 1
1
2
还是编译错误

网上解决方案四：
brew install llvm
然后
open -e .bash_profile
添加：
export PATH="/usr/local/opt/llvm/bin:$PATH"
export CC="/usr/local/opt/llvm/bin/clang"
export CXX="/usr/local/opt/llvm/bin/clang++"
export CXX11="/usr/local/opt/llvm/bin/clang++"
export CXX14="/usr/local/opt/llvm/bin/clang++"
export CXX17="/usr/local/opt/llvm/bin/clang++"
export CXX1X="/usr/local/opt/llvm/bin/clang++"
export LDFLAGS="-L/usr/local/opt/llvm/lib"
export CPPFLAGS="-I/usr/local/opt/llvm/include"
1
2
3
4
5
6
7
8
9
然后终端里面：
source .bash_profile
很遗憾～～～ 报错继续～～～

五、最后解决方案：

修改系统偏好里面的“安全性与隐私”：

在 “开发者工具” 里面把 “终端” 打勾
打开终端
pip install -U 'mujoco-py<2.1,>=2.0'
成功：
Successfully installed mujoco-py-2.0.2.11

在 PyCharm 中运行测试代码，依然报错，考虑了下应该还是权限问题，改用了终端里面的 python3 运行，成功！

在 PyCharm 里面运行的时候，会跳出无法验证开发者的提示，点击“问号”，会提示跳转到“安全性与隐私”中，点击允许。

重新运行，如果还有跳出，再点击允许。

多允许几次，直到没有跳出提示，运行成功！

PS： 每个人的系统环境都有所差别，所以如果不成功，可以挑选上面的各种解决方案进行尝试，如果还有问题，也欢迎留言探讨！
————————————————
版权声明：本文为CSDN博主「AItrust」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_42067550/article/details/107430221