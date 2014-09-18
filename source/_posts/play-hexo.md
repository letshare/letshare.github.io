title: 玩转hexo
date: 2013-06-12 19:50:12
categories: web
tags: ['hexo','blog']
photos:
- /images/201307/angelababy.jpg
- /images/201307/july.jpg
---

##一些小玩意
<!-- more -->
###fancybox
只要在页头加上:
```markdown
title:  xxx
date: xxx
photos:
- /images/201307/angelababy.jpg
- /images/201307/july.jpg

```

###文章摘要
在需要显示摘要的地方加入：
```markdown
//以上为摘要内容
<!-- more-->
//以下为详细内容
```
那么在首页只会显示文章摘要，更多内容点击`Read More`跳到文章页

###description
可以在页头加上description描述网页，会转换为`<meta name="description" content="">`，有利于seo哦。

##主题安装
一个好的博客，除了内容优秀外，一个好的主题也重要，能传达一个博主的品味。[hexo thems](http://github.com/tommy351/hexo/wiki/Themes "hexo thems list")，个人比较喜欢pacman,简单大气小清新。

安装方式：
```bash
$ git clone https://github.com/A-limon/pacman.git themes/pacman
```
主题配置方式可以参阅它的主页[pacman](https://github.com/A-limon/pacman "pacman github")。

##github pages
github pages的发布有两种形式，一种是作为个人主页，访问链接为http(s)://username.github.io,
另外一种是作为项目页,访问链接为http(s)://username.github.io/projectnam。

个人主页需要建立一个名为username.github.io的repository，访问的页面发布在分支master下 ，而项目的的页面分支建在gh-pages分支下。


##参考
+ [https://help.github.com/categories/20/articles](https://help.github.com/categories/20/articles)
+ [https://help.github.com/articles/user-organization-and-project-pages](https://help.github.com/articles/user-organization-and-project-pages)



