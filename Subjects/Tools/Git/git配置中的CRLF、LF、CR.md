# git配置中的CRLF、LF、CR


---
title: git配置中的CRLF、LF、CR
authors: Ethan Lin
year:
tags:
  - 日期/2023-06-29 
  - 类型/笔记 
  - 来源/转载 
  - 内容/Git 
---







# 来源

> [git配置中的CRLF、LF、CR - 简书](https://www.jianshu.com/p/3e7b11606721)



基本
CRLF: Carriage-Return Line-Feed的缩写，意思是回车换行，即`\r\n`;
LF: Line-Feed的缩写,意思是换行，即`\n`;
CR: Carriage-Return的缩写，回车，即`\r`;
进阶
当我们敲击回车键(Enter)时，操作系统会插入不可见的字符表示换行，不同的操作系统插入不同

Windows: 插入`\r\n`,回车换行；
Linux\Unix: 插入`\n`,换行；
MacOS: 插入`\r`，回车；
Git
1. AutoCRLF
提交时转换为LF，检出时转换为CRLF
`git config --global core.autocrlf true`
提交时转换为LF，检出时不转换
`git config --global core.autocrlf input`
提交检出均不转换
`git config --global core.autocrlf false`
2.SafeCRLF
拒绝提交包含混合换行符的文件
`git config --global core.safecrlf true`
允许提交包含混合换行符的文件
`git config --global core.safecrlf false`
提交包含混合换行符的文件时给出警告
`git config --global core.safecrlf warn`

> 作者：1df4818f1030
> 链接：https://www.jianshu.com/p/3e7b11606721
> 来源：简书
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。