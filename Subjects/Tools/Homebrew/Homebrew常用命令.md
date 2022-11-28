   #来源/转载 #资料 
   
   [[homebrew]]
   [[管理工具]]
   
   
   
   

一、官方网址

[Homebrew](https://link.jianshu.com?t=https%3A%2F%2Fbrew.sh%2F)

二、目录

-   安装
-   查看帮助信息
-   查看版本
-   更新Homebrew自己
-   安装软件包
-   查询可更新的包
-   更新包 (formula)
-   清理旧版本
-   锁定不想更新的包
-   卸载安装包
-   查看包信息
-   查看安装列表
-   查询可用包
-   卸载Homebrew

三、常用命令

-   安装

//安装依赖工具  
xcode-select --install

/usr/bin/ruby -e "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/master/install](https://raw.githubusercontent.com/Homebrew/install/master/install))"

-   查看帮助信息

brew help

-   查看版本

brew -v

-   更新Homebrew自己

brew update

-   安装软件包

brew install \[包名\]

//安装git  
brew install git

//安装git-lfs  
brew install git-lfs

//安装wget  
brew install wget

//安装openssl  
brew install openssl

-   查询可更新的包

brew outdated

-   更新包 (formula)

//更新所有  
brew upgarde

//更新指定包  
brew upgarde \[包名\]

-   清理旧版本

//清理所有包的旧版本  
brew cleanup

//清理指定包的旧版本  
brew cleanup \[包名\]

//查看可清理的旧版本包，不执行实际操作  
brew cleanup -n

-   锁定不想更新的包

  
//锁定某个包brew pin $FORMULA //取消锁定brew unpin $FORMULA 

-   卸载安装包

brew uninstall \[包名\]

//例：卸载git  
brew uninstall git

-   查看包信息

brew info \[包名\]

-   查看安装列表

brew list

-   查询可用包

brew search \[包名\]

-   卸载Homebrew

cd \`brew --prefix\`rm -rf Cellar  
brew cleanup  
rm \`git ls-files\`  
rm -r Library/Homebrew Library/Aliases Library/Formula Library/Contributions  
rm -rf .git  
rm -rf ~/Library/Caches/Homebrew

四、参考文章

-   1、[你应该定期更新 Homebrew](https://link.jianshu.com?t=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000004353419)
-   2、[Homebrew简介和基本使用](https://link.jianshu.com?t=http%3A%2F%2Fblog.csdn.net%2Fandanlan%2Farticle%2Fdetails%2F51589800)
-   3、[Mac上Homebrew的使用 (Homebrew 使 OS X 更完整)](https://link.jianshu.com?t=http%3A%2F%2Fblog.csdn.net%2Fdelphiwcdj%2Farticle%2Fdetails%2F19679891)
-   4、[HomeBrew的安装和简单使用](https://link.jianshu.com?t=http%3A%2F%2Fblog.csdn.net%2Fazhou_hui%2Farticle%2Fdetails%2F49718511)
-   5、[Mac OS下包管理器Homebrew的安装与使用](https://www.jianshu.com/p/d229ac7fe77d)