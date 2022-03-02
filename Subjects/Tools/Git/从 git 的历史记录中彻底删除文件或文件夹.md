#用途/解决
#来源/转载 
#内容/Git 

[[Git进阶操作]]



# 从 git 的历史记录中彻底删除文件或文件夹







如果你对外开源的代码中出现了敏感信息（例如你将私钥上传到了仓库中），你可能需要考虑将这个文件从 git 的历史记录中完全删除掉。

本文介绍如何从 git 的历史记录中彻底删除文件或文件夹。

第一步：修改本地历史记录

彻底删除文件：

`git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch 《你要删除的文件名称比如walterlv.xml》' --prune-empty --tag-name-filter cat -- --all`

其中 walterlv.xml 是本来不应该上传的私钥文件，于是使用此命令彻底删除。后面的命令 --tag-name-filter 指所有相关的标签都需要更新。

彻底删除文件夹：

`git filter-branch --force --index-filter 'git rm --cached -r --ignore-unmatch 《你要删除的文件夹名称》' --prune-empty --tag-name-filter cat -- --all`

删除文件夹时需要额外带一个 -r 选项，并指定文件夹名称，这里的例子是 WalterlvDemoFolder。

第二步：强制推送到远端仓库

刚刚我们的操作仅仅发生在本地仓库，敏感信息需要删除的仓库通常都在远端，于是我们一定要将修改推送到远端仓库。

需要推送的目标分支包括我们所有长期维护的分支，这通常就包括了 master 分支和所有的标签。

于是使用推送命令：

`git push 《你的远程仓库名》 《你的本地分支名》:《你的远程分支名》 --tags --force`

我的博客会首发于 https://blog.walterlv.com/，而 CSDN 会从其中精选发布，但是一旦发布了就很少更新。

如果在博客看到有任何不懂的内容，欢迎交流。我搭建了 dotnet 职业技术学院 欢迎大家加入。



> 本作品采用知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议进行许可。欢迎转载、使用、重新发布，但务必保留文章署名吕毅（包含链接：https://walterlv.blog.csdn.net/），不得用于商业目的，基于本文修改后的作品务必以相同的许可发布。如有任何疑问，请与我联系。
------------------------------------------------
版权声明：本文为CSDN博主「walter lv」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/WPwalter/article/details/100157721