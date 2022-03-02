#来源/转载

#类型/教程



[[部署环境]]
[[MATLAB]]



[TOC]



# 安装与卸载 Matlab 教程系列









## MacOS







## Windows







## Linux

一、环境

系统：Linux Deepin 20beta

安装软件： Matlab R2019b for Linux

安装包下载：


适用性：该安装方法使用任何Linux系统

二、安装过程

（一）解压挂载执行

1. 解压

方法一：Deepin系统鼠标右键就有解压的快捷键，解压到当前文件夹下
方法二：想通过命令行解压的执行以下步骤：
通过cd命令进入到你下载的压缩包的文件夹，比如我下载在Downloads文件夹

cd ~ Downloads
tar -xvf Matlab R2019b Linux64 Crack.tar.gz 
1
2


2. 挂载安装包

2.1 在/mnt下创建一个iso文件夹来挂载，执行

cd /mnt
sudo mkdir iso
1
2
2.2 修改/mnt/iso 权限，为挂载做准备

cd /
chmod 755 mnt
1
2
2.3 进入到R2019b_Linux.iso文件所在文件夹执行挂载

cd ～/Downloads/MATLAB R2019b linux
sudo mount -t auto -o loop R2019b_Linux.iso /mnt/iso
1
2
2.3 root模式下执行安装，因为后面安装过程需要创建文件夹

cd ～
sudo  /mnt/iso/install
1
2
（二）安装选择过程

如果你是有Mathworks账户的，参考/mnt/iso下的install_guide.pdfhe和install_guide_zh_CN.pdf安装过程去 执行
本人没有账户，以下是我执行的步骤。

选择使用文件安装密钥


选择如果所示，输入：09806-07443-53955-64350-21751-41297


默认执行


如果需求不大，这里可以勾选仅仅要的工具，但是全部安装大概26个G，安装过程一个小时左右。


关于MATLAB工具箱的介绍，参考
[[MATLAB工具箱大全]]

关于我选配的常用工具箱，参考
[[我选配的MATLAB常用工具箱]]


开始安装


等待完成后就点击完成即可，开始下面的操作。

（三）添加文件许可证

进入matlab启动目录cd /usr/local/Polyspace/R2019b下创建存放文件许可证license_server.lic的文件夹哎licenses
cd /usr/local/Polyspace/R2019b
sudo mkdir licenses
1
2
又通过cd命令，进入到解压缩的文件下，我解压的安装包在Downloads下
cd ~/Downloads/MATLAB R2019b linux/Matlab R2019b Linux64 Crack/
1
把压缩包里的文件许可证license_server.lic放复制到matlab的启动目录/usr/local/Polyspace/R2019b/licenses下
sudo cp license_standalone.lic /usr/local/Polyspace/R2019b/licenses
1
又回到matlab的启动目录，修改文件许可证license_standalone.lic的读写权限
cd /usr/local/Polyspace/R2019b/licenses
chmod 755 license_standalone.lic
1
2
用Crack包R2019b下的.so文件替换安装目录R2019b下的.so文件。把在Downloads/Matlab R2019b Linux64 Crack//R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl下的文件复制替换到/usr/local/Polyspace/R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl下。

-f表示强制复制，替换文件
sudo cp -f Downloads/Matlab R2019b Linux64 Crack/Polyspace/R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl/libmwlmgrimpl.so /usr/local/Polyspace/R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl

1
2
通过软链接，在目录cd /usr/local/bin下创建快捷方式，就可以在该目录下打开软件了
cd /usr/local/bin
ln -s /usr/local/Polyspace/R2019b/bin/matlab matlab
1
2
启动matlab
cd /usr/local/bin
./matlab
1
2
如果成功Active，直接会开启matlab，如果没有成功，就会显示如下界面，选择浏文件许可证，在目录/usr/local/Polyspace/R2019b/licenses下的license_standalone.lic。还有一种情况是License checkout failed.License Manager Error -8。则问题出自以上第5步，没有成功替换libmwlmgrimpl.so文件。尝试删除安装目录下的此文件，再复制一次，并一定查看是否复制成功。


点击完成即可，重启一遍。以后打开软件都是执行以下命令
cd /usr/local/bin
./matlab
1
2
（四）收拾残局

取消挂载

sudo umount /mnt/iso
cd /mnt
sudo rmdir iso
1
2
3
三、bug总结

安装过程难免会遇到权限不够的问题，那就使用root模式执行命令，给予文件最高权限
sudo 你的命令
1
但是难免会遇到在读取文件的时候又是权限太高，很可能是无法读取许可证文件。把文件权限修改一下就可以.
chmod 755 文件名
1
如果那些步骤安装错了，卸载掉，但是挂载不用取消，直接重装就行，执行以下步骤
sudo rm -rf /usr/local/Polyspace
cd ～
sudo /mnt/iso/install
1
2
3
启动MATLAB失败：License checkout failed:Make sure the HostID of the license file matches this machie
解决办法：
没有成功替换.so文件。用Crack包R2019b下的.so文件替换安装目录R2019b下的.so文件。把在Downloads/Matlab R2019b Linux64 Crack//R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl下的文件复制替换到/usr/local/Polyspace/R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl下。可以先删除安装目录下的.so文件，再复制过去，确保.so文件复制到位。


-f表示强制复制，替换文件

sudo cp -f Downloads/Matlab R2019b Linux64 Crack/Polyspace/R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl/libmwlmgrimpl.so /usr/local/Polyspace/R2019b/bin/glnxa64/matlab_startup_plugins/lmgrimpl

1
2
四、卸载

1 软件版本

Ubuntu 16.04.6

MATLAB 2016b

查看Ubuntu版本号

name@ubuntu:~$ cat /etc/issue
2 卸载MATAB

2.1 查看MATLAB安装路径

name@ubuntu:~$ whereis matlab
matlab: /usr/lib/matlab /etc/matlab /usr/share/matlab
2.2 卸载MATLAB

方法1

MATLAB文件安装在/usr/local/MATLAB/R2014a路径下

name@ubuntu:~$ sudo rm -rf /usr/local/MATLAB/R2014a

删除各路径下的matlab文件

name@ubuntu:~$ sudo rm -r /usr/lib/matlab /etc/matlab /usr/share/matlab
方法2 

name@ubuntu:~$ sudo apt-get remove --purge matlab
2.3 清理配置残留

n@ubuntu:~$ sudo apt-get autoremove
n@ubuntu:~$ sudo apt-get clean

------------------------------------------------
版权声明：本文为CSDN博主「sdaubaby」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/sdaubaby/article/details/90678486