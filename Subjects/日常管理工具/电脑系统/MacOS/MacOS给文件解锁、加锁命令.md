#用途/解决


[[MacOS常用命令]]

# MacOS给文件解锁、加锁命令

锁定文件： chflags uchg front_door.jpeg
解锁文件： chflags nouchg front_door.jpeg
如果还需要另一种方法，则可以使用SetFile，它可以让您更改文件的属性：
锁定文件：（SetFile -a L front_door.jpeg大写L）
解锁文件：（SetFile -a l front_door.jpeg小写l）

--- 

>版权声明：本文为CSDN博主「MAC知识技巧分享」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_48140874/article/details/113057613