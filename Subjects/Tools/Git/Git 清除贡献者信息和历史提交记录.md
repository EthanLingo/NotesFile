---
title: Git 清除贡献者信息和历史提交记录
authors: Ethan Lin
year: 2023-11-30
tags:
  - 类型/笔记
  - 日期/2023-11-30
  - 内容/Git
  - 来源/转载
---


如果我们用git与github扒了别人的开源代码，想拿来用到自己项目中，但是提交过后，会发现仓库的历史记录又臭又长，贡献者里还有别人的名字，打算把历史记录全部清除并且让目前所有文件全部变成首次 commit 的状态。可以试试以下这个方法，包你百试百灵！

1.Checkout
检出新的分支

```
# orphan参数用于创建没有commit记录的分支
$ git checkout --orphan latest_branch
```

2.Add all the files
添加分支的所有文件
```
$ git add -A
```

3.Commit the changes
提交更改并写明提交描述
```
$ git commit -am "这是我提交的描述"
```

4.Delete the branch
删除之前的主分支
```
$ git branch -D master
```

5.Rename the current branch to master 
将当前这个分支重命名为master，是它变成主分支
```
$ git branch -m master
```

6.Finally, force update your repository
最后，强制更新到主分支master
```
$ git push -f origin master
```

总结：大概步骤就是把master分支复制，删除原有分支，用新的分支覆盖旧分支。从而完成分支替换，清除历史记录。

注意：历史记录清除后无法回滚。目前这个仓库算是一个新的仓库，以后所有的修改只需要在现在基础上修改。

————————————————
版权声明：本文为CSDN博主「Liu_Wd」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Liu_Wd/article/details/120910899