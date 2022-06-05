[[Python虚拟环境]]
#类型/资料
#来源/转载

**一.创建virtualenv虚拟环境**

如果出现没有找到virtualenv命令的情况，则参考[如何解决找不到virtualenv命令的情况？](#appendix01)

mkvirtualenv -p 版本号 虚拟名

```
virtualenv -p python3 env_1
```

激活环境：创建完虚拟环境之后，进入该虚拟环境，选择activate：
```
cd env_1
source ./bin/activate
```

　　python3:版本号  
　　env\_1: 虚拟环境名称

![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111225899-582222608.png)

**创建成功过后，会默认进入该虚拟环境**

**2.查看该虚拟环境下，安装了哪些Python包**  
　　

在进入该虚拟环境之后，查看该虚拟环境下安装来哪些包

1

`pip` `list`

![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111326809-76132171.png)

**3.在该虚拟环境下，安装Python包**

1

`pip insatll xxxx`

如：

![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111450299-1430448670.png)

**4.退出虚拟环境**


当前在虚拟环境下，准备退出

1

`deactivate`

![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111532944-1192601711.png)

**5.查看当下，共存在多少个虚拟环境**  


1

`workon``+``空格``+``按两次Tab键`

![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111615087-1441783041.png)

**6.进入虚拟环境**  


1



`workon 虚拟环境名`

**![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111655009-239138298.png)**

**7.删除虚拟环境**

1.确保当下没有在使用该虚拟环境，若有，执行:deactivate退出  
2.执行：

1

`rmvirtualenv 虚拟环境名` 

![](https://img2018.cnblogs.com/blog/1251758/201902/1251758-20190227111744744-1604209614.png)



<span id="appendix01"></span>

## 解决找不到virtualenv的情况的解决方法：

在pip install virtualenv 安装virtualenv后

直接用 virtualenv env 命令 来创建虚拟环境（env为虚拟环境的目录名）会提醒bash: virtualenv:command not found

这是因为/usr/bin/中还没有创建软连接。

在不创建软连接的前提下，可以直接去通过执行原可执行文件创建虚拟环境。命令如下：

/usr/local/python3/bin/virtualenv env

--/usr/local/python3/bin/virtualenv 为virtualenv的安装位置
在/usr/bin/中创建软连接之后，就可以直接使用 virtualenv env 命令 来创建虚拟环境了。

 

1） 首先找到virtualenv的安装路径

find / -name virtualenv
2） 文件地址

/usr/local/python3/bin/virtualenv
3） 创建软连接

ln -s /usr/local/python3/bin/virtualenv /usr/bin/virtualenv
接下来就可以直接使用virtualenv命令了
————————————————
版权声明：本文为CSDN博主「酒精灯_」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_41753664/article/details/94494567