# Python下载已经有的安装包



1、将pip安装的包导出导文件列表

`pip freeze > requirements.txt`
2、pip批量安装包及通过列表文件安装

`pip install -r requirements.txt`
3、下载pip包-通过列表文件批量下载pip包

单个包：栗子

`pip download numpy`
批量：

`pip download -r requirements.txt`  
默认保存到当前目录，也可指定目录 : 用  -d  指定

`pip3 download -r requirements.txt -d /tmp/packages/`
————————————————
版权声明：本文为CSDN博主「Davide~苏」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/GodDavide/article/details/94894770

