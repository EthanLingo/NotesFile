---
title: 国内npm镜像源推荐及使用
authors: Ethan Lin
year:
tags:
  - 内容/NodeJS 
  - 类型/解决 
---


# 国内npm镜像源推荐及使用





NPM（Node Package Manager），是NodeJs的模块依赖管理工具。由于Npm源在国外，使用起来不方便，

故需要国内可靠的npm源可以使用，现整理如下：

一、国内镜像

1、淘宝NPM镜像

搜索地址：http://npm.taobao.org
registry地址：http://registry.npm.taobao.org

2、cnpmjs镜像

搜索地址：http://cnpmjs.org
registry地址：http://r.cnpmjs.org

二、使用方法

1、临时使用

```
npm --registry https://registry.npm.taobao.org install express
```

2、持久使用



```
npm config set registry https://registry.npm.taobao.org

#配置后可通过下面方式来验证是否成功
npm config get registry

# 或者
npm info express
```

或者

```
#编辑 ~/.npmrc 加入下面内容

registry = http://registry.npm.taobao.org/
```

3、通过cnpm使用

```
npm install -g cnpm --registry=https://registry.npm.taobao.org

// 使用
cnpm install expresstall express
```