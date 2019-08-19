---
title: 教你不让别人偷看你的源代码
abbrlink: 5c1e78e2
date: 2019-08-07 17:00:15
tags: 
  - 笔记
  - JavaScript
reward: true
declare: true
---

![qC6S.jpg](https://cdn.anyway1314.cn/imageqC6S.jpg)

一段不让别人查看你页面内容的代码, ╮(╯▽╰)╭ 然鹅...<!-- more -->
其实对老鸟来说，形同虚设 ╮(╯_╰)╭ 
``` js
document.onkeydown=function(){
    var e = window.event||arguments[0];
    if(e.keyCode==123){
    	alert('还在按F12?╭(╯^╰)╮');
            return false;
    }else if((e.ctrlKey)&&(e.shiftKey)&&(e.keyCode==73)){
    	alert('Crtl+Shift+I 有用？(￣ε(#￣)');
            return false;
    }else if((e.ctrlKey)&&(e.shiftKey)&&(e.keyCode==74)){
    	alert('Crtl+Shift+J 有用咩??o(*￣︶￣*)o');
            return false;
    }else if((e.ctrlKey)&&(e.keyCode==83)){
            alert('Crtl+S保存？╰╮(￣▽￣///)！');
            return false;
    }else if((e.ctrlKey)&&(e.keyCode==85)){
           alert('Crtl+U ?(╯‵□′)╯才不给你看源代码');
           return false;
    }
}
document.oncontextmenu=function(){
	alert('鼠标右键也不好使呦罒ω罒');
    return false;
}
```
实际效果参考：[可以去这个页面试一试](https://anyway1314.cn/ZONE/point)  