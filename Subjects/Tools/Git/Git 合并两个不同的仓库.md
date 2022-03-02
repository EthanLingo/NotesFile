
#用途/解决 
#内容/Git


# Git 合并两个不同的仓库


[![图南](https://pic2.zhimg.com/v2-0ba7eb9a23eedcdead4e2221679a32a2_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/tu-nan-sui-bi)

[图南](https://www.zhihu.com/people/tu-nan-sui-bi)

​关注

9 人赞同了该文章

## **应用场景：**

应用场景1：A公司的几个项目是找第三方B公司做的，每次发版上线的时候，A公司需要把B公司的代码合并到自己的代码库，然后发版部署 

应用场景2：有系统基础脚手架B，A系统是在这个脚手架基础上开发的，A和B不在一个git仓库中，有时候脚手架B也会更新迭代，这个时候就需要把脚手架B合并到已经开发的系统A中 

以上两个场景，都需要合并两个不同仓库的代码 

## **部署步骤：**

下载A公司的代码分支，并切换到test分支 

```text
git clone https://git.test1.tech/project/A.git 
git checkout test 
```

添加需要合并的B公司远程仓库 

```text
git remote add project_B http://git.test2.com/project/B.git 
```

把project_B远程仓库中数据抓取到本仓库 

```text
git fetch project_B 
```

checkout 切换到project_B的master分支上，命名为test_B 

```text
git checkout -b test_B project_B/master 

// 查看所有分支，可以看到 master、test、test_B三个分支 
git branch 
```

切换到test分支 

```text
git checkout test 
```

合并 

```text
git merge test_B 
```

合并报错： 

```text
fatal: 拒绝合并无关的历史 
```

解决： 

```text
git merge test_B --allow-unrelated-histories 
```

合并完成后会出现很多冲突（第一次合并会出现很多冲突，后续会好很多），需要再本地代码中解决冲突，然后编译没有问题，再提交到test中 

```text
git push
```

最后把test分支合并到master上线就可以了 

本文的思路是伪造远程的B仓库为A仓库的一个分支，然后合并进来 

更多内容，请点击查看下面的扇贝编程，带你打开编程世界的大门，适合零基础入门人员、想提高工作效率的人员和专业编程技能人员，它提供了Python基础课、爬虫课、Python数据分析课和自动化办公实践等，可以更快的提高技术水平，提交工作效率：