---
title: Hexo博客添加自定义HTML页面
abbrlink: e9072c01
date: 2019-08-05 22:06:24
tags: 
  - Hexo
  - 笔记
reward: true
declare: true
---

![6b1htm0.jpg](https://cdn.anyway1314.cn/image6b1htm0.jpg-title)

改 “友链” 为 “ZONE” ,增加了一些以前收藏的特效页面。  
顺便说说怎么往博客添加自定义的HTML文件。
<!-- more -->

## 首先，在博客根目录的`source`文件夹下，新建文件夹用于存放HTML文件 

![20190805222613.png](https://cdn.anyway1314.cn/image20190805222613.png)

这里我建了个`ZONE`文件夹，然后里面的子文件夹存放各个HTML文件，当然你也可以只创建一个主文件夹，直接在里面放文件也行。

## 第二步，在博客根目录的配置文件`_config.yml`文件里，跳过渲染

![20190805223219.png](https://cdn.anyway1314.cn/image20190805223219.png)

注意格式：这里如果你是只创建了一个文件夹，要跳过它目录下所有文件的渲染，就写：
``` yml
# 跳过文件夹下所有文件
skip_render: 
  - "文件夹名/*"  
```
如果像我那样，文件夹下还有子文件夹，那就这样写：  
``` yml
# 跳过子文件夹
skip_render: 
  - "文件夹名/子文件夹名/*"
```
或者更简单直接的方式
``` yml
# 跳过文件夹下所有子文件夹和文件
skip_render: 
  - "文件夹名/**"   
```
![QQ截图20190807141009.png](https://cdn.anyway1314.cn/imageQQ截图20190807141009.png)

## 最后，处理css、js文件
我们都知道，hexo部署的是静态文件，所有文章的md文件会被渲染成html文件(hexo g生成)，  
hexo会帮我们把所有css、js文件都加到文章里，我们之前跳过了渲染(第二步)，所以就需要手动  
<u>把css、js整合到html文件里</u>  一般我们的代码就是这种结构:

![20190805225310.png](https://cdn.anyway1314.cn/image20190805225310.png)

下面分两部分：
### css
找到`index.html`文件里的语句,形如：
``` html
    <link rel="stylesheet" href="css/xxx.css">   
    <!-- css目录下的xxx.css文件 -->
```
直接在css文件夹里面找到对应的文件`xxx.css`，复制文件内容，把上面的代码改为：
``` html
    <style> css代码内容 </style>
```
### js
找到`index.html`文件里的语句，形如：
``` html
    <script src="js/xxx.js"></script>
```
直接在js文件夹里面找到对应的文件`xxx.js`，复制文件内容，把上面的代码改为：
``` HTML
    <script> js代码内容 </script>
```
重新部署即可。