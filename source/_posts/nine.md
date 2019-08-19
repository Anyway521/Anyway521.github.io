---
title: 从Valine到Gitalk
tags:
  - Valine
  - Gitalk
toc: true
abbrlink: 2ee2703d
date: 2019-07-18 18:35:26
---

![togitalk.png](https://cdn.anyway1314.cn/imagetogitalk.png)

Valine用了没几天，感觉还是不习惯￣へ￣  
果断换回我的Gitalk(/≧▽≦)/
<!--more-->

# Github注册OAuth application
## 1、[点击这里注册](https://github.com/settings/applications/new)
## 2、填写信息

![QQ截图20190718191625.png](https://cdn.anyway1314.cn/imageQQ截图20190718191625.png)

## 3、注册成功后得到两个ID、备用

![20190718185223.png](https://cdn.anyway1314.cn/image20190718185223.png)

# Github新建仓库(存储评论)

![20190718185557.png](https://cdn.anyway1314.cn/image20190718185557.png)

# 修改本地配置
## 1、找到layout\\_partial\article.ejs，添加代码：
``` js
  <% if(theme.gitalk.enable){ %>
    <%- partial('post/gitalk', {
      key: post.slug,
      title: post.title,
      url: config.url+url_for(post.path)
    }) %>
  <% } %>
```
## 2、在`layout\_partial\post`目录下新建`gitalk.ejs`
``` js
  <div id="gitalk-container" style="padding: 0px 30px 0px 30px;"></div> 

  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
  <script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>
  <script type="text/javascript">

  if(<%=theme.gitalk.enable%>){
    var gitalk = new Gitalk({
      clientID: '<%=theme.gitalk.clientID%>',
      clientSecret: '<%=theme.gitalk.clientSecret%>',
      repo: '<%=theme.gitalk.repo%>',
      owner: '<%=theme.gitalk.owner%>',
      admin: ['<%=theme.gitalk.admin%>'],
      id: '<%= page.date %>',
      distractionFreeMode: '<%=theme.gitalk.distractionFreeMode%>'
  })
  gitalk.render('gitalk-container') 
  }
  </script>
```
## 3、修改`yilia\source-src\css\`目录下的`comments.scss`
*在第一行增加 `#gitalk-container`，修改后：
``` css
  #disqus_thread, .duoshuo, .cloud-tie-wrapper, #SOHUCS, #gitment-ctn, #gitalk-container{
    padding: 0 30px !important;
    min-height: 20px;
  }

  #SOHUCS {
    #SOHU_MAIN .module-cmt-list .block-cont-gw {
      border-bottom: 1px dashed #c8c8c8 !important;
    }
  }
```
# 配置主题的`_config.yml`
## 注释掉valine的代码，新增gitalk的配置：
``` yml
  #7、配置gitalk
  gitalk: 
    enable:  true #用来做启用判断可以不用
    owner:  #github用户名
    repo:  '' # 存储博客评论的仓库地址，可以是存储博客的仓库
    clientID:  '' #ClientID
    clientSecret:  '' #ClientSecret
    admin:  #github用户名
    distractionFreeMode:  true
```

## 重新部署，记得初始化一下哦(/≧▽≦)/