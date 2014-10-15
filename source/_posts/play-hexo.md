title: 玩转hexo
date: 2014-08-12 19:50:12
categories: web
tags: ['hexo','blog']
photos:
- /img/201307/angelababy.jpg
- /img/201307/july.jpg
---

##一些小玩意
<!-- more -->
###fancybox
只要在markdown页头加上:
```markdown
title:  xxx
date: xxx
photos:
- /img/201307/angelababy.jpg
- /img/201307/july.jpg

```

###文章摘要
在需要显示摘要的地方加入：
```markdown
//以上为摘要内容
<!-- more-->
//以下为详细内容
```
那么在首页只会显示文章摘要，更多内容点击`Read More`跳到文章页。

这个功能跟主题有关，比如我的pacman主题就没有，而默认的landscape主题是有这个功能的。

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

你需要配置_config.yml的deploy选项，才可以用"hexo d"发布文章到github pages，说白了就是"hexo d"提交你的.deploy目录下的所有文件到你github pages对应的仓库中，
```
deploy:
  type: github
  repo: <repository url>
  branch: [branch]
  message: [message]
```
branch默认是master，message默认是`Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}`。


##BitTorrent
github pages是用hexo push到github仓库的，但我的文章源码并不想push到github仓库上。而我又想随处可以编辑我的文章，很多人说用dropdox，但被墙了，国内环境不好用。最终找到了[BitTorrent](http://www.bittorrent.com/)。这是个好东西，运用p2p技术，你的文件并不会传达某个云或服务器，安全私密性完全可以得到保障。通过二维码或密钥或链接的形式，将你的文件共享给别的节点。在BitTorrent中，各个同步的机器称为节点。据说Facebook就是运用BitTorrent协议技术在它的全球伺服器上同步代码。。

BitTorrent像git的.gitignore一样可以配置让某些文件不同步，比如你并不想同步发布的目录.deploy以及public，那么找到BitTorrent的同步目录.sync下的IgnoreList文件，配置方法跟.gitignore一样。比如：
```shell
.DS_Store
.Spotlight-V100
.Trashes
ehthumbs.db
desktop.ini
Thumbs.db
db.json
debug.log
public
.deploy
.git
```
BitTorrent有个bug，其他节点的IgnoreList是初始的IgnoreList，不是你同步出去的IgnoreList。比如hexo会生成public和.deploy目录，这两个目录是本地目录并不想同步给其他节点。经过我的测试找到了一个方法，我是输入密钥的方式同步源节点文件。
1. 第一次在别的机器同步文件后，马上断开链接。
2. 重新编辑这台机器的IgnoreList。
3. 还是输入那个密钥，还是把同步文件放在刚才的文件夹。
第二次建立同步链接的时候，并不会覆盖IgnoreLis，于是解决了这个问题，本地的public和.deploy目录就不会同步给其他节点了。


##参考
+ [https://help.github.com/categories/20/articles](https://help.github.com/categories/20/articles)
+ [https://help.github.com/articles/user-organization-and-project-pages](https://help.github.com/articles/user-organization-and-project-pages)
+ [http://hexo.io/docs/deployment.html](http://hexo.io/docs/deployment.html)


