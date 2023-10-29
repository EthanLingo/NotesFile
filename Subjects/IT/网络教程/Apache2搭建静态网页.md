# apache2搭建静态网页


---
title: apache2搭建静态网页
authors: Ethan Lin
year:
tags:
  - 来源/转载 
  - 内容/网站 
---



## 安装apache2

- 安装 `sudo apt install apache2`
- 重启`service apache2 restart`
- 停止`service apache2 stop`
- 部署网页内容: 只需修改`/var/www/html`里的文件

## 配置域名
- 开启80端口
- 在aliyun域名相关的页面中把ip地址与域名对接下
- 配置文件为`/etc/apache2/apache2.conf`, 配置信息为
	 ```text
	<VirtualHost *:80>
	  ServerName kz16.top
	  DocumentRoot "/var/www/html/"
	  <Directory "/var/www/html/">
	    AllowOverride all
	    Order allow,deny
	    Allow from all
	  </Directory>
	</VirtualHost>

	<VirtualHost *:80>
	  ServerName na.kz16.top
	  DocumentRoot "/var/www/html/na"
	  <Directory "/var/www/html/na">
	    AllowOverride all
	    Order allow,deny
	    Allow from all
	  </Directory>
	</VirtualHost>
	```


## 配置https

1. 开启443端口
2. 先购买免费的ssl证书, 并下载解压, 上传到`/etc/apache2`中
3. 修改`/etc/apache2/sites-available`中的配置文件, 主要是配置文件的路径, 例如
	```xml
	<VirtualHost _default_:443>
		ServerName na.kz16.top
		DocumentRoot /var/www/html/na
		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined
		SSLEngine on
		SSLCertificateFile	/etc/apache2/ssl_na/6444675_na.kz16.top_public.crt
		SSLCertificateKeyFile /etc/apache2/ssl_na/6444675_na.kz16.top.key
		SSLCertificateChainFile /etc/apache2/ssl_na/6444675_na.kz16.top_chain.crt
		<FilesMatch "\.(cgi|shtml|phtml|php)$">
				SSLOptions +StdEnvVars
		</FilesMatch>
		<Directory /usr/lib/cgi-bin>
				SSLOptions +StdEnvVars
		</Directory>
	</VirtualHost>
	```
4. 最后重启`service apache2 restart`

整个配置不会有任何难度


## 自动跳转为https或http

http 跳转为 https, 页面代码为
```html
<script type="text/javascript">
var loc = location.href.split(':');
if(loc[0]=='http'){
	location.href='https:'+loc[1];
}
</script>
```

https 跳转为 http, 页面代码为
```html
<script type="text/javascript">
var loc = location.href.split(':');
if(loc[0]=='https'){
	location.href='http:'+loc[1];
}
</script>
```


> 来源：[课中引路网](https://kz16.top)