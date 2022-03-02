#来源/转载 #解决 


[[Linux]]
[[自动化操作]]
[[Shell]]
[[操作文件]]

# Linux系统只复制文件夹的名字和结构不复制里面的文件

> 作者：BigHatMao  
> 链接：https://www.zhihu.com/question/337520589/answer/770444972  
> 来源：知乎  
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。  

只需要简单一条命令即可：


```text
find 被复制的目录路径 -type d -exec mkdir 目标目录路径/{} \; 
```

下面是演示：

-   使用tree -N命令可以看到演示目录中有文件夹有txt文本：

&lt;img src="https://pic3.zhimg.com/50/v2-caf6516cbb16052eaa4045092f89efce\_hd.jpg?source=1940ef5c" data-caption="" data-size="normal" data-rawwidth="227" data-rawheight="179" data-default-watermark-src="https://pic1.zhimg.com/50/v2-aa098c46820f089ba9a5ca0d9fd27bca\_hd.jpg?source=1940ef5c" class="content\_image" width="227"/&gt;

![](https://pic3.zhimg.com/80/v2-caf6516cbb16052eaa4045092f89efce_720w.jpg?source=1940ef5c)

-   使用命令把1-1及其目录结构复制到des目录中: 
-   命令如下： 

```bash
find ./1-1 -type d -exec mkdir ./des/{} \; 

参数：
  -type d : 表示只差早目录
  -exec <命令> 空格\;  : 表示把前面查找的结果输入到命令中作为参数，{}会被替换成搜索结果，必须\;结尾
  ./1-1 : 目标目录，这里可以使绝对路径，可以写相对路径
  ./des/{} : 表示把结果拷贝到 "./des/....."中
```

如果创建目录失败，可以尝试 mkdir -p参数，再次运行上面命令

-   结果如下：

&lt;img src="https://pic1.zhimg.com/50/v2-e1ec45829a991e34af947c13ecd11dbc\_hd.jpg?source=1940ef5c" data-caption="" data-size="normal" data-rawwidth="285" data-rawheight="213" data-default-watermark-src="https://pic4.zhimg.com/50/v2-3cc5c0381db5efc8331161e1ec56dfe0\_hd.jpg?source=1940ef5c" class="content\_image" width="285"/&gt;

![](https://pic1.zhimg.com/80/v2-e1ec45829a991e34af947c13ecd11dbc_720w.jpg?source=1940ef5c)