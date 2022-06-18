> 转载自[http://kz16.top/md](http://kz16.top/md)

tags: #来源/转载 #内容/Markdown 

# 1. markdown教程案例

## 1.1. 标题

要注意空格与空行, 例如

```
题目
===

小标题
---

# 一级标题

## 二级标题

### 三级标题

```

## 1.2. 列表

可以用`-`  `*`  `+`三种任意一种, 要注意空格

-   第1节
    -   第1.1节
    -   第1.2节
-   第2节

```
- 第1节
	- 第1.1节
	- 第1.2节
- 第2节

```

## 1.3. 复选框

-    复选框  `- [x] 复选框`
    
-    复选框  `- [] 复选框`
    

## 1.4. 常用

-   **加粗**  `**加粗**`
    
-   用Esc键下面的~ 键可得到`阴影`, 例如
    
    ```
    `阴影菌`
    ```
    
-   Esc上面加个凸出方框`<kbd>Esc</kbd>`
    
-   [链接](https://kz16.top/)  `[链接](https://kz16.top/)`
    
-   [鼠标悬浮在链接上](https://kz16.top/ "链接解释")  
    `[鼠标悬浮在链接上](https://kz16.top/ "链接解释")`
    
-   书签目录  `[TOC]`
    
-   注释  `<!--我是注释菌, 你看不见我-->`
    
-   表格找它就对了  [https://kz16.top/ckeditor/](https://kz16.top/ckeditor/)
    
    ```
    |1|22|333|4444|
    |:--:|:--|--:|--|
    |55555|666666|7|8|
    ```
    
    1
    
    22
    
    333
    
    4444
    
    55555
    
    666666
    
    7
    
    8
    
-   公式找它就对了  [https://kz16.top/latex/symbol/](https://kz16.top/latex/symbol/)
    
-   加入代码块, 以Python为例:
    
    ```
        ```python
        print("hello, python")
        ```
    ```
    
    print("hello, python")
    

1.  插入图片的方法一  
    `![](https://kz16.top/circle.svg)`
    
2.  插入图片的方法二(该方法同样适用于链接)
    
    ```
    ![][f]
    
    [f]:https://kz16.top/circle.svg
    ```
    
3.  插入图片的方法三  
    `<img src="https://kz16.top/circle.svg" width="50">`
    
4.  上面三种方法都可以得到下面的动图, 要想插入本地图, 可以把图片转为Base64代码, 推荐在线转换 [https://kz16.top/png2base64.html](https://kz16.top/png2base64.html)
    
    ![](https://kz16.top/circle.svg)
    
5.  链接和图片的区别其实只差一个感叹号
    

## 1.5. 段落

```
第一段第一行, 行尾空两格  
第一段第二行

第二段与第一段要空行
```

第一段第一行, 行尾空两格  
第一段第二行

第二段与第一段要空行

## 1.6. 字体格式

_斜体文本1_  _斜体文本2_  
**粗体文本1**  **粗体文本2**  
_**粗斜体文本1**_  _**粗斜体文本2**_  
下划线文本  ~~删除线文本~~  
变为红色  
高亮显示

```
*斜体文本1*   _斜体文本2_ 
**粗体文本1**  __粗体文本2__ 
***粗斜体文本1***  ___粗斜体文本2___
<u>下划线文本</u>  ~~删除线文本~~
变为<font color="red">红</font>色
==高亮显示==
```

## 1.7. 区块

```
> 最外层 
> 最外层 
> > 第一层
> > > 第二层
```

> 最外层  
> 最外层
> 
> > 第一层
> > 
> > > 第二层

## 1.8. 尾注

-   尾注[[1]](https://kz16.top/md/#fn1)
    
-   尾注[[2]](https://kz16.top/md/#fn2)
    

```
- 尾注^[我是尾注菌1] 

- 尾注[^尾注菌2] 

[^尾注菌2]: 我是尾注菌2
```

## 1.9. 公式

已知∣x∣+∣y∣=0∣x∣+∣y∣=0, 则

x=y=0(2)x=y=0(2)

引用公式[(2)](https://kz16.top/md/#eq2)的结果

```
已知$|x|+|y|=0$, 则

<p id="eq2">

$$\tag{2}
x=y=0
$$

引用公式[(2)](#eq2)的结果
```

**注:** markdown做公式标签略微麻烦,  `<p>`标签为了瞄点, 从而让公式的链接生效. 部分md编辑器会自动生成`</p>`

## 1.10. 分割线

三个减号 `---`

## 1.11. 打印分页

只需添加下面代码

<div STYLE="page-break-after: always;"></div>

## 1.12. 流程图

参考 [mermaid官方文档](https://github.com/mermaid-js/mermaid/blob/develop/README.zh-CN.md)

DogsCatsRats

```
	```mermaid
	flowchart LR
	A[Hard] -->|Text| B(Round)
	B --> C{Decision}
	C -->|One| D[Result 1]
	C -->|Two| E[Result 2]
	```

	```mermaid
	pie
	"Dogs" : 386
	"Cats" : 85
	"Rats" : 15
	```
```

## 1.13. 总结警告和标注

Summary

总结

Warning

警告

Note

标注

!!! summary
    总结 

!!! warning
    警告

!!! Note
    标注

## 1.14. 配合html语言

点我查看折叠内容

我是文字滚动菌

---

这种上下局部滚动可以适用于长代码块  
第1行  
第2行  
第3行  
第4行  
第5行  
第6行  
...

---

这种可以适用于长公式  
x=a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+gx=a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g​

上面的例子分别代码为

<details>
<summary>点我查看折叠内容</summary>

- 我是折叠菌内容
- 我是折叠菌内容

</details>

<marquee>我是文字滚动菌</marquee>

---

<div style="height: 80px; overflow-y: scroll;">

这种上下局部滚动可以适用于长代码块 
第1行
第2行
第3行
第4行
第5行
第6行
...
</div>

---

<div style="overflow-x: auto; display: block;">

这种可以适用于长公式
$x=\sqrt{a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g+a+b+c+d+e+f+g}$
</div>

## 1.15. 插入GeoGebra交互动图

参考这里 [https://kz16.top/geogebra/ggbmd.html](https://kz16.top/geogebra/ggbmd.html)  
参考效果 [https://kz16.top/geogebra/offiex/xcg.html](https://kz16.top/geogebra/offiex/xcg.html)

# 2. markdown小技巧

## 2.1. markdown插入图片比较好的一种方案

-   别用图床, 不安全
    
-   别用图床, 不安全
    
-   别用图床, 不安全
    
-   先用这个网站  [https://kz16.top/png2base64.html](https://kz16.top/png2base64.html) 把图片转成base64代码, 然后插入base64代码这样既可以插入图片又可以保证安全. 但是会带来新问题, base64代码太长怎么办?
    
-   base64代码太长可用折叠方案, 例如VScode可以用标签`<!-- #region -->`与`<!-- #endregion -->`
    
-   想简单省事, 直接用vscode中的Paste Image插件, 截图之后, Ctrl+Alt+V快速插入图片
    
-   或者用[marktext](https://github.com/marktext/marktext/releases)编辑器就不存在图片代码过长的问题
    

## 2.2. markdown伴侣工具

-   富文本编辑器ckeditor:  [https://kz16.top/ckeditor/](https://kz16.top/ckeditor/) 支持从word中粘贴带格式的文本和表格, 然后导入到markdown中, 一定要试试
    
-   无广告表格: [https://mengshukeji.gitee.io/luckyexceldemo/](https://mengshukeji.gitee.io/luckyexceldemo/) 配合 ckeditor有奇效
    
-   有广告但好用的在线表格: [https://www.tablesgenerator.com/](https://www.tablesgenerator.com/)
    
-   在线图片转base64代码  [https://kz16.top/png2base64.html](https://kz16.top/png2base64.html), 从根源上解决markdown插图问题.
    
-   mdnice:  [https://mdnice.com/](https://mdnice.com/) 可以把公式转化为svg, 因此用来写邮件和公众号很不错, 要注意部分邮件可能不支持svg图片.
    
-   常用latex公式  [https://kz16.top/latex/symbol/](https://kz16.top/latex/symbol/)
    
-   mathpix: 在线也有一个markdown, 它的优势有两个, 一个是可以很方便支持同步编写, 另外一个可以识别数学公式.
    
-   在线表格:  [https://www.tablesgenerator.com/](https://www.tablesgenerator.com/), 虽然有广告, 但是很强大
    
-   思维导图  [https://app.diagrams.net/](https://app.diagrams.net/)
    
-   数学绘图  
    官网网站[https://www.geogebra.org/](https://www.geogebra.org/)  
    中文镜像[https://ggb123.cn/](https://ggb123.cn/)  
    推荐好用[https://geogebra.kz16.top/ggbppt.html](https://geogebra.kz16.top/ggbppt.html)
    
-   矢图编辑  [https://inkscape.org/](https://inkscape.org/)
    

# 3. 那些年用过的markdown

## 3.1. 用的第一款markdown

stackedit官网:  [https://stackedit.io/app#](https://stackedit.io/app#)

stackedit个人经验:  [https://kz16.top/stackedit/](https://kz16.top/stackedit/)

### 3.1.1. 案例

-   一开始选择它最关键的原因是, 它可以很方便与GeoGebra结合, 生成含有可交互动态图的html文件,  [详见视频](https://www.bilibili.com/video/BV1UJ411s7vZ) . 具体内容见  [https://geogebra.kz16.top/](https://geogebra.kz16.top/) 该页面里的不少链接里的内容是用stackedit写好的
    
-   后面发现用它写笔记也不错,  [笔记链接](https://kz16.top/tianyuan2019cdu)
    
-   再后面用它写了一些计算数学相关经验  [https://na.kz16.top/](https://na.kz16.top/), 这个链接里的大部分内容是一天内完成的
    

### 3.1.2. 优点

-   无需安装, 打开浏览器就可用, 很方便做笔记, 特别是网上找资料做笔记, 用它准错不了
    
-   进入界面就是一个很好的教程样例, 无需经验, 打开链接就会写
    
-   强大的同步功能, 用它同步文档到github或gitlab很方便
    
-   导出的html书签模板很不错, 很方便电脑查看
    
-   可以很方便自定义输出模板
    
-   自动保存
    

### 3.1.3. 缺点

-   浏览器中不能很好地和本地建立同步,因此有安全隐患, 清除浏览器记录可能导致所有笔记被删除
    
-   没有代码折叠
    

## 3.2. 用的第二款markdown

VScode:  [https://code.visualstudio.com/](https://code.visualstudio.com/)

直接用的话不太给力, 需要下载一些插件,  [参考这里](https://kz16.top/deepin/#vscode%E5%86%99latex%E4%B8%8Emarkdown)

-   Markdown Preview Enhanced
-   Markdown TOC
-   Excel to Markdown
-   Paste Image

可以用[gethtml.py](https://kz16.top/gethtml.py)把导出的html文件转换成含有左侧目录树的样式, 要注意从eBook格式中导出的html文件会得到链接引用的本地绝对路径, 因此如果链接里有相对路径, 就千万别用eBook格式

### 3.2.1. 优点

-   写公式相当方便, 因为有提示, 并且非常智能, 体验感很强
    
-   速度很快, 没出现过卡顿现象
    
-   支持`[toc]`添加书签, 并且支持给大小标题自动加序号
    
-   同步渲染, 定位精准
    
-   很方便自定义样式, 快捷键Ctrl+Shift+P打开命令面板, 输入`Customize CSS`, 然后打开`style.less`就可以自定义样式, 例如个人设置为
    
```json
    .markdown-preview{
      body {
        margin: 0
      }
      
      article,aside,footer,header,nav,section {
        display: block
      }
      
      h1,h2,h3,h4,h5,h6 {
        margin: .5em 0;
        line-height: 1.5
      }
      
      hr {
        color:#e1e4e8;
        background-color: #e1e4e8;
      }
    
      h1:after,h2:after {
        content: "";
        display: block;
        position: relative;
        top: .13em;
        border-bottom: 1px solid hsla(0,0%,20%,.33)
      }
      
      ol ol,ol ul,ul ol,ul ul,ol li,ul li {
        margin: 1em 0;
        line-height:1.5
      }
    }
```
    
-   轻松与github同步
    

## 3.3. 其它的一些markdown

用得不多, 所以不做过多评价, 但是都在github点了星星, 毕竟开源不容易

-   [marktext](https://github.com/marktext/marktext/releases): 这款软件很不错, 插入片方便, 可以修改图片大小, 据说和typora差不多(typora不开源不曾用过). 导出的html文件样式很方便手机查看
    
-   [Notable](https://github.com/notable/notable/releases): 用它分享文档不错, 直接得到链接
    
-   [joplin](https://github.com/laurent22/joplin)
    
-   [zettrl](https://github.com/Zettlr/Zettlr/releases)
    
-   [boost](https://github.com/BoostIO/Boostnote)
    

## 3.4. 小结

总之, markdown编辑软件千万别只选一个, 不同的需求用不同的软件. 每款软件都有它优秀的地方, 应该充分利用好它们的优势, 当然要注意下不同软件的兼容问题, 不同编辑器语法会略有不同, 但是大体是兼容的.



本文转载来源:  [http://kz16.top/md](http://kz16.top/md)

请支持原作者`kz16`，辛苦制作不易

---

1.  我是尾注菌1 [↩︎](https://kz16.top/md/#fnref1)
    
2.  我是尾注菌2 [↩︎](https://kz16.top/md/#fnref2)