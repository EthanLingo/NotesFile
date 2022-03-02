


#内容/Git 
#解决 
#教程 




# [Git克隆部分文件](https://www.cnblogs.com/xilifeng/p/5225666.html)

[克隆部分文件](https://www.cnblogs.com/xilifeng/p/5225666.html#header-c47)[总结一下](https://www.cnblogs.com/xilifeng/p/5225666.html#header-c86)[一个完整的例子:](https://www.cnblogs.com/xilifeng/p/5225666.html#header-c123)

## 克隆部分文件

http://blog.csdn.net/linlzk/article/details/49019787 在进行项目开发的时候，有时候会有这样的需求那就是：我们只希望从Git仓库里取指定的文件或者文件夹出来。在SVN里面，这非常容易实现，因为SVN基于文件方式存储，而Git却是基于元数据方式分布式存储文件信息的，它会在每一次Clone的时候将所有信息都取回到本地，即相当于在你的机器上生成一个克隆版的版本库。

**因此在Git1.7.0以前，这无法实现，但是幸运的是在Git1.7.0以后加入了Sparse Checkout模式，这使得Check Out指定文件或者文件夹成为可能。**

具体实现如下：

```
mkdir project_folder

cd project_folder

git init

git remote add -f origin <url>
```

上面的代码会帮助你创建一个空的本地仓库，同时将远程Git Server URL加入到Git Config文件中。 接下来，我们在Config中允许使用Sparse Checkout模式： 

```
git config core.sparsecheckout true
```

接下来你需要告诉Git哪些文件或者文件夹是你真正想Check Out的，你可以将它们作为一个列表保存在.git/info/sparse-checkout文件中。 例如： 

```
echo “libs” >> .git/info/sparse-checkout

echo “apps/register.go” >> .git/info/sparse-checkout

echo “resource/css” >> .git/info/sparse-checkout
```

最后，你只要以正常方式从你想要的分支中将你的项目拉下来就可以了：

```
git pull origin master
```



## 总结一下

1.指定远程仓库

2.指定克隆模式: 稀疏克隆模式

3.指定克隆的文件夹(或者文件)

4.拉取远程文件





```
git remote add -f origin <url>
git config core.sparsecheckout true
echo “resource/css” >> .git/info/sparse-checkout #resource/css路径
git pull origin master
```



## 一个完整的例子:

```
  mkdir gitSparse
  cd gitSparse/
  git init
  git remote add -f origin https://github.com/bestswifter/MySampleCode.git
  ls
  git config core.sparsecheckout true
  echo "CornerRadius" >> .git/info/sparse-checkout
  cat ./.git/info/sparse-checkout 
  git pull origin  master 
```













by zuo.xue[AT]outlook[DOT]com 2021