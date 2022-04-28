# Linux安装ssh服务并设置开机自启动


#来源/转载
#解决 
#教程 


[[ssh]]
[[部署]]
[[Linux部署环境]]
[[远程]]


# Linux安装ssh服务并设置开机自启动

安装ssh服务
sudo apt-get install openssh-server
启动ssh服务
sudo /etc/init.d/ssh start
设置开机自启动
sudo systemctl enable ssh
关闭ssh开机自动启动命令
sudo systemctl disable ssh
单次开启ssh
sudo systemctl start ssh
单次关闭ssh
sudo systemctl stop ssh
设置好后重启
reboot
————————————————
版权声明：本文为CSDN博主「淦123」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_40700617/article/details/90780009