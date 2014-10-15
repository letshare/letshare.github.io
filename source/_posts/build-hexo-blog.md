title: 用hexo建blog
date: 2014-08-02 20:08:20
categories: web
tags: ['hexo','blog']
---

##why hexo？
一直纠结该用什么写博客，wordpress、cnbolg、jekyll，直到遇到hexo。

它是用nodejs写的，跨平台、性能优秀，当文档很多时生成速度是jekyll的几十倍。而又保留了jekyll的好处，它是静态博客系统可以托管在github，使用markdown文档作为中间文档。

api简单好用：
```shell
$ hexo n #写文章
$ hexo g #生成
$ hexo d #部署 # 可与hexo g合并为 hexo d -g
```
下面介绍，如果搭建一个hexo博客。

<!--more-->

##环境准备

###安装nodejs
去[nodejs官网](http://nodejs.org/ 'noejs home')下载最新稳定版的nodejs。

###安装hexo
最新版的nodejs集成了npm，可以直接安装hexo。
```shell
$ npm install -g hexo
```
###安装git客户端
去[github官网](https://github.com/ 'github home')申请一个github账号。

因为本屌丝用的是windows，就用了[github的客户端](https://windows.github.com/ 'github client download')，它附带了一个git的shell工具。

###markdown
如果你不太熟悉markdown的使用，可以参考我的另外一篇文章[markdown用法](/2013/05/13/markdown-use/)

##hexo你的博客
###init
将一个目录初始成hexo项目，初始化后目录下有个package.json记录了依赖的nodejs模块，运行`npm install`，会安装好那些模块。

```shell
$ hexo init [folder] #如果不带folder，则默认为当前目录
$ npm install
```
###generate
生成静态页面，是将\source\_post\ 下的.md文件转换到\public\ 下的html文件
```bash
$ hexo g
```
###write
执行new命令，生成指定名称的文章至\source\_posts\postName.md。
```bash
hexo new [layout] "postName" #新建文章
```
layout默认为\scaffolds\post.md，生成的postName.md会在头部包含post.md的内容。你可以书写自己的layout，这样生成文章的时候可以指定为你自己的layout。

post.md的内容如下：
```markdown
title: {{ title }}
date: {{ date }}
tags:
---
```
生成的postName.md的内容如下：
```markdown
title: postName #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2013-06-01 18:40:26 #文章生成时间，一般不改，当然也可以任意修改
categories: #文章分类目录，可以为空，注意:后面有个空格
tags: #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
---
这里开始使用markdown格式输入你的正文。
```



