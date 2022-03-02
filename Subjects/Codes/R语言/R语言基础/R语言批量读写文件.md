# R语言批量读写文件

#内容/编程/R语言 
#内容/读写文件 


## 用xlsx包

在对很多数据处理时，通常要循环读取文件夹中的文件，这个时候需要批量读取和写入文件，在R语言中，批量读取和写入文件夹中文件的方法如下所示。

批量读取文件



```R
##读取同一目录下的所有文件
path <- "E:/实验数据/UseData/2013"
fileNames <- dir(path) 
filePath <- sapply(fileNames, function(x){ 
  paste(path,x,sep='/')})   
data <- lapply(filePath, function(x){
  read.csv(x, header=T)})  
```

批量输出文件

对结果批量输出csv文件,其中data为list格式

```R
outPath <- "E:/实验数据/UseData/2013" ##输出路径
out_fileName <- sapply(names(data),function(x){
                    paste(x, ".csv", sep='')}) ##csv格式
out_filePath  <- sapply(out_fileName, function(x){
                     paste(outPath ,x,sep='/')}) ##输出路径名
##输出文件
for(i in 1:length(data)){
  write.csv(data[[i]], file=out_filePath[i], row.name=F) 
}
```
————————————————
版权声明：本文为CSDN博主「HuFeiHu-Blog」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
[原文链接](https://blog.csdn.net/u011596455/article/details/79601113)



## 用