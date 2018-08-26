---
layout: post
title: 第一篇博客，小鸡冻
categories:
- blog
tags:
- web
- Jekyll
- GitHub Pages
---

## 既然是第一篇博客，那就讲讲是怎么搭建的吧
### Ⅰ 总
我想明眼人更确切地说coders看到这个域名直接就能知道：这是一个GitHub page静态页面，也就是说没有数据库接口等额外的配置，总体上是<strong>很容易</strong>配置的，加上博主是个拿来主义者 ——主题模板什么的从不动手写（逃，希望看到这篇文章的人不会被我唠唠叨叨的”裹脚布“吓到。

作为一个技术水平有限的coder我在这个博客搭建过程中遇到过<strong>几个坑</strong>，这也是我写这篇文章的原因之一，如果对gayhub（雾，GitHub）有一点点基础并且jekll或相关环境本身不会有大变动的话相信大家都能成功搭一个自己的<strong>纯净</strong>的静态博客。

如果对GitHub的<strong>git基本操作</strong>不够熟悉的话，建议聪明的你花10-30分钟看下[基础教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)，这里我分享的廖雪峰的。

今天才知道认认真真写个文档不容易（也是第一次用🐎👇markdown语言），不知道会不会有人看，反正写完我肯定能记住了(烂笔头赛高)，如果小可爱们要<strong>转载请注明原作者（就是本仙女(‾◡◝)/~和原文链接哦</strong>。

### Ⅱ 安装环境

ruby和liquid是这个博客构成的主要语言，但是我们不用一步步深入学习，但可以简单了解下[liquid的官方文档](https://liquid.bootcss.com/)，这种模板语言让我想起了python的django模板语言，还是很简单易懂的。

哦对，这部分我们讲搭建环境。很多博客讲搭GitHub Pages的时候总是将建立远程仓库放在最前面说，但是我觉得吧还是要先把本地的东西安排地明明白白再推送远程更适合我，也不能排除可能一些大佬下了模板就直接放到GitHub上远程调试。

首先我们安装[ruby](http://www.ruby-lang.org/zh_cn/downloads/)，本次我们以Win10系统为例（其他系统大佬：你这不清真啊，，，太菜了没办法）。Win系统的话基本就是一路next就行了。像python语言的pip，ruby安装的命令是gem，所以我们：

```powershell
gem install jekyll
```
后面可能会有环境依赖问题，直接`gem install`他报错中所显示缺失的包即可。

### Ⅲ 下载主题

我的主题是[Naringu](https://github.com/ariestiyansyah/naringu)，我们可以直接git clone这个链接，或者参考这个链接的[jekyll模板](http://jekyllthemes.org/)下载其他样式的到本地即可。

### Ⅴ 测试配置

#### ① 必经步骤

我们用powershell，`cd` 进入相应目录，然后：

```powershell
jekyll serve
```

我们就可以在浏览器打开[http://127.0.0.1:4000](http://127.0.0.1:4000)这个默认的链接来查看我们代码画出来的真实效果啦。

> 注意：
>
> * 在命令行端可能会有报错，一般都是404，这就是我曾掉进去过的坑。一般出现 not found 的 error 都是因为liquid模板语言的目录部分没配置好，可能是这个模板作者或jekyll、liquid升级等的锅。此外感谢@[不系舟](https://www.zmonster.me/)大佬的指点（在我“不懈”的追问下），直接帮我找到有问题的文件。
> * 后面远程推送完成打开我们带github.io域名的网站时，如果想用浏览器确切查看我们每次commit前后网页的变化的话，我用火狐和Chrome测试后发现这两种都需要在刷新页面前清除缓存。
> * 博客的本地路径最好不要出现中文否则可能会有GBK与utf-8编码不兼容的报错。

所以我们下一步要修改如下文件：

* `_includes/head.html`中的所有"{{site.baseurl}}"更改为”/“表示根目录

#### ② 自定义

存储图片几种方式：

* 七牛云存储
* 找个能上传文件的网站(没让你日站)最好支持https
* 本地增加assets目录或直接在naringu自带的public目录存储

更改我们的favicon：

* /pubulic/favicon.ico文件是我们的HTML文件中的标签页的icon，换成自己设计的或喜欢的icon文件即可。

### Ⅳ 仓库操作

首先我们需要在GitHub新建一个仓库（repo），命名方式为：你的用户名.github.io。

然后我们在本地git push过去就吼啦，就可以打开我们的GitHub分配给我们的链接了。

GitHub学生包可以实现私有仓库，不知道我还能苟几年。。。

### Ⅵ 额外功能

よし～ ，走到这里说明你已经成功了（之前有问题也不要着急先度娘或谷哥再问我），那么我们看看如何把这个博客优化一下吧。

* Google analytics：需要自备梯子，进入[官网](https://analytics.google.com)注册账号先，获得了UA码（for free，但不知道谷歌他怎么用你数据，对这些大公司反正我是不会仔细研究那些“我同意“同意的具体是啥的）之后，打开我们的`_includes/analytics.html`，在最后（但在</script>前）添加两句话：

  ```yaml
    ga('create', 'UA-你获得的码', 'auto');
    ga('send', 'pageview');
  ```

* 其他还没试过┭┮﹏┭┮。

### Ⅶ 总结怪发言

祝大家一路顺利_/



