---
title: Yilia主题自定义左侧背景图片
abbrlink: c5c4ef21
date: 2019-07-30 14:46:58
tags: Themes
toc: false
reward: true
declare: true
---

![134522_爱奇艺.jpg](https://cdn.anyway1314.cn/image134522_爱奇艺.jpg)

左侧默认的背景是纯色的，这里给出一种方法更改为图片背景。
<!-- more -->

## 修改主题配置
### 1、找到`themes\yilia\`目录下的`_config.yml`,修改配置：
`header` 这一项修改为 `#00000`

![20190730150445.png](https://cdn.anyway1314.cn/image20190730150445.png)

### 2、把你选好的背景图片放到`themes\yilia\source`目录下

![20190730151232.png](https://cdn.anyway1314.cn/image20190730151232.png)

### 3、打开`yilia\source`目录下的`main.xxxx.css`,进行修改
<p style="color:red">这里的xxxx是不确定的意思，有些人重新build后会和原版的不一样</p>  

### <kbd>Crtl</kbd> + <kbd>F</kbd>搜索`.left-col{`、`.left-col .overlay{`以及`#mobile-nav .overlay`

![20190730152116.png](https://cdn.anyway1314.cn/image20190730152116.png)

![20190730152431.png](https://cdn.anyway1314.cn/image20190730152431.png)

![20190730152804.png](https://cdn.anyway1314.cn/image20190730152804.png)

分别在括号里面加上属性： 

``` js
    background-image:url("图片文件名");
```
<p style="color:red">如果你的图片存储在网络上，可以不进行第2步，第3步添加的代码改成:</p>  

``` js
    background-image:url("图片地址");
```

重新部署就行啦。






