---
title:
  - 自动部署 SSL 证书
authors: BingZhen Zhou
year: 2024-03-24
tags:
  - 类型/笔记
  - 日期/2024-03-24
  - 内容/管理网站
---
# 自动部署 SSL 证书


## 第一次部署的步骤


#### 1. 登录网站所在的服务器
#### 2. 安装和启动 nginx：
1. 更新资源 `sudo apt-get update`；
2. 安装 nginx `sudo apt install nginx`
3. 重启 `service nginx restart`
不出意外，就可以启动服务。如果成功，则可以开始下一步，安装证书。
#### 3. 安装证书：
1. 安装 certbot

``` shell
sudo apt update
sudo apt install certbot python3-certbot-nginx -y 
```

2. 生成证书
		

`certbot --nginx`

3. 输入`certbot --nginx` → 输入自己申请的邮箱 → 选择 "A" → 选择 "Y" → 选择要生成的域名，如果是多个域名的话，用分号或者空格分割；然后是选择是否重定向 https , 选 "2" 的话就是重定向 https 。这样就生成了 SSL 证书了。SSL证书具体位置： `/ect/letsencrypt/live` 下。
3. 别忘记重启 nginx 服务让它生效 `service nginx restart`；

## 继续部署的步骤



上述的证书有效期是 3 个月。临期时，需要重新申请与部署证书。



有两种方法部署。一种是手动部署。另一种是自动部署。

### 手动部署方法



1. 输入 `certbot renew --force-renew` 。最好是等到两个月之后 输入这一行。

### 自动部署方法



把 https 的申请加入到定时服务中。方法是 `crontab -e` 

第一次需要选择编辑器, 建议选 "2" , 用 vim 作为编辑器, 然后按 "i" 开启写入模式, 粘贴下面代码可确保每月1号3时申请新证书 

```shell
0 3 1 * * certbot renew --force-renew
```



键入 <kbd>Esc</kbd> 退出写入模式, <kbd>shift</kbd> + <kbd>z</kbd> + <kbd>z</kbd>保存退出。如果编辑器选择错误。可以 `sudo select-editor` 重选 。

查看是自启动命令否修改成功 `crontab -l`；

重启 crontab 服务 `sudo service cron restart`；

