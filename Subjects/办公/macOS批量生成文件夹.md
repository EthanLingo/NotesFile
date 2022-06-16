
tags: #类型/解决 #类型/教程 #来源/转载 

[[办公自动化]]
[[文件夹]]

# macOS批量生成文件夹

我们在工作中常常利用文件夹的形式来呈现最佳工作流，比如在我自己开发课程的过程中，会给一个课程项目划分了如下几个子文件夹：

-   01_Scripts：课程脚本
-   02_Slides：课程演示文档
-   03_ExerciseFiles：课程配套文件
-   04_Design：设计文件资料
-   05_Marketing：营销活动资料
-   06_Operation：教务活动资料

当时当我要研发新的课程的时候，再重新根据这些文档来新建显然是非常浪费时间的，所以我们就需要一个可以根据这个「模版」自动批量新建文件夹的工具：Mac Terminal。

## 方法一：Mkdir

你可以打开 Mac 的命令行工具 Terminal，然后使用`cd`到具体的需要创建子文件夹的文件夹里，再执行对应的命令`mkdir`命令：

```
cd /Users/aban/Documents/Sites/course
mkdir "01_Scripts" "02_Slides" "03_ExerciseFiles" "04_Design" "05_Marketing" "06_Operation"
```

这样一来，系统就会自动在Course的文件夹里头创建了5个子文件夹了。

## 方法二：Mkdir

如果你的文件夹一多，这样手动输入的方式也不是特别的方法。所以我们可以先把对应的「子文件夹名」输入到`txt`文档中，比如`dirlist.txt`，然后在保存到具体的需要创建子文件夹的文件夹里：

```
01_Scripts
02_Slides
03_ExerciseFiles
04_Design
05_Marketing
06_Operation
```

然后还是使用 Terminal `cd`命令进入到这个文件夹里，然后使用更为更强大的`xargs`命令：

```
cd /Users/aban/Documents/Sites/course
cat dirlist.txt | xargs mkdir
```

用这个方法，还是同样可以在Course的文件夹里头创建同样的5个子文件夹。

这样一来，下一次当你需要同样的项目结构的时候，只要输入这行短短的命令，所有的文件夹就会自动新建完成了。