title: 折腾hexo
date: 2014-09-01 19:50:12
categories: web
tags: ['hexo','blog']
---

要想让hexo博客更好，更符合我们自己的要求，就要弄清楚怎么配置hexo。先从hexo
的目录说起。。。。

##目录结构

###目录
```shell
.
├── .deploy
├── public
├── scaffolds
├── scripts
├── source
|   ├── _drafts
|   └── _posts
├── themes
├── _config.yml
└── package.json

```

+ .deploy：执行hexo deploy命令部署到GitHub上的内容目录
+ public：执行hexo generate命令，输出的静态网页内容目录
+ scaffolds：layout模板文件目录，其中的md文件可以添加编辑
+ scripts：扩展脚本目录，这里可以自定义一些javascript脚本
+ source：文章源码目录，该目录下的markdown和html文件均会被hexo处理。该页面对应repo的根目录，404文件、favicon.ico文件，CNAME文件等都应该放这里，该目录下可新建页面目录。
	* _drafts：草稿文章
	* _posts：发布文章
+ themes：主题文件目录
+ _config.yml：全局配置文件，大多数的设置都在这里
+ package.json：应用程序数据，指明hexo的版本等信息，类似于一般软件中的关于按钮

----------------------------------------------------------------------------------------------------

###配置
下面我们来看看全局配置文件，可以配置哪些东西。
```shell
# Site  #整站的基本信息
title: 寻图的博客 #网站标题
subtitle: 程序猿、全栈工程师 #网站副标题
description:  寻图的博客 | javascript | css | html | nodejs | java | php #网站描述，给搜索引擎用的，在生成html中的head->meta中可看到
author: bruce #网站作者，在下方显示
email: brucecai2012@gmail.com
language: zh-CN

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://www.xuntuu.com
root: /
permalink: :year/:month/:day/:title/
tag_dir: tags
archive_dir: archives
category_dir: categories
essay_dir: essays
code_dir: downloads/code
permalink_defaults:

# Directory
source_dir: source
public_dir: public

# Writing  #写文章选项
new_post_name: :title.md # File name of new posts
default_layout: post  #默认layout方式
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
highlight:  #代码高亮
  enable: true  #是否启用
  line_number: false  #是否显示行号
  tab_replace: 

# Category & Tag   #分类与标签
default_category: uncategorized
category_map:
tag_map:

# Archives  #存档，这里的说明好像不对。全部选择1，这个选项与主题中的选项有时候会有冲突
## 2: Enable pagination
## 1: Disable pagination
## 0: Fully Disable
archive: 2
category: 2
tag: 2

# Server  #本地服务参数
## Hexo uses Connect as a server
## You can customize the logger format as defined in
## http://www.senchalabs.org/connect/logger.html
port: 4000
server_ip: localhost
logger: false
logger_format: dev

# Date / Time format  #日期显示格式
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: MMM D YYYY
time_format: H:mm:ss

# Pagination #分页设置
## Set per_page to 0 to disable pagination
per_page: 10  #每页10篇文章
pagination_dir: page

# Disqus #社会化评论disqus，我使用多说，在主题中配置
disqus_shortname:

# Extensions
## Plugins: https://github.com/hexojs/hexo/wiki/Plugins
## Themes: https://github.com/hexojs/hexo/wiki/Themes
theme: pacman
exclude_generator:

# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: github
  repository: git@github.com:letshare/letshare.github.io.git  #你的GitHub Pages仓库
```

***********************************************************************

##修改局部页面
页面展现的全部逻辑都在每个主题中控制，源代码在hexo\themes\你使用的主题\中，以pacman主题为例：
```css
.
├── languages          #多语言
|   ├── default.yml    #默认语言
|   └── zh-CN.yml      #中文语言
├── layout             #布局，根目录下的*.ejs文件是对主页，分页，存档等的控制
|   ├── _partial       #局部的布局，此目录下的*.ejs是对头尾等局部的控制
|   └── _widget        #小挂件的布局，页面下方小挂件的控制
|── scripts            #脚本    
├── source             #源码
|   ├── css            #css源码 
|   |   ├── _base      #*.styl基础css
|   |   ├── _partial   #*.styl局部css
|   |   └── style.styl #*.styl引入需要的css源码
|   ├── fancybox       #fancybox效果源码
|   ├── font           #字体
|   ├── img            #图片
|   └── js             #javascript源代码
├── _config.yml        #主题配置文件
└── README.md          #用GitHub的都知道
```
如果你需要修改头部，直接修改hexo/themes/pacman/layout/_partial/header.ejs，比如搜索框替换成百度搜索：
```ejs
<form class="search" method="get" target="_blank" action="http://www.baidu.com/baidu" accept-charset="utf-8">       
    <input name="word" id="search" autocomplete="off" size="30" maxlength="30" placeholder="<%= __('search') %>" />
    <input type="submit" value="Baidu Search" style="display:none;"/>					       
    <input name="tn" type="hidden" value="bds" />
    <input name="cl" type="hidden" value="3" />
    <input name="si" type="hidden" value="www.xuntuu.com" />
    <input name=ie type=hidden value=utf-8>
    <input name="ct" type="hidden" value="2097152" />
    <label for="s">Search</label>
</form>
```
将如上代码加入即可，您需要修改css以便这个搜索框比较美观或跟你的主题一致，我就是使用了主题中原来google的搜索框样式。

***********************************************************************

##自定义404页面
GitHub Pages 自定义404页面非常容易，直接在对应分支（个人主页是master分支，项目也是gh-pages分支）根目录下创建自己的404.html就可以。hexo是在source目录下创建一个404.html，发布的时候会发布到对应分支的根目录下。
404页面其实可以一些不同寻常的事情，比如广告、宣传、公益，推荐几个公益404：

+ [腾讯公益404](http://www.qq.com/404)
+ [404公益_益云(公益互联网)社会创新中心](http://yibo.iyiyun.com/Index/web404)
+ [失蹤兒童少年資料管理中心404](http://404page.missingkids.org.tw/)

我接入的是腾讯404，你可以尝试下访问一个不存在的资源，比如：http://www.xuntuu.com/hello


***********************************************************************

##统计
因Google Analytics基本被墙，故用百度统计，以pacman主题为例，介绍如何添加。

首先在/themes/pacman/_config.yml添加这段配置。
```shell
bd_analytics:
  enable: true
```
新建 pacman/layout/_partial/bd_analytics.ejs,内容如下：
```ejs
<% if (theme.bd_analytics.enable){ %>
<script type="text/javascript">
  //你的百度统计代码
</script>
<% } %>
```
> 注册并登录百度统计获取你的统计代码。

编辑 pacman/layout/_partial/after_footer.ejs,在最后添加：
```ejs
<%- partial('bd_analytics') %>
```

***********************************************************************

##自定义挂件

除了默认已提供的挂件外，你还可以自定义自己的小挂件，在/themes/pacman/layout/_widget/下，新建自己的ejs文件，如myWidget.ejs，然后在配置文件/themes/pacman/_config.yml中配置。
```shell
widgets:
  - myWidget
```
用上述方法可以添加新浪微博小挂件。
+ 生成自己的微博组件。
+ 添加/themes/pacman/layout/_widget/weibo.ejs文件。
+ 配置/themes/pacman/_config.yml。

***********************************************************************

##分享和网站图标

pacman主题可以在配置中pacman/_config.yml配置图标：
```shell
favicon: img/favicon.ico
```
将你的favicon.ico放到工程根目录下的img即可，也就是hexo\source\img目录。可以在[Faviconer](http://www.faviconer.com/)制作你的ico图标，国内有[比特虫](http://www.bitbug.net/)。

***********************************************************************

##插件

安装插件：
```shell
npm install <plugin-name> --save
```

启用插件：在hexo/_config.yml文件添加：
```shell
plugins:
- <plugin-name>  #插件名
```

升级插件：
```shell
npm update
```

卸载插件：
```shell
npm uninstall <plugin-name>
```
###RSS插件
将上述命令中的『plugin-name』，替换为hexo-generator-feed。一旦安装完成，你可以在主题配置显示你站点的RSS，文件路径/atom.xml。

你可以用rss作为迁移工具，用如下命令读取其他位置的rss：
```shell
hexo migrate rss <source>
```
>『source』是本地或网络文件路径。

###Sitemap插件
将上述命令中的『plugin-name』，替换为hexo-generator-sitemap。安装好插件后在 _config.yml配置：
```shell
sitemap:
    path: sitemap.xml
```
每次生成博客的时候都会重新生成 sitemap.xml。你可以将你sitemap.xml提交给搜索引擎。

更多插件的安装方法，请参考[官方Wiki](https://github.com/hexojs/hexo/wiki/Plugins)。

******************************************************************************************

##工具推荐

###网站加速
[Webluker-CDN 网站加速 免费CDN DNS解析](http://www.webluker.com/)    
[Webluker-FAQ索引](http://blog.webluker.com/)

###网站监控
[监控宝-网站监控 网页监控 服务器监控](http://www.jiankongbao.com/)  
[监控宝-常见问题](http://www.jiankongbao.com/faq)

###站长工具
[谷歌站长工具](http://www.google.com/intl/zh-CN/webmasters)  
[百度站长工具](http://zhanzhang.baidu.com/)  
[站长之家工具](http://tool.chinaz.com/)  
[360搜索站长平台](http://zhanzhang.so.com/)  
[360网站安全检测](http://webscan.360.cn/)  
[奇云测](http://ce.cloud.360.cn/index)  
[360云监控](http://jk.cloud.360.cn/)  

###SEO
[谷歌搜索引擎优化初学者指南.PDF](http://www.google.com/intl/zh-CN/webmasters/docs/search-engine-optimization-starter-guide-zh-cn.pdf)

###数据统计
[百度统计](http://tongji.baidu.com/)    
[Google Analytics](http://www.google.com/analytics/web/?hl=zh-CN)

###企业邮箱
[腾讯企业邮箱](http://exmail.qq.com/)    
[在DNSPod域名解析商处如何设置企业邮箱](http://service.exmail.qq.com/cgi-bin/help?subtype=1&&id=20012&&no=1000931)

###图片生成
[邮箱地址生成图片](http://pic.sdodo.com/tool/mailpic)  
[MakePic.com邮址图片生成](http://www.makepic.com/email.php)

###徽章生成
[Logo Creatr](http://creatr.cc/creatr)    
[Web 2.0 Logo Creator](http://www.simwebsol.com/imagetool) _(可能需翻墙)_

###文章推荐/猜你喜欢
[无觅关联推荐](http://www.wumii.com/widget/relatedItems)  
[友荐](http://www.ujian.cc/)  
[乐知推荐](http://www.lezhi.me/)  
[百度推荐](http://tuijian.baidu.com/)  

###广告
[百度联盟](http://union.baidu.com/)  

**********************************************************************************************************

##常见问题
配置文件缺少空格会报错，每项配置:后面一定要加个空格，不知道的童鞋可能会中招。比如我就在配置git的时候冒号后面没加空格，出错后一直以为是其他问题。
```shell
deploy:
  type: github
  repository: git@github.com:youname/youname.github.io.git  
```

***********************************************************************************************************

##参考
+ [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)