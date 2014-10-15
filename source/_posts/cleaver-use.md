title: 30秒用cleaver做一个幻灯片
date: 2014-05-18 22:14:10
tags: ['cleaver','幻灯片','ppt','slider']
categories: 工具
author:
    name: Bruce Cai
    url: http://xuntuu.com
output: ../demo/smart-slide.html
-----------------------------

#  大家好!
## 这是一个幻灯片演示

####幻灯片演示请狂点这里[--》演示](/demo/smart-slide.html)

--

###简介
cleaver是一个幻灯片制作工具，将markdown文档转化为html5的幻灯片，它只有非常简单的规定：
+ markdown编写
+ 每页幻灯片用`--`分割

默认生成的幻灯片就已经很简约大气，而且你可以任意修改幻灯片的主题和样式。

<style type="text/css">
	.cleaver-cool{
		color: #66D9EF;
		background-image: url('../img/201401/cleaver-cool.jpg');
	}
</style>

-- cleaver-cool

#让你的
##幻灯片变得cool!

--

###简单使用
npm安装

`npm install -g cleaver`

运行

`cleaver cleaver-use.md`

然后就在当前目录下生成了一个cleaver-use-cleaver.html，它就是html5幻灯片

--

###配置
```markdown
title: 30秒用cleaver做一个幻灯片            //标题
author:									    //作者信息
    name: Bruce Cai
    url: http://xuntuu.com
output: ../html/smart-slide.html            //输出路径
style:                                      //自定义样式
theme:                                      //主题
```
配置信息放在页头

更多介绍:[title](https://github.com/jdan/cleaver/blob/master/docs/options.md#title), [author](https://github.com/jdan/cleaver/blob/master/docs/options.md#author), [theme](https://github.com/jdan/cleaver/blob/master/docs/options.md#theme), [style](https://github.com/jdan/cleaver/blob/master/docs/options.md#style), [output](https://github.com/jdan/cleaver/blob/master/docs/options.md#output), [controls](https://github.com/jdan/cleaver/blob/master/docs/options.md#controls), [progress](https://github.com/jdan/cleaver/blob/master/docs/options.md#progress), [encoding](https://github.com/jdan/cleaver/blob/master/docs/options.md#encoding), [template](https://github.com/jdan/cleaver/blob/master/docs/options.md#template), [layout](https://github.com/jdan/cleaver/blob/master/docs/options.md#layout)

--

###主题

一个包含stylesheet, template, layout, javascript的目录，指定你的幻灯片如何呈现

它可以是url、本地目录、git地址

在页头配置theme: url

比如`theme: ../themes/reveal-cleaver-theme-master`

--
###更多
+ `#`和`##`垂直居中，一个幻灯片只有`#`或`##`时会呈现为标题页
+ `###`时会呈现为内容页
+ `--`幻灯片分割符后面可以加class，作为这个幻灯页的特有样式


