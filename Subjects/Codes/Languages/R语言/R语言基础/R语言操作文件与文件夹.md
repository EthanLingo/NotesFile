# R语言操作文件与文件夹

tags: #内容/编程/R语言 #来源/转载 



有时候，编写代码时，需要查看一下当前文件夹的内容，有时候需要创建文件或者文件夹，之前都是在windows系统或者Linux系统下创建好，但总不够原滋原味。这里，总结一下常用的文件创建，文件夹创建，判断是否存在，文件复制，文件删除等操作。

**「太长不看版：」**

```R
## 浏览功能
dir # 浏览整体文件及文件夹
list.files # 浏览文件
list.dirs # 浏览文件夹

## 判断功能
file.exists # 判断文件是否存在
dir.exists # 判断文件夹是否存在

## 创建功能
file.create # 创建文件
dir.create # 创建文件夹

## 重命名功能
file.rename # 重命名文件和文件夹

## 删除功能
file.remove # 删除文件
unlink # 删除文件夹

## 复制功能
file.copy # 复制文件
```

## **1. 文件浏览**

共有三个：

- dir() # 全部的文件和文件夹
- list.files() # 全部的文件
- list.dirs() # 全部的文件夹

**「语法：」**

```R
dir(path = ".", pattern = NULL, all.files = FALSE,
           full.names = FALSE, recursive = FALSE,
           ignore.case = FALSE, include.dirs = FALSE, no.. = FALSE)
           
list.files(path = ".", pattern = NULL, all.files = FALSE,
           full.names = FALSE, recursive = FALSE,
           ignore.case = FALSE, include.dirs = FALSE, no.. = FALSE)

list.dirs(path = ".", full.names = TRUE, recursive = TRUE)
```

**「举个例子：」**

![img](R语言操作文件与文件夹.assets/v2-da5ff0c913832b3b2d70d7082b4c2acf_1440w.jpg)

**「R语言实现：」**



```R
# 浏览功能

## 浏览全部
dir()

## 浏览文件夹
list.dirs()

## 浏览文件
list.files()
```

## **2. 判断文件和文件夹是否存在**

编写代码时，经常用到，如果不存在文件夹，就创建文件夹。或者如果不存在某个文件，就怎么样……

**「file只能判断文件，dir只能判断文件夹」**

```R
file.exists("1.txt")
file.exists("单位.txt")

file.exists("文件夹1/")

dir.exists("单位.txt")
dir.exists("文件夹1/")
```

![img](R语言操作文件与文件夹.assets/v2-5c5dbb48b336f8bb21082bd75296a243_1440w.jpg)

## **3. 文件复制**

file.copy只能复制文件，不能复制文件夹，如果复制成功，会出现TRUE，不成功是返回FALSE

```R
# 文件复制
file.copy("单位.txt","aaa.txt")
list.files()

file.copy("文件夹1/","file_dir_copy_test")
list.files()
```

![img](R语言操作文件与文件夹.assets/v2-c0f92aaa97ff15af9b737bc175c903fb_1440w.jpg)

## **4. 文件重命名**

file.rename，可以修改文件名，不可以修改文件夹名

```R
# 文件移动或重命名
file.rename("aaa.txt","bbb.txt")
dir()

file.remove("文件夹1 - 副本/","direc_test")
```

![img](R语言操作文件与文件夹.assets/v2-087786197f910c4eeacd152a73f1b6be_1440w.jpg)

## **5. 文件和文件夹删除**

**「文件删除`file.remove`」**

```R
# 删除，remove
dir()
file.remove("aaa.txt")
dir()
```

![img](R语言操作文件与文件夹.assets/v2-0bd8b111a7204abf81d02664bdd34626_1440w.jpg)

**「文件夹删除`unlink`」**

文件夹删除： unlink

注意，要删除文件夹：

- 不要写/， 比如unlink("a/")，是不会成功的
- 要加上参数，recursive = T

完整的写法：

```R
dir()
unlink("新建文件夹/",recursive = T)
dir()

unlink("新建文件夹",recursive = T)
dir()
```

![img](R语言操作文件与文件夹.assets/v2-b4b4b888daffce0a6a5f03d8d1aca9d2_1440w.jpg)

## **5. 文件和文件夹创建**

![img](R语言操作文件与文件夹.assets/v2-52fbc2d9017567a201cd7259b7c34022_1440w.jpg)

**「文件创建：`file.create`」**

```R
> file.create("a1.txt")
[1] TRUE
```

**「文件夹创建：`file.create`」**

```R
> dir.create("file1")
>
```

![img](R语言操作文件与文件夹.assets/v2-e8cc5daedbdc65f52f84549349aa5dab_1440w.jpg)

## **6. 汇总**

### **6.1 dir前缀的函数，是文件夹的操作**

- dir.create，创建
- dir.exists，是否存在
- dir，浏览

![img](R语言操作文件与文件夹.assets/v2-67cf79bccfde6f79159577227d7403fa_1440w.jpg)

### **6.2 file前缀的函数，是文件的操作**

![img](R语言操作文件与文件夹.assets/v2-665676a7705354bbf56e8754c08de816_1440w.jpg)

![img](R语言操作文件与文件夹.assets/v2-373f0a1f377ef5da39781e1cb30bcc6a_1440w.jpg)

![img](R语言操作文件与文件夹.assets/v2-00341b2747ebba8d19f2bcf2de858961_1440w.jpg)

## **7. 举个例子**

**「创建文件夹写入文件」**

> ❝ 如果当前路径中，存在result文件夹，就往里面写入1.txt, 2.txt ……20.txt等20个文件。如果不存在result文件夹，就创建文件，然后往里面写入txt文件。
> ❞

```R
# ex1
dir()
if(! dir.exists("result")){
  dir.create("result")
}
namelist = str_c(1:20,".txt")
namelist

map(namelist,~file.create(str_c("result/",.)))
```

**「代码：」**

- 首先检查是否存在，如果不存在就创建
- 建立一个文件名
- 用map函数进行批量创建，里面用了str_c，里面用了匿名函数



![img](R语言操作文件与文件夹.assets/v2-d88b890d81c32c2570ac36faad64b093_1440w.jpg)

看一下效果： 

![img](R语言操作文件与文件夹.assets/v2-b8d827cee26ab6f4172a5987663df73f_1440w.jpg)



搞定，666！

