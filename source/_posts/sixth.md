---
title: 博客项目托管到Coding
tags:
  - Blog
  - Coding
  - Github
toc: true
abbrlink: 59308
date: 2019-07-02 10:55:22
---
![coding.jpg](https://cdn.anyway1314.cn/imagecoding.jpg)

考虑到github国内访问速度，以及偶尔"404"的尴尬情况，把博客项目<br>也部署到Coding。
<!--more-->

# 注册Coding账号、完善信息
## 1、[Coding官网点这里](https://coding.net/)<br>
## 2、个人方式注册后，完善下个人信息(邮箱、密码之类的)。
# 配置SSH公钥
## 1、找到本地的`User/xxx/.ssh`目录
![446.png](https://cdn.anyway1314.cn/image446.png)
## 2、Notepad++打开`id_rsa.pub`文件，复制公钥
## 3、Coding里打开`个人设置`->`SSH设置`、添加SSH

![gf.png](https://cdn.anyway1314.cn/imagegf.png)

## 4、测试是否添加成功
Win+R cmd输入
``` SSH
ssh -T -p 443 git@git-ssh.coding.net
```
见到如下提示则为成功(ps:443是https端口)

![test.png](https://cdn.anyway1314.cn/imagetest.png)

# 在Coding上新建项目
## 1、项目名填自己的用户名、最后一栏选上`用README.md文件初始化项目组`

![nr.png](https://cdn.anyway1314.cn/imagenr.png)

*这是基本的项目初始化工作。

## 2、选择`Pages服务`，以`master分支`进行部署。

![21.png](https://cdn.anyway1314.cn/image21.png)

## 3、配置博客根目录的`_config.yml`
在 `repository` 里添加: `coding: git@git.coding.net:coding用户名/coding用户名.git`
以下是我的配置：

``` yml
deploy:
  type: git
  repository: 
      github: git@github.com:Anyway521/anyway521.github.io.git
      coding: git@git.coding.net:Des_tiny/Des_tiny.git
  branch: master
```  

## 4、在博客根目录的`source`文件夹下新建文档，命名为`Staticfile`(无文件扩展名)

![44.png](https://cdn.anyway1314.cn/image44.png)

# 添加解析、Coding配置域名
## 1、在域名控制台添加解析：
Github pages设置为`境外`、Coding Pages设置为`默认`

![jx.png](https://cdn.anyway1314.cn/imagejx.png)

## 2、进入Coding、找到`Pages服务`
//ps:"设置"的图标在右上角  
绑定域名

![pp.png](https://cdn.anyway1314.cn/imagepp.png)

# 重新部署博客


