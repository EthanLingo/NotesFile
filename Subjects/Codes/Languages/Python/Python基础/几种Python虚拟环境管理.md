[[Python虚拟环境]]
#资料 
#来源/转载


# 几种Python虚拟环境管理
写在前面
----

关于Python虚拟环境管理，曾经做为一名新人一直不以为意，心想反正都是我要用的库，全安装在一起，要用直接导入，多好。可是，后来，懂得越来越多的我，不仅流下了悔恨了泪水呀，这一次，关于Python虚拟环境管理的方法一网打尽，喜欢哪种方式，大家自己选吧。再说一次虚拟环境很重要。

一、使用virtualenv
--------------

### 1\. 使用pip

```text
pip install virtualenv
```

### 2\. 创建运行环境

```text
virtualenv [虚拟环境名称] 
virtualenv venv

#如果不想使用系统的包,加上–no-site-packeages参数
virtualenv  --no-site-packages 创建路径名
```

### 3\. 激活环境

linux:

```text
$ cd venv
$ source ./bin/activate
```

Windows 10:

```text
> cd venv
> .\Scripts\activate.bat
```

### 4\. 退出环境

linux:

`$ deactivate`

Windows 10:

`> .\Scripts\deactivate.bat`

### 5\. 删除环境

没有使用virtualenvwrapper前，可以直接删除venv文件夹来删除环境

### 6\. 使用环境

进入环境后，一切操作和正常使用python一样 安装包使用`pip install 包`

二、使用Virtualenvwrapper
---------------------

Virtaulenvwrapper是virtualenv的扩展包，用于更方便管理虚拟环境，它可以做： - 将所有虚拟环境整合在一个目录下 - 管理（新增，删除，复制）虚拟环境 - 快速切换虚拟环境

### 1\. 安装

```text
# on Windows
pip install virtualenvwrapper-win
# on macOS / Linux
pip install --user virtualenvwrapper
# then make Bash load virtualenvwrapper automatically
echo "source virtualenvwrapper.sh" >> ~/.bashrc
source ~/.bashrc
```

### 2\. 创建虚拟环境

```text
# on macOS/Linux:
mkvirtualenv --python=python3.6 venv
# on Windows
mkvirtualenv --python=python3 venv
```

### 3\. 激活环境

```text
workon #列出虚拟环境列表
workon [venv] #切换环境
```

### 4\. 退出环境

```text
deactivate
```

### 5\. 删除环境

```text
rmvirtualenv venv
```

### 6\. 其他有用指令

```text
pip freeze #查看当前安装库版本
#创建 requirements.txt 文件，其中包含了当前环境中所有包及 各自的版本的简单列表
#保持部署相同，一键安装所有包
pip install -r requirements.txt
pip freeze > requirements.txt 
lsvirtualenv    #列举所有的环境
cdvirtualenv    #导航到当前激活的虚拟环境的目录中，相当于pushd 目录
cdsitepackages   # 和上面的类似，直接进入到 site-packages 目录
lssitepackages     #显示 site-packages 目录中的内容
```

三、 使用conda管理
------------

> conda可以直接创建不同python版本的虚拟环境。前面讲的virtualenv只是指定创建不同python版本的虚拟环境，前提是你的电脑上已经安装了不同版本的python,与conda相比没有conda灵活。  

### 1\. 安装

下载anaconda安装的python直接可以使用conda工具

### 2\. 创建虚拟环境

创建不同的python版本，直接写出版本号就好了，还可以同时安装想要的库。

```text
# Python 2.7  
$ conda create -n venv python=2.7  

# Python 3.4  
$ conda create -n venv python=3.4  

# Python 3.5  
$ conda create -n venv python=3.5
```

### 3\. 激活虚拟环境

```text
#on windows
activate venv
#on linux
source activate venv
```

### 4\. 退出虚拟环境

```text
#on windows
deactivate
#on linux
source deactivate
```

### 5\. 删除虚拟环境

```text
# 删除一个已有环境
conda remove --name venv --all
```

### 6\. 其他有用指令

```text
# 列出系统存在虚拟环境
conda info -e
conda env list

# 查看当前环境下已安装的包
conda list

# 查看某个指定环境的已安装包
conda list -n venv

# 查找package信息
conda search numpy

# 安装package
conda install -n venv numpy
# 如果不用-n指定环境名称，则被安装在当前激活环境
# 也可以通过-c指定通过某个channel安装

# 更新package
conda update -n venv numpy

# 删除package
conda remove -n venv numpy
```

四. 使用pipenv管理
-------------

> pipenv是Python官方推荐的包管理工具。 它综合了 virtualenv , pip 和 pyenv 三者的功能。能够自动为项目创建和管理虚拟环境。如果你使用过requests库，就一定会爱上这个库，因为是同一个大神出品。 pipenv使用 Pipfile 和 Pipfile.lock 来管理依赖包，并且在使用pipenv添加或删除包时，自动维护 Pipfile 文件，同时生成 Pipfile.lock 来锁定安装包的版本和依赖信息，避免构建错误。相比pip需要手动维护requirements.txt 中的安装包和版本，具有很大的进步。  

### 1\. 安装

```text
pip install pipenv
```

### 2\. 创建虚拟环境

```text
$ cd myproject
$ pipenv install # 创建环境
$ pipenv install requests # 或者直接安装库
```

如果不存在pipfile,会生成一个pipfile，并且如果有的库添加会自动编辑该文件，不会我们手动更新requirements.txt文件了。

### 3\. 激活Pipenv Shell

```text
$ pipenv shell
$ python --version
```

编辑于 2020-03-25

**补充**
```text
pipenv --python 3.6 创建虚拟环境
vim Pipfile  —> 修改源 为阿里云镜像    https://mirrors.aliyun.com/pypi/simple
[packages] 为生产环境依赖包
[dev-packages] 为开发环境依赖包

Pipfile.lock  保存安装包的哈希值防止篡改
pipenv graph 查看安装包依赖

pipenv install requests --skip-lock   跳过lock锁定
pipenv install --dev pytest --skip-lock  开发环境安装包并跳过锁定

pipenv --where  查看所在路径 /Users/zhangfulong
pipenv --venv 查看虚拟环境所在路径 /Users/zhangfulong/.local/share/virtualenvs/zhangfulong-KNmScTXV
pipenv --py 查看虚拟环境中Python执行文件所在位置/Users/zhangfulong/.local/share/virtualenvs/zhangfulong-KNmScTXV/bin/python

 pipenv check 检查安装包的安全性

Exit 退出虚拟环境

pipenv --rm 删除虚拟环境 Removing virtualenv (/Users/zhangfulong/.local/share/virtualenvs/zhangfulong-KNmScTXV)…
```