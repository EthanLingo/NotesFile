# pip install




# Python Pip 参考手册 - pip install 命令 


`pip install` 命令用于安装包

## 语法

`pip install` 命令的语法格式如下

pip install \[options\] <requirement specifier> \[package-index-options\] ...

或

pip install \[options\] -r <requirements file> \[package-index-options\] ...

或

pip install \[options\] \[-e\] <vcs project url> ...

或

pip install \[options\] \[-e\] <local project path> ...

或

pip install \[options\] <archive url/path> ...

`pip install` 命令可以从以下地址安装包

-   使用需求说明符从 PiPY 或其它索引上安装
-   VCS 项目网址
-   本地项目目录
-   本地或远程源代码归档

pip 还支持从 「 需求文件 」 ( requirements file ) 安装，这为安装指定的整个环境提供了一种简便方法

## 选项

-   `-c, --constraint <file>`
    
    使用给定的约束文件约束版本，该选项可以重复添加
    
-   `-r, --requirement <file>`
    
    从给定的需求文件中安装，该选项可以重复添加
    
    按照惯例，需求文件名为 `requirements.txt`
    
-   `--no-deps`
    
    不安装包的任何依赖项
    
-   `--pre`
    
    包含预发布版本和开发版本，默认只会包行稳定的版本
    
-   `-e, --editable <path/url>`
    
    在可编辑模式下从一个本地的项目路径或 VCS URL 中安装一个项目 ( 例如，setuptools 的 「 开发者模式 」 ) 
    
-   `-t, --target <dir>`
    
    将包安装到指定目录 `<dir>`
    
    默认情况下，该选项并不会覆盖 `<dir>` 目录中已经存在的文件或目录，但可以使用 `--upgrade`选项将已经存在的包更新到最新的版本
    
-   `--user`
    
    将所有的包安装到我们的平台的Python 用户安装目录，通常为 `~/.local/` 或 Windows 上为 `%APPDATA%Python` ( 更多详细信息，可以查看 Python 文档中的 `site.USER_BASE` 部分 )
    
-   `--root <dir>`
    
    安装与此备用根目录 `<dir>` 包含的所有内容
    
-   `--prefix <dir>`
    
    安装时，`lib` 、`bin` 和其它顶级目录的存放目录，也就是这些目录的路径前缀
    
-   `-b, --build <dir>`
    
    用于存放解压缩的包和构建的包
    
    请注意，初始构建仍发生在临时目录中
    
    可以通过适当地设置 `TMPDIR` 环境变量 （ Windows上的 `TEMP` ) 来控制临时目录的位置
    
    注意，如果使用了该参数，当构建发生故障时，并不会清空构建目录
    
-   `--src <dir>`
    
    用于存放迁出的可编辑项目
    
    在虚拟环境中，默认的目录为 `<venv path>/src`， 在全局安装中，默认的目录为 `<current dir>/src`
    
-   `-U, --upgrade`
    
    更新所有指定的包到最新的可用版本。 依赖项的处理取决于所使用的升级策略
    
-   `--upgrade-strategy <upgrade_strategy>`
    
    确定应如何处理依赖项升级 ( 默认值：「 仅在需要时 」)
    
    -   `eager` \- 无论当前安装的版本是否满足升级包的要求，都会升级依赖项
    -   `only-if-needed` \- 仅在不满足升级包的要求时才升级
-   `--force-reinstall`
    
    重新安装所有的包，即使它们已经是最新的版本
    
-   `-I, --ignore-installed`
    
    忽略已经安装的包 ( 用重新安装取代 )
    
-   `--ignore-requires-python`
    
    忽略 Requires-Python 信息
    
-   `--no-build-isolation`
    
    在构建现代的源代码分发包是禁用隔离
    
    如果使用了此选项，则必须已安装 PEP518 规定的构建依赖项
    
-   `--install-option <options>`
    
    安装时提供给 `setup.py` 安装命令的额外参数( 使用方法类似于 `--install-option="--install-scripts=/usr/local/bin"` )
    
    可以使用多个 `--install-option` 选项将多个选项传递给 `setup.py install`
    
    如果你使用带有目录路径的选项，请确保使用绝对路径
    
-   `--global-option <options>`
    
    在 `bdist_wheel` 命令之前提供给 `setup.py` 调用的额外全局选项
    
-   `--compile`
    
    将 Python 源代码编译为 bytecode
    
-   `--no-compile`
    
    不要将 [Python](https://www.twle.cn/l/yufei/python30/python-30-index.html) 源代码编译为 `bytecode`
    
-   `--no-warn-script-location`
    
    当安装脚本不在 `PATH` 路径中时不要发出警告
    
-   `--no-warn-conflicts`
    
    出现已损坏的依赖关系时不要发出警告
    
-   `--no-binary <format_control>`
    
    不使用二进制包
    
    该选项可以重复添加，每增加一个就会自增当前的值
    
    可选的值有
    
    -   `:all:` ：禁用所有二进制包
    -   `:none:` ：清空集合，或者使用逗号之间的一个或多个包名称
    
    注意，某些软件包编译起来很棘手，并且，即使在添加了此选项后仍然可能无法安装
    
-   `--only-binary <format_control>`
    
    不使用源代码包
    
    该选项可以重复添加，每增加一个就会自增当前的值
    
    可选的值有
    
    -   `:all:` ：禁用所有源代码包
    -   `:none:` ：清空集合，或者使用逗号之间的一个或多个包名称
    
    注意，没有二进制发行版的软件包在使用此选项时将无法安装
    
-   `--no-clean`
    
    不要清空构建目录
    
-   `--require-hashes`
    
    对于可重复安装，需要根据哈希值来检查每个需求
    
    如果需求文件中的任何一项包含了 `--hash` 选项，则隐式包含此选项
    
-   `--progress-bar <progress_bar>`
    
    用于指定要显示的进度条类型，可选项有 `on`、`ascii`、`off`、`pretty`、`emoji`，默认为 `on`
    
-   `-i, --index-url <url>`
    
    Python 包索引的基础 URL 地址，默认为 [https://pypi.org/simple](https://pypi.org/simple)
    
    该选项的值应该指向符合 PEP503 ( 简单存储库 API ) 的存储库或以相同格式布局的本地目录
    
-   `--extra-index-url <url>`
    
    除了 `--index-url` 之外的附加的 Python 包索引 URL，规则和 `--index-url` 一样
    
-   `--no-index`
    
    忽略包索引，使用 `--find-links` 指定的 URL
    
-   `-f, --find-links <url>`
    
    如果提供的 URL 或路径链接到一个 html 文件，则会解析该 html 文件以获取归档
    
    如果是本地目录，或 `file://url` 指向的是一个目录，那么就在该目录中查找归档
    
-   `--process-dependency-links`
    
    启用依赖关系链接的处理
    

## 范例

使用 [要求描述符](https://www.twle.cn/t/85#requirement-specifiers) 从 [PyPI](https://pypi.org/) 安装 `SomePackage` 及其依赖项

$ pip install SomePackage            \# 最新版本
$ pip install SomePackage\==1.0.4     \# 指定版本
$ pip install 'SomePackage>=1.0.4'   \# 最小版本

安装文件中指定的要求列表,更多信息可以参考本章节的 [Requirements 文件](https://www.twle.cn/t/85#requirements-files)

$ pip install -r requirements.txt

升级已安装的 `SomePackage` 到 `PyPI` 中的最新版本

$ pip install --upgrade SomePackage

以 「 可编辑 」 模式从 `VCS` 安装项目，更多信息可以参考本章节的 [可编辑安装模式](https://www.twle.cn/t/85#editable-installs)

$ pip install -e .                     \# project in current directory
$ pip install -e path/to/project       \# project in another directory

安装包含 [setuptools 附件](https://setuptools.readthedocs.io/en/latest/setuptools.html#declaring-extras-optional-features-with-their-own-dependencies) 的软件包

$ pip install SomePackage\[PDF\]
$ pip install git+https://git.repo/some\_pkg.git#egg\=SomePackage\[PDF\]
$ pip install SomePackage\[PDF\]==3.0
$ pip install -e .\[PDF\]==3.0  \# editable project in current directory
$ pip install SomePackage\[PDF,EPUB\]  \# multiple extras

安装特定的源代码归档文件

$ pip install ./downloads/SomePackage-1.0.4.tar.gz
$ pip install http://my.package.repo/SomePackage-1.0.4.zip

从备用软件包存储库安装

从其它的索引处安装，而不是 `PyPI`

$ pip install --index-url http://my.package.repo/simple/ SomePackage

除了 `PyPI` 之外，安装期间还可以搜索其它索引

$ pip install --extra-index-url http://my.package.repo/simple SomePackage

从包含归档的本地目录安装，并且不扫描索引

$ pip install --no-index --find-links\=file:///local/dir/ SomePackage
$ pip install --no-index --find-links\=/local/dir/ SomePackage
$ pip install --no-index --find-links\=relative/dir/ SomePackage

除了稳定版本外，还可以查找预发布版本和开发版本

默认情况下，pip 只会查找稳定的版本

$ pip install --pre SomePackage
	
	`pip install` 命令用于安装包，在 [Python Pip 参考手册 - pip install 命令 ( 一 )](https://www.twle.cn/t/85#reply0) 章节中我们介绍了 `pip install` 命令的基本用法，可用命令行参数和一些使用范例，但我们没有对 `pip install` 命令做一些深入的了解

本章节，我们就来深入了解 `pip install` 命令

## pip install 简介

`pip install` 安装一个包时要经过几个阶段

1.  确定基本的需求 ( requirements )，用户传递的参数会在这个阶段处理
2.  解决依赖关系，要安装的内容会在这个阶段确定
3.  构建 wheels，所有的依赖项目都会在此阶段编译成 wheel
4.  安装所有的包，并卸载任何刚刚升级或替换的内容

## 参数处理

`pip install` 命令的第一阶段，在查看要安装的项目时，pip 会按照以下的顺序检查每个项目的类型

1.  项目或归档 URL
2.  本地项目 ( 必须包含 `setup.py`，否则 `pip` 会报错 )
3.  本地文件 ( 一个 sdist 或 wheel 格式归档，名字则会采用这些格式的约定 ) 
4.  PEP440 指定的需求文件 ( requirements )

每个确定的项目都会添加到安装要满足的 requirements 集合中

## 确定名称和版本

`pip install` 命令的第二个阶段，会确定依赖关系，主要就是确定每个依赖的名称和版本

对于每个候选项，`pip` 需要知道项目名称和版本。 对于 wheel ( 由 `.whl` 文件扩展名标识 )，可以根据 `Wheel` 规范从文件名中获取。 对于本地目录或显式指定的 `sdist` 文件，可以使用 `setup.py egg_info` 命令获取项目的元数据。 对于通过索引定位的 `sdists`，可以从文件名中解析出名称和项目版本 ( 虽然理论上说，这比使用 `egg_info`命令稍差，但可以避免下载和处理不必要的文件数 ）

而对于任意的 URL ，则可以通过 `egg=name` 参数 ( 请参阅 [VCS](https://www.tutorialdocs.com/tutorial/pip/reference-install.html#vcs-support) 支持 ) 获取声明的项目名称

## 满足要求

一旦 `pip` 拥有了能够满足要求的集合，它就会使用 **选择满足给定约束条件的最新版本** 这种简单来安装每个需求的版本（ 想要了解有关预发布版本的例外情况，可以参阅 [此处](https://www.tutorialdocs.com/tutorial/pip/reference-install.html#pre-release-versions)）

所选版本的如果有多个来源可用，则会假定任何一个来源都是可可接受的，否则版本会有所不同

## 控制 setup\_requires

`Setuptools` 为 `setup_requires` 提供了 `setup()` 关键字，用于在运行 `setup.py` 脚本之前设置需要预先安装的依赖项，而内部实现中，Setuptools 使用 `easy_install` 来安装这些依赖关系

pip 无法控制这些依赖项的位置，即使添加了包索引选项都不会有任何效果

如果需要实现定制，解决方案是配置 「 系统 」 或 「 个人 」 的 [`Distutils` 配置文件](http://docs.python.org/2/install/index.html#distutils-configuration-files) 来管理履行

例如，要使依赖项位于备用索引处，请添加以下内容

\[easy\_install\]
index\_url \= https://my.index-mirror.com

要使依赖项位于本地目录而不是 `PyPI` ，请添加以下内容

\[easy\_install\]
allow\_hosts \= ''
find\_links \= file:///path/to/local/archives/

## 构建系统接口

为了使 `pip install` 命令能够从源代码安装包，包的 `setup.py` 文件必须实现以下命令

setup.py egg\_info \[--egg-base XXX\]

和

setup.py install --record XXX \[--single-version-externally-managed\] \[--root XXX\] \[--compile|--no-compile\] \[--install-headers XXX\]

`egg_info` 命令用于为包创建 `egg` 元数据，详细资料可以查看 `setuptools`文档 [https://setuptools.readthedocs.io/en/latest/setuptools.html#egg-info-create-egg-metadata-and-set-build-tags](https://setuptools.readthedocs.io/en/latest/setuptools.html#egg-info-create-egg-metadata-and-set-build-tags)

`install` 应该实现将软件包安装到目标目录 `XXX` 的完整过程

为了可以用 「 可编辑 」模式 ( `pip install -e` ) 安装软件包，`setup.py` 必须实现以下命令

setup.py develop --no-deps

所以应该实现以 「 可编辑 」 模式安装包的完整过程

所有的包都会尝试安装到 `wheels` 中

setup.py bdist\_wheel -d XXX

未来，`pip install` 可能还会调用 `setup.py` 中的另一个命令

setup.py clean

调用此命令以从构建中清除临时命令 ( TODO : 此命令需要更详细地调查 )

除了以上列出的这些，`pip install` 命令不会调用调用构建系统的其它命令

从 `wheel` 中安装包根本就不会调用构建系统
	
	`pip install` 命令的知识点怎么会这么多啊，都用了两个章节感觉还没讲完，哎，本章节我们继续

## 安装顺序

从 `v6.1.0` 开始， `pip install` 命令会在安装指定的包之前先安装所有包的依赖项，即使用 「 拓扑顺序 」

这是目前唯一承诺的排序方式，尽管 Pip 可能会按照安装参数的顺序或按需求文件中的项目顺序安装，但这不是一个承若，随时都可能会变

在 **依赖循环** ( 也称为 「 循环依赖 」) 的情况下，当前实现 ( 稍后可能改变 ) 的流程是让循环遇到的第一个成员最后安装

例如，如果 `quux` 依赖于 `foo` ，而 `foo` 依赖于 `baz` ，而 `bar` 又依赖于 `foo`

pip install quux
...
Installing collected packages baz, bar, foo, quux

pip install bar
...
Installing collected packages foo, baz, bar

在 `v6.1.0` 之前，pip 没有对安装顺序做出任何承诺

拓扑安装的决定基于以下原则：**安装应该让环境在每个步骤都可用的方式进行**

这个原则会带来两大好处：

1.  安装过程中可以并行使用环境
2.  安装失败不太可能会破坏环境，虽然 pip 最终会支持故障回滚，但这只是一种改进而已

新的安装顺序的目的并不是替换（ 也不会不替换 ）使用 `setup_requires` 来声明构建依赖关系，但在下面列出的三种情况下，则是有助于某些项目从 `sdist` 安装的，这在之前的安装顺序中是可能失败的

1.  使用 `install_requires` 构建了依赖项，同时这些依赖项也被声明为安装依赖项
2.  `python setup.py egg_info` 在没有安装构建依赖项的情况下仍然可以工作
3.  无论出于何种原因，不想也不会使用 `setup_requires` 声明其构建依赖项

## 需求 ( Requirements ) 文件格式

需求文件的每一行都表示要安装的内容，跟 [pip install](https://www.twle.cn/t/85) 命令的参数一样，支持以下格式

\[\[--option\]...\]
<requirement specifier> \[; markers\] \[\[--option\]...\]
<archive url/path>
\[-e\] <local project path>
\[-e\] <vcs project url>

对于所有的格式，可以查看 [范例](https://www.twle.cn/t/85) 以了解它们是如何使用的

1.  以 `#` 开头的行是注释，在解析的时候会被忽略
    
2.  空格后跟一个 `#` 会导致 `#`和该行的其余部分被视为注释
    
3.  以未转义的 `\` 结尾的行被视为行继续，会忽略后面紧跟的换行符
    
4.  在继续处理每一行之前，首先会删除注释
    
5.  同时支持以下可选参数
    
    \-i, --index-url
    
    --extra-index-url
    
    --no-index
    
    -f, --find-links
    
    --no-binary
    
    --only-binary
    
    --require-hashes
    

例如，可以使用下面的代码指定 `--no-index` 和 `--find-links`

    --no-index
    --find-links /my/local/archives
    --find-links http://some.archives.com/archives

如果有需要，还可以使用 `-r` 引入其它需求文件，使用方式如下

    -r more\_requirements.txt

同时还可以使用 `-c` 指定约束条件

    -c some\_constraints.txt

### 使用环境变量

从 `v10` 版本开始，Pip 支持在需求文件中使用环境变量，这样我们就可以在环境变量中存储敏感数据 ( 令牌，密钥等 ) ，然后在需求文件中引用变量的名称，让 pip 在运行时查找它们的值，这种方法与常用的 [12不配置模式](https://12factor.net/config) 一致

环境变量名称必须遵循 POSIX 格式，包括大写名称旁边的括号，例如 `${API_TOKEN}`，pip 会在运行时尝试查找在主机系统上定义的相应环境变量

注意: 并不支持其它变量扩展语法，例如 `$VARIABLE` 和 `%VARIABLE%`

### 需求文件范例

将下面的内容保存到 `requirements.txt` 中，然后就可以使用 `pip install -r example-requirements.txt` 命令来安装

#
####### example-requirements.txt #######
#
###### Requirements without Version Specifiers ######
nose
nose-cov
beautifulsoup4
#
###### Requirements with Version Specifiers ######
#   See https://www.python.org/dev/peps/pep-0440/#version-specifiers
docopt == 0.6.1             # Version Matching. Must be version 0.6.1
keyring >= 4.1.1            # Minimum version 4.1.1
coverage != 3.5             # Version Exclusion. Anything except version 3.5
Mopidy-Dirble ~= 1.1        # Compatible release. Same as >= 1.1, == 1.\*
#
###### Refer to other requirements files ######
-r other-requirements.txt
#
#
###### A particular file ######
./downloads/numpy-1.9.2-cp34-none-win32.whl
http://wxpython.org/Phoenix/snapshot-builds/wxPython\_Phoenix-3.0.3.dev1820+49a8884-cp34-none-win\_amd64.whl
#
###### Additional Requirements without Version Specifiers ######
#   Same as 1st section, just here to show that you can put things in any order.
rejected
green
#

### 需求说明符

Pip 支持从包索引中使用需求说明符来进行安装，一般来说，一个需求说明符由项目名称和可选的紧跟在项目名称后的版本说明符组成

\[PEP508\] 文档包含了一份关于需求格式的完整的说明文档 (当前 `pip` 当前还不支持 `url_req` 形式的说明符)

下表列出了一些说明符的例子

SomeProject
SomeProject == 1.3
SomeProject >=1.2,<.2.0
SomeProject\[foo, bar\]
SomeProject~=1.4.2

从 `v6.0` 版开始，pip 还支持包含环境标记的说明符

如下所示

SomeProject ==5.4 ; python\_version < '2.7'
SomeProject; sys\_platform == 'win32'

环境标记在命令行和需求文件都可以使用

## 按要求覆盖

从 `v7.0` 开始，pip 支持通过使用需求文件传递和控制给 `setup.py` 的命令行选项，但以此同时也会禁用该包的 `wheels` 、缓存或其它，因为 `setup.py` 中不包含 `wheel`

`--global-option` 和 `--install-option` 选项用于将选项参数传递给 `setup.py`，例如：

FooProject >= 1.2 --global-option="--no-user-cfg" \\
    --install-option="--prefix='/usr/local'" \\
    --install-option="--no-compile"

以上内容会转换为如下运行 `FooProject` 的 `setup.py` 脚本

\# Invalid. Please use '--install-option' twice as shown above.
FooProject >= 1.2 --install-option="--prefix=/usr/local --no-compile"

## 预发布版本

从 `v1.4` 版本开始，pip 默认只会安装 [PEP426](http://www.python.org/dev/peps/pep-0426) 指定的稳定版本

如果某个版本无法解析为 PEP426 兼容的版本，则会被认定为是预发布版本

如果需求说明符包含了预发布版本或开发版本 ( 例如 `>= 0.0.dev0` )，那么 `pip` 将允许安装该需求的预发布版本和开发版本，有个例外，就是使用了 `!=` 标记

`pip install` 命令还支持 `--pre` 标志，该标志支持安装预发行版和开发版

## VCS 支持

pip 支持从 [Git](https://www.twle.cn/l/yufei/git/git-basic-index.html)、`Mercurial`、`Subversion` 和 `Bazaar` 安装，并使用 URL 前缀检测 `VCS` 的类型 `git+`、`hg+`、`bzr+`、`svn+`

pip 运行 VCS 命令需要先安装相应的客户端：`git`、`hg`、`svn` 或 `bzr`

VCS 项目可以自由选择是否在编辑模式下安装 ( 使用 `--editable` 选项 )

-   如果使用可编辑安装，在虚拟环境中，克隆的位置为 `<venv path>/src/SomeProject`，对于全局安装，则为 `<cwd>/src/SomeProject`
    
-   对于不可编辑的安装，项目在 `temp dir` 进行本地构建，然后正常安装。请注意，如果已经安装了符合要求的版本，且没有添加 `--upgrade` 标志的情况下，VCS 源将不会进行覆盖安装。VCS 要求固定提交目标的包版本号 ( 在`setup.py` 文件中指定 )，版本号不一定是提交本身
    
-   当且仅当使用可编辑模式完成安装时，[pip freeze](https://www.twle.cn/t/82#reply0) 子命令才会记录 VCS 需求说明符 ( 引用特定的提交 )
    

`pip` 会在其其依赖逻辑中使用 URL 后缀 `egg=<project name>-<version>` 作为 「项目名称 」组件，以便在 pip 下载和分析元数据之前识别项目

`egg` 值中的 `<version>` 是可选的，在功能上并不重要，它的作用仅用于改进可读性，让人们了解正在使用的版本

对于 `setup.py` 不在项目根目录中的项目，会使用 「 子目录 」 组件，「 子目录 」 组件的值为项目的根目录到 `setup.py` 文件所在的路径名

所以，如果我们存储库的采用了如下布局

| pkg\_dir/
|----| setup.py # setup.py for package pkg
|----| some\_module.py
| other\_dir/
|----| some\_file
| some\_other\_file

那么就需要使用 `pip install -e vcs+protocol://repo_url/#egg=pkg&subdirectory=pkg_dir.` 命令来安装

### Git

Pip 目前支持使用 `git`、`git+http`，`git+https`、`git+ssh`，`git+git` 和  `git+file` 进行克隆 ( clone ) 操作

下面的代码列出了这些支持的格式的用法

\[-e\] git://git.example.com/MyProject#egg=MyProject
\[-e\] git+http://git.example.com/MyProject#egg=MyProject
\[-e\] git+https://git.example.com/MyProject#egg=MyProject
\[-e\] git+ssh://git.example.com/MyProject#egg=MyProject
\[-e\] git+git://git.example.com/MyProject#egg=MyProject
\[-e\] git+file:///home/user/projects/MyProject#egg=MyProject
-e git+git@git.example.com:MyProject#egg=MyProject

同时还支持传递分支名称，提交的哈希或标记名称，如下所示

```
\[-e\] git://git.example.com/MyProject.git@master#egg=MyProject
\[-e\] git://git.example.com/MyProject.git@v1.0#egg=MyProject
\[-e\] git://git.example.com/MyProject.git@da39a3ee5e6b4b0d3255bfef95601890afd80709#egg=MyProject
```
	
当传递了提交的哈希值时，指定完整哈希比部分哈希更可取，因为完整哈希允许 pip 更有效地运行 ( 例如通过减少网络调用 )

### Mercurial

对于 Mercurial，pip 支持的协议有 : `hg+http`、`hg+https`、`hg+static-http` 和 `hg+ssh`

下面的代码列出了这些支持的协议的用法

\[-e\] hg+http://hg.myproject.org/MyProject#egg=MyProject
\[-e\] hg+https://hg.myproject.org/MyProject#egg=MyProject
\[-e\] hg+ssh://hg.myproject.org/MyProject#egg=MyProject
\[-e\] hg+file:///home/user/projects/MyProject#egg=MyProject

pip 同时还支持指定修订号，修订哈希，标记名称或本地分支名称，如下所示

\[\-e\] hg+http://hg.example.com/MyProject@da39a3ee5e6b#egg=MyProject
\[\-e\] hg+http://hg.example.com/MyProject@2019#egg=MyProject
\[\-e\] hg+http://hg.example.com/MyProject@v1.0#egg=MyProject
\[\-e\] hg+http://hg.example.com/MyProject@special\_feature#egg=MyProject

### Subversion

对于 Subversion，pip 支持的 URL 协议有： `svn`、`svn+svn`、`svn+http`、`svn+https`、`svn+ssh`

pip 还支持对 SVN URL 进行特定修订，如下所示

\[\-e\] svn+svn://svn.example.com/svn/MyProject#egg=MyProject
\[\-e\] svn+http://svn.example.com/svn/MyProject/trunk@2019#egg=MyProject

后一条语句将迁出修订版 2019，还可以使用 `@{20080101}` 迁出从 `2008-01-01` 以来的修订版，当需要迁出指定的修订版本时，只能使用 `-e svn+....`

### Bazaar

对于 Bazaar，pip 支持的协议有 `bzr+http`、`bzr+https`、`bzr+ssh`、`bzr+sftp`、`bzr+ftp`和  `bzr+lp`

下面的代码列出了这些支持的协议的用法

\[-e\] bzr+http://bzr.example.com/MyProject/trunk#egg=MyProject
\[-e\] bzr+sftp://user@example.com/MyProject/trunk#egg=MyProject
\[-e\] bzr+ssh://user@example.com/MyProject/trunk#egg=MyProject
\[-e\] bzr+ftp://user@example.com/MyProject/trunk#egg=MyProject
\[-e\] bzr+lp:MyProject#egg=MyProject

还支持标签和修订版本，如下所示

\[\-e\] bzr+https://bzr.example.com/MyProject/trunk@2019#egg=MyProject
\[\-e\] bzr+http://bzr.example.com/MyProject/trunk@v1.0#egg=MyProject

### 使用环境变量

从版本 `v10` 开始，pip 还可以使用环境变量，这样就可以引用私有存储库而无需在需求文件中存储访问令牌

例如，可以像下面的代码一样重新启用允许 Basic Auth 进行身份验证的私有 git 存储库

\[-e\] git+http://${AUTH\_USER}:${AUTH\_PASSWORD}@git.example.com/MyProject#egg=MyProject
\[-e\] git+https://${AUTH\_USER}:${AUTH\_PASSWORD}@git.example.com/MyProject#egg=MyProject

注意：仅支持 `${VARIABLE}` 语法格式，不支持 `$VARIABLE` 或 `%VARIABLE%`

## 后记

不行，接下来的内容还是太长，算了，剩下的内容挪到下一章节吧
	
	`pip install` 命令的知识点怎么会这么多啊，本来以为三个章节就差不多了，现在看来，再加上这第四个，说不定还讲不完

## 查找包

`pip install` 命令通过简单的 [HTTP](https://www.twle.cn/l/yufei/http/http-basic-index.html) 接口在 PiPY 上查找包，相关的文档可以访问 [这里](https://setuptools.readthedocs.io/en/latest/easy_install.html#package-index-api) 和 [这里](http://www.python.org/dev/peps/pep-0301/)

pip 提供了提供了许多包索引选项，用于定制包的查找方式

pip 可以从多处查找包，从 `PyPI` 上 ( 如果没有通过 `--no-index` 禁用 ) ，从本地文件系统中，以及通过`--find-links` 或 `--index` 指定的任何其他存储库 URL

搜索的位置没有优先级，而是全部检查，然后选择 「 最佳 」 匹配要求 ( 有关版本号的知识，可以访问 PEP440 了解详细信息 ) 

关于查找包的范例，可以访问 [Python Pip 参考手册 - pip install 命令 ( 一 )](https://www.twle.cn/t/85)

## SSL 证书验证

从 `v1.3` 开始，pip 通过 `https` 提供 SSL 证书验证，以防止针对 PyPI 下载的中间人攻击

## 缓存

从 `v6.0` 开始，pip 提供了一个功能类似于 Web 浏览器的默认启用 ( `on-by-default` ) 的缓存系统

虽默认情况下缓存处于启用状态，且默认情况下也会正确的运行，但我们可以使用 `--no-cache-dir` 选项禁用缓存并始终访问 PyPI

在进行任何实质性的 [HTTP](https://www.twle.cn/l/yufei/http/http-basic-index.html) 请求前，pip 首先会检查本地缓存，以确定本地是否存在针对该请求的合适的本地响应，如果存在，则直接返回该响应，而不是从远程 PiPY 获取

如果本地缓冲中存在该请求的包，但包已经过时，那么它将会尝试发出条件请求以刷新本地缓存，该请求可能会收到一个空的响应，告诉 pip 应该使用缓存项 ( 并刷新过期时间 )，也可能收到一个全新的响应，而 pip 就可以把该响应保存到缓存中

将响应保存到缓存中时，pip 会首先使用 `CacheControl` 响应头，如果存在的话，否则使用 `Expires`响应头，如果存在的话

这种缓存行为可以将 pip 作为浏览器来使用，允许 pip 与索引服务器进行通讯，以便确定特定项目的缓存时长

这种缓存系统非常强大，能够最小化网络活动，但它并不完全网络访问，如果你需要绕过访问 PyPI 而使用本地安装，请访问 [本地软件包安装](https://www.twle.cn/t/69) 以获得更多信息

缓存目录的默认位置取决于操作系统

1.  在 `Unix` 上，一般为 `~/.cache/pip`，但也同时受 `XDG_CACHE_HOME` 环境变量影响
    
2.  在 `macOS` 上，为 `~/Library/Caches/pip`
    
3.  在 `Windows` 上，为 `<CSIDL_LOCAL_APPDATA>\pip\Cache`
    

### Wheel 缓存

Pip 会从 pip 缓存目录中的子目录 `wheels` 中查找并使用在那里找到的任何包，这也可以通过使用禁用 HTTP 缓存的 `--no-cache-dir` 选项来禁用

pip wheels 缓存的内部结构不是 pip API 的一部分，从 `v7.0` 版本开始，pip 为每个构建 wheel 的 sdist 创建一个子目录，并将结果 wheel 放在里面

Pip 会尝试从这些构建中选择最合适的 wheel，但其实更偏爱构建一个新的 wheel，这意味着当一个包包含了可选的 C 扩展并且构建带有 `py` 标记的 wheel 时，当无法构建 C 扩展时，只要任何通用的 wheel 已经构建，那么 pip 将不会尝试为支持它的 Pythons 构建更好的 wheel

为了纠正这个问题，可以使用 Python 特定标记来构建 wheel

当没有找到一个 sdist wheels 时，pip 将尝试自动构建一个 wheel 并将其插入 wheels 缓存中

## 哈希校验模式

从 `v8.0` 开始，pip 支持使用本地哈希值来检查检查下载的包归档，防止被远程篡改，如果要使用一个或多个哈希值来验证包，可以将这些哈希值添加到行的末尾，就像下面的代码一样

FooProject == 1.2 --hash=sha256:2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824 \\
    --hash=sha256:486ea46224d1bb4fb680f34f7c9ad96a8f24ec88be73ea8e5a6c65260e9cb8a7

支持使用多个哈希是很重要的，因为包可能同时存在二进制和源代码分发，或者存在为各种平台提供二进制分发，这些分发的哈希值是不一样的，如果要跨平台构建，那么就要添加多个哈希值

目前推荐的哈希算法是 `sha256`，但 pip 支持 `hashlib` 模块中的所有哈希算法，但是，请不要使用比较弱的哈希算法，比如 `md5`，`sha1`和 `sha224` ，以免带来错误的安全感

需要注意的是，哈希校验的选择只能是全有或全无，出于任何要求而使用 `--hash` 选项不仅会检查该哈希值，还会激活全局哈希检查模式，这会强加其它几个安全限制

1.  所有的需求 ( requirements ) 都需要哈希值，很少使用部分散列的需求文件，因为它可能带来一个安全隐患：恶意代理可能会通过其中一个未处理的需求将错误的代码放入安装的包中
    
    请注意，在 URL 中使用 `#md5 = ...` 添加的哈希值同样也会带来安全隐患，因为 md5 是可碰撞的，无论强度如何，因此我们需要使用使用更强大的哈希值，例如 `sha256`
    
2.  所有依赖项都需要哈希值，如果需求文件中存在某个未添加哈希值的依赖项，同样会导致错误
    
    记住上面说的全有或全无，要么所有的需求都添加哈希值，要么都不添加
    
3.  如果使用了哈希校验，项目名称 ( 而不是 URL 或本地文件系统路径) 形式的需求必须使用 `==` 符号固定到特定版本，防止使用了与需求说明符匹配的新版本时出现哈希不匹配的情况
    
4.  如果使用了哈希校验，则不允许再使用 `--egg` ，因为它会将依赖项的安装委托给 `setuptools`，这使得 pip 无法执行上述任何一项安全检查
    

可以使用 `--require-hashes` 命令行选项强制使用哈希检查模式

$ pip install --require-hashes -r requirements.txt
    ...
    Hashes are required in --require-hashes mode (implicitly on when a hash is
    specified for any package). These requirements were missing hashes,
    leaving them open to tampering. These are the hashes the downloaded
    archives actually had. You can add lines like these to your requirements
    files to prevent tampering.
        pyelasticsearch\==1.0 --hash\=sha256:44ddfb1225054d7d6b1d02e9338e7d4809be94edbe9929a2ec0807d38df993fa
        more-itertools\==2.2 --hash\=sha256:93e62e05c7ad3da1a233def6731e8285156701e3419a5fe279017c429ec67ce0

这种强制模式在部署脚本中很有用，可以确保需求文件的作者提供哈希值，这也是一种获取哈希值列表的便捷方式，因为它会显示所获取的包的哈希值

但这个选项仅为每个包提取首选归档，因此我们可能需要使用 [pip hash](https://www.twle.cn/t/75#reply0) 命令给备用归档添加哈希，例如，同时存在二进制和源分发的时候

### 哈希检查模式下会禁用 wheel 缓存

哈希检查模式下会禁用 **wheels 缓存**，以防止出现虚假哈希不匹配的错误，这种错误一般出现在安装已经自动构建到缓存 wheels 中的 `sdists` 时，因为这些 wheels 将被选中进行安装，但它们的哈希值与需求文件中的 sdist哈希值不匹配。

更复杂的是，本地构建的 wheels 是不确定的，因为会把修改时间加入归档中，使得哈希在机器和缓存刷新之间变得不可预测

[C](https://www.twle.cn/l/yufei/cprogramming/cprogramming-basic-index.html) 代码的编译进一步增加了非确定性，因为许多编译器在其输出中包含随机种子值

当然了，也不要太悲观，至少，从索引服务器获取的 wheels 每次都是相同的，它们会保存在本地的 HTTP 缓存中，而不是 wheels 缓存中，因此，在哈希检查模式下也是可用的

因此，禁用 wheels 缓存的唯一缺点是为 sdists 提供额外的构建时间，这可以使用索引服务器提供预构建的 wheels 来解决

哈希检查模式也适用于 [pip download](https://www.twle.cn/t/84#reply0) 命令和 [pip wheel](https://www.twle.cn/t/76#reply0) 命令，同时我们也在用户指南章节中详细阐述了 [散列检查模式与其他可重复性策略的比较](https://www.twle.cn/t/65#reply0)

警告：请注意 `setup.py` 中的 `setup_requires` 变量，会 (比较罕见) 导致软件包的依赖项直接由 `setuptools` 下载，跳过 pip 的哈希检查，如果你需要使用这样的包，可以访问 [控制 setup\_requires](https://www.tutorialdocs.com/tutorial/pip/reference-install.html#controlling-setup-requires)

警告：通过直接使用 `setuptools` 安装实际项目时，请注意不要使所有安全工作无效，例如，通过调用 `python setup.py install` 或 `python setup.py develop` 或 `easy_install`。`setuptools` 会下载，不检查需求文件中缺失的任何内容，随着项目的发展，很容易错过任何内容。安全起见，你应该使用 `pip install --no-deps` 安装项目

可以使用下面的命令代替 `python setup.py develop`

pip install --no-deps -e .

可以使用下面的命令代替 `python setup.py install`

pip install --no-deps .

### 从 PiPY 返回的哈希摘要

每个包的下载网址的哈希部分，PiPY 都添加了该包的 MD5 哈希摘要值，如 `＃md5=123...` ，用于 pip 检查下载的包是否遭到损坏

除了 md5 外，此处还可以使用其它的 hashlib 模块支持的哈希算法：`sha1`、`sha224`、`sha384`、`sha256` 和 `sha512`

由于这个哈希是远程生成的，因此并不能够有效的防止篡改，也就不满足 `--require-hashes` 选项要求的每个包都有一个本地哈希

## 「 可编辑 」 安装

「 可编辑 」 安装基本上就是 [setuptools 开发模式](https://setuptools.readthedocs.io/en/latest/setuptools.html#development-mode) 安装

我们可以在 「 可编辑 」 模式下安装本地项目或 VCS 项目

$ pip install -e path/to/SomeProject
$ pip install -e git+http://repo/my\_project.git#egg\=SomeProject

有关 [VCS 相关语法](https://www.twle.cn/t/87#reply0) 的详细信息，可以阅读前面章节中的 [VCS 支持部分](https://www.twle.cn/t/87#reply0)

对于本地项目，`SomeProject.egg-info` 是相对于项目路径创建的，这比仅使用 `setup.py develop` 更有优势，因为它直接相对于当前工作目录创建 `egg-info`