---
title: Yilia主题优化
tags:
  - Themes
  - Blog
toc: true
abbrlink: 25766
date: 2019-06-12 09:19:07
---

![yilia.jpg](https://cdn.anyway1314.cn/imageyilia.jpg)

分享一些博客基础的配置((*^▽^*))<br>参考了一些博客，Ծ‸Ծ一点一点填坑~
<!--more-->

# 一、添加统计(不蒜子&字数统计)
## 1、总体统计
找到`themes\yilia\layout\_partial\after-footer.ejs`,添加：
``` js
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```
找到`themes\yilia\layout\_partial\footer.ejs`，在`<div class="footer-right">`标签内添加：
``` php
<!-- # PV方式，单个用户连续点击 n 篇，记录 n 次记录值 -->
<span id="busuanzi_container_site_pv"> 总访问量: <span id="busuanzi_value_site_pv"></span> /</span>
<!-- # UV方式，单个用户连续点击 n 篇，记录 1 次记录值 -->
<span id="busuanzi_container_site_uv">  访客数:<span id="busuanzi_value_site_uv"></span></span>
```
## 2、文章统计
找到`themes\yilia\layout\_partial\post\nav.ejs`，注释掉以下两行：大概在27行左右(无此代码请忽略)  
``` php
<span class="post-meta-item-text">本文阅读量 </span>
<span class="leancloud-visitors-count">8848</span>
```
注释掉之后直接在这两行下面加上：
``` php
<span id="busuanzi_container_page_pv">
        本文阅读量: <span id="busuanzi_value_page_pv"></span>次
 </span>
```
## 3、字数、阅读时长统计
打开博客根目录、安装插件
``` yml
npm i -save hexo-wordcount
```
博客根目录`_config.yml`添加配置:
``` yml
word_count: true
```
找到`themes\yilia\layout\_partial\article.ejs`,在大概第七行

![20190715180810.png](https://cdn.anyway1314.cn/image20190715180810.png)

下面添加代码:
``` js
<% if(theme.word_count && !post.no_word_count){%>
          <%- partial('post/word') %>
          <% } %>
```
最后在`themes\yilia\layout\_partial\post`目录下新建`word.ejs`,内容如下：
``` js
<div style="margin-top:10px;">
    <span class="post-time">
      <span class="post-meta-item-icon">
        <i class="fa fa-keyboard-o"></i>
        <span class="post-meta-item-text" style="font-size: 16px;color: grey">  字数统计: </span>
        <!--这里样式可以自己定制-->
        <span class="post-count" style="font-size: 16px;color: grey"><%= wordcount(post.content) %>字</span>
      </span>
    </span>
    
    <span class="post-time">
      &nbsp; | &nbsp;
      <span class="post-meta-item-icon">
        <i class="fa fa-hourglass-half"></i>
        <span class="post-meta-item-text" style="font-size: 16px;color: grey">  阅读时长: </span>
        <span class="post-count" style="font-size: 16px;color: grey"><%= min2read(post.content) %>分</span>
      </span>
    </span>
</div>
```
# 二、添加文章目录(两种)
## 1、主题默认方式

![QQ截图20190718120622.png](https://cdn.anyway1314.cn/imageQQ截图20190718120622.png)

<p style="color:red">注意！！！文章Markdown文件一定要从一级标题开始写，直接从二级标题是无法生成目录的！！！</p>  

### 直接在yilia目录下的`_config.yml`配置toc属性即可  

``` yml
   toc: 0    #不开启目录
   toc: 1    #文章.md文件添加"toc:true"属性的才有目录
   toc: 2    #所有文章开启目录
```

## 2、自制滑动白色目录

![QQ截图20190718120545.png](https://cdn.anyway1314.cn/imageQQ截图20190718120545.png)

### 1、修改css文件：
`themes\yilia\source\assets`路径下找到`main.xxxxx.css`，在最后添加代码：   
<p style="color:red">这里的xxxxx是不确定的意思，有些人重新build后会和原版的不一样</p>  

``` css
#container .show-toc-btn,#container .toc-article{display:block}
.toc-article{z-index:100;background:#fff;border:1px solid #ccc;max-width:250px;min-width:150px;max-height:500px;overflow-y:auto;-webkit-box-shadow:5px 5px 2px #ccc;box-shadow:5px 5px 2px #ccc;font-size:12px;padding:10px;position:fixed;right:35px;top:129px}.toc-article .toc-close{font-weight:700;font-size:20px;cursor:pointer;float:right;color:#ccc}.toc-article .toc-close:hover{color:#000}.toc-article .toc{font-size:12px;padding:0;line-height:20px}.toc-article .toc .toc-number{color:#333}.toc-article .toc .toc-text:hover{text-decoration:underline;color:#2a6496}.toc-article li{list-style-type:none}.toc-article .toc-level-1{margin:4px 0}.toc-article .toc-child{}@-moz-keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}@-webkit-keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}@-o-keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}@keyframes cd-bounce-1{0%{opacity:0;-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}60%{opacity:1;-o-transform:scale(1.01);-webkit-transform:scale(1.01);-moz-transform:scale(1.01);-ms-transform:scale(1.01);transform:scale(1.01)}100%{-o-transform:scale(1);-webkit-transform:scale(1);-moz-transform:scale(1);-ms-transform:scale(1);transform:scale(1)}}.show-toc-btn{display:none;z-index:10;width:30px;min-height:14px;overflow:hidden;padding:4px 6px 8px 5px;border:1px solid #ddd;border-right:none;position:fixed;right:40px;text-align:center;background-color:#f9f9f9}.show-toc-btn .btn-bg{margin-top:2px;display:block;width:16px;height:14px;background:url(https://7xtawy.com1.z0.glb.clouddn.com/show.png) no-repeat;-webkit-background-size:100%;-moz-background-size:100%;background-size:100%}.show-toc-btn .btn-text{color:#999;font-size:12px}.show-toc-btn:hover{cursor:pointer}.show-toc-btn:hover .btn-bg{background-position:0 -16px}.show-toc-btn:hover .btn-text{font-size:12px;color:#ea8010}
.toc-article li ol, .toc-article li ul {
    margin-left: 30px;
}
.toc-article ol, .toc-article ul {
    margin: 10px 0;
}
```
### 2、修改ejs文件：
找到`themes\yilia\layout\_partial\article.ejs`,
在 `</header> <% } %>`下面加入:  
``` js
<!-- 目录内容 -->
<% if (!index && post.toc){ %>
    <p class="show-toc-btn" id="show-toc-btn" onclick="showToc();" style="display:none">
          <span class="btn-bg"></span>
          <span class="btn-text">文章导航</span>
          </p>
	<div id="toc-article" class="toc-article">
	    <span id="toc-close" class="toc-close" title="隐藏导航" onclick="showBtn();">×</span>
		<strong class="toc-title">文章目录</strong>
           <%- toc(post.content) %>
         </div>
   <script type="text/javascript">
	function showToc(){
		var toc_article = document.getElementById("toc-article");
		var show_toc_btn = document.getElementById("show-toc-btn");
		toc_article.setAttribute("style","display:block");
		show_toc_btn.setAttribute("style","display:none");
		};
	function showBtn(){
		var toc_article = document.getElementById("toc-article");
		var show_toc_btn = document.getElementById("show-toc-btn");
		toc_article.setAttribute("style","display:none");
		show_toc_btn.setAttribute("style","display:block");
		};
   </script>
      <% } %>		
<!-- 目录内容结束 -->
```
对应每篇文章的md文件，开头加上`toc: true`属性就行
# 三、添加valine评论系统(Gitalk参见另一篇文章：[点击跳转](https://blog.anyway1314.cn/post/2ee2703d.html) )
## 1、注册learncloud账号，创建应用(需要先实名认证账号)

![20190715170626.png](https://cdn.anyway1314.cn/image20190715170626.png)

## 2、应用设置里找到 `App ID` 和 `App Key`  

![20190715171100.png](https://cdn.anyway1314.cn/image20190715171100.png)

## 3、打开yilia主题目录下的`_config.yml`,修改设置  
``` yml
valine: 
  enable: true 
  appid: '' #Leancloud应用的App ID
  appkey: '' #Leancloud应用的App Key 
  #这里的appid和appkey如果配置失败可以试试改成app_id和app_key
  verify: false #验证码
  notify: false #评论回复提醒
  avatar: mm #评论列表头像样式：
  avatar_cdn: '' #头像CDN
  placeholder: '友情提醒，留下正确的邮箱地址可以第一时间获取评论反馈' #评论框占位符
  pageSize: 10 #评论分页
  visitor: true #阅读统计
```

## 4、找到`yilia\layout\_partial\`目录下的`article.ejs`、添加代码:
``` js
<% if (theme.valine && theme.valine.appid && theme.valine.appkey){ %>
    <section id="comments" class="comments">
      <style>
        .comments{margin:30px;padding:10px;background:#fff}
        @media screen and (max-width:800px){.comments{margin:auto;padding:10px;background:#fff}}
      </style>
      <%- partial('post/valine', {
        key: post.slug,
        title: post.title,
        url: config.url+url_for(post.path)
        }) %>
    </section>
<% } %>  
```
## 5、在\_partial\post目录下新建`valine.ejs`,内容如下:
``` js
<div id="vcomment"></div>
<script src="//cdn.jsdelivr.net/npm/jquery/dist/jquery.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/leancloud-storage/dist/av-min.js"></script>
<script src='//cdn.jsdelivr.net/npm/valine/dist/Valine.min.js'></script>
<script>
   var notify = '<%= theme.valine.notify %>' == true ? true : false;
   var verify = '<%= theme.valine.verify %>' == true ? true : false;
   new Valine({
            av: AV,
            el: '#vcomment',
            notify: notify,
            verify: verify,
            app_id: "<%= theme.valine.appid %>",
            app_key: "<%= theme.valine.appkey %>",
            placeholder: "<%= theme.valine.placeholder %>",
            avatar: "<%= theme.valine.avatar %>",
            avatar_cdn: "<%= theme.valine.avatar_cdn %>",
            pageSize: "<%= theme.valine.pageSize %>"
    });
</script>
```
## 6、valine绑定邮箱接收回复通知
参考valine文档连接：[参考链接1](https://deserts.io/diy-a-comment-system/#云引擎一键部署)、[参考链接2](https://github.com/xCss/Valine/wiki/Valine-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F%E4%B8%AD%E7%9A%84%E9%82%AE%E4%BB%B6%E6%8F%90%E9%86%92%E8%AE%BE%E7%BD%AE)

# 四、添加爱心点击效果
## 1、新建js文件：
yilia\source\asset路径下新建`clicklove.js`,内容如下：
``` js
! function (e, t, a) {
    function n() {
        c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"), o(), r()
    }
    function r() {
        for (var e = 0; e < d.length; e++) d[e].alpha <= 0 ? (t.body.removeChild(d[e].el), d.splice(e, 1)) : (d[e].y--, d[e].scale += .004, d[e].alpha -= .013, d[e].el.style.cssText = "left:" + d[e].x + "px;top:" + d[e].y + "px;opacity:" + d[e].alpha + ";transform:scale(" + d[e].scale + "," + d[e].scale + ") rotate(45deg);background:" + d[e].color + ";z-index:99999");
        requestAnimationFrame(r)
    }
    function o() {
        var t = "function" == typeof e.onclick && e.onclick;
        e.onclick = function (e) {
            t && t(), i(e)
        }
    }
    function i(e) {
        var a = t.createElement("div");
        a.className = "heart", d.push({
            el: a,
            x: e.clientX - 5,
            y: e.clientY - 5,
            scale: 1,
            alpha: 1,
            color: s()
        }), t.body.appendChild(a)
    }
    function c(e) {
        var a = t.createElement("style");
        a.type = "text/css";
        try {
            a.appendChild(t.createTextNode(e))
        } catch (t) {
            a.styleSheet.cssText = e
        }
        t.getElementsByTagName("head")[0].appendChild(a)
    }
    function s() {
        return "rgb(" + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + ")"
    }
    var d = [];
    e.requestAnimationFrame = function () {
        return e.requestAnimationFrame || e.webkitRequestAnimationFrame || e.mozRequestAnimationFrame || e.oRequestAnimationFrame || e.msRequestAnimationFrame || function (e) {
            setTimeout(e, 1e3 / 60)
        }
    }(), n()
}(window, document);
```

## 2、修改ejs文件：
找到`themes\yilia\layout\_partial\after-footer.ejs`,添加：
``` js
<script type="text/javascript" src="/assets/clicklove.js"></script>
//注意：这里的路径要对应之前创建clicklove.ejs的地方
```
# 五、调用一言API(刷新自动生成个性签名)
## 修改代码
找到`themes\yilia\layout\_partial\left-col.ejs`文件
(大概12行，theme.subtitle属性内):

![yiyan.png](https://cdn.anyway1314.cn/imageyiyan.png)

把
``` html
<p class="header-subtitle"><%=theme.subtitle%></p>
```
修改为
``` html
<p id="hitokoto">:D 获取中...</p>
<script src="https://v1.hitokoto.cn/?encode=jsselect=%23hitokoto" defer></script>
```
# 六、CSS自定义
## 1、<kbd>F12</kbd> 审查元素,找到自己要修改的内容：

![20190720140107.png](https://cdn.anyway1314.cn/image20190720140107.png)

## 2、修改themes\yilia\source目录下的`main.xxxx.css`  
 <kbd>Crtl</kbd> + <kbd>F</kbd> 搜索自己需要修改的内容,虽然是经过打包的css,还是能看懂的哈(┌(。Д。)┐)  

![QQ截图20190720110450.png](https://cdn.anyway1314.cn/imageQQ截图20190720110450.png)

*<kbd>F12</kbd> 是个好东西(-^▽^-) 
# 七、文章加密
## 1、引入加密插件`encrypt`  
找到博客根目录下的`package.json`,最下面添加：
``` json
"hexo-blog-encrypt": "2.0.*"
```
如图：

![45.png](https://cdn.anyway1314.cn/image45.png)

cmd进入博客根目录，执行：
``` yml
npm install
```
## 2、修改配置
找到根目录下的`_config.yml`文件，添加：
``` yml
# Security
#
encrypt:
    enable: true
```
## 3、加密文章的配置
在需要加密的文章.md文件开头写入：
``` markdown
---
title: 加密文章
date: 2019-05-30 22:02:07
password: 这里填密码
abstract: 这里是博客简述（能被访客看见）
message: 输入密码提示语句（例如：请输入密码）
---
```
# 八、添加RSS
## 1、安装插件：
``` yml
npm install --save hexo-generator-feed
```
## 2、在根目录的_config.yml添加:
``` yml
#rss
  plugins: hexo-generater-feed
```
## 3、修改主题目录下的_config.yml
在subnav:里面添加：
``` yml
  rss: '/atom.xml'
```
# 九、上传README.md文件
## 1、在博客根目录的source文件夹内，新建`README.md`文件
## 2、在博客根目录的`_config.yml`里修改配置：  

![QQ截图201907201318100.png](https://cdn.anyway1314.cn/imageQQ截图201907201318100.png)  
    
//hexo部署页面的时候会默认把source目录下的`.md`文件渲染成`html`,所以需要跳过`README.md`的渲染。 
# 十、SEO优化
## 1、加密文章URL
默认的 `网址/年/月/日/文章名` 格式不便于搜索引擎抓取，需要进行优化  
<p style="color:red">注意：修改之后旧文章的统计数据(浏览量)会重新计数，所以建议在一开始写文章时就做好这一步</p> 

### 1、安装插件
``` yml
npm install hexo-abbrlink --save
```
### 2、修改根目录的_config.yml:
把 `permalink: :year/:month/:day/:title/` 改为 `permalink: post/:abbrlink.html`,之后在下面添加： 

``` yml
abbrlink:
  alg: crc32  # 算法
  rep: hex    # 进制
```
## 2、添加sitemap
*安装两个插件就搞定
``` yml
  npm install hexo-generator-sitemap --save     //默认的
  npm install hexo-generator-baidu-sitemap --save    //百度专属
```
## 3、添加百度统计
### 1、注册、获取统计代码：
[百度统计官网](https://tongji.baidu.com/)<br>

![07.png](https://cdn.anyway1314.cn/image07.png)

### 2、修改主题配置
找到yilia主题目录下的`_config.yml`,最后添加一句：
``` php
baidu_tongji: true
```
### 3、新建ejs、修改`head.ejs`
`themes\yilia\layout`目录下新建`baidu_tongji.ejs`,内容如下:
``` js
<% if (theme.baidu_tongji) { %>
   //这里添上上面获取的代码
<% } %>
```
找到`themes\yilia\layout\_partial\head.ejs`,在`</head>`上面添加：
``` js
<%- partial("baidu_tongji") %>
```
### 4、hexo d -g  (重新部署)
### 5、检查代码是否安装成功:[点此查看官方教程](https://tongji.baidu.com/web/help/article?id=93&type=0)

