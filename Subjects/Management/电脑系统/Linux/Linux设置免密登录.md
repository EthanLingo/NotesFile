# Linux设置免密登录

tags: #内容/办公 #内容/Linux/操作 

Linux系统远程端与其它终端设备之间，通过生成密钥对方式实现免密登录。
操作如下：

1. 本地终端输入指令：
	指令：`ssh-keygen -t rsa -C '《你的备注》'  -f  ~/.ssh/id_rsa_x
	注解：`-t rsa`表示密钥对类型；`-C '《你的备注》'`表示备注；` -f  ~/.ssh/id_rsa_x`表示生成密钥对之名称与所在路径；
2. 部署公钥至远程端：
   指令 `ssh-copy-id -i ~/.ssh/id_rsa.pub <your user name>@10.10.10.100`
	下次直接输入`ssh <your user name>@10.10.10.100`可以不用密码。

注意，如果配置多对密钥，可以本地终端输入`ssh-keygen`，首次回车之后输入`id_rsa_<你自己填的名字>.pub`，然后剩余一路回车即可。
`

