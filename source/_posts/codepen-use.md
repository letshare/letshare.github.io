title: 如何使用codepen
date: 2014-06-18 22:14:10
tags: ['codepen']
categories: 工具
-----------------------------

##简介
codepen是一个HTML, CSS和JavaScript的在线编辑器，可以所见即所得的看到代码的效果。而且它的作用不止代码的编辑，它可以用来分享代码，通过codepen可以更好的跟他人请教代码问题。

codepen的官网是：[codepen.io](https://codepen.io)。

##使用
codepen中一个项目称为一个pen。

使用codepen需要先到其官网注册账号，它有几种资费类型，免费账号已提供了比较多的功能。它的编辑器支持很多功能，比如：
+ html的预处理，可以使用Markdown、Haml、Slim、Jade来编写html。
+ css的预处理，可以使用SCSS、Sass、LESS、Stylus来编写css。
+ javascript的预处理，可以使用CoffeeScript、LiveScript来编写javascript。
+ 支持的js库有JQuery、MooTools、Prototype、Angular。

###分享别人的pen
在codepen首页展示一些共享的pen，并且可以按照被引用数、流行度、更新事件等排序。

比如：打开一个pen
![open public pen](/img/201401/pick-pen.png)

打开一个pen的代码页面后，选择右下角的"embed"就可以打开一个窗口,这个窗口用来设置一些选项，规定将codepen嵌入一个网页时的主题。
![embed this pen](/img/201401/embed-pen.png)

然后将那段embed代码嵌入网页就可以引入一个codepen项目了。比如下面将引入一个codepen：
```html
<p data-height="377" data-theme-id="8440" data-slug-hash="veshd" data-default-tab="result" data-user="amos" class='codepen'>See the Pen <a href='http://codepen.io/amos/pen/veshd/'>veshd</a> by amos (<a href='http://codepen.io/amos'>@amos</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>
```
<p data-height="377" data-theme-id="8440" data-slug-hash="veshd" data-default-tab="result" data-user="amos" class='codepen'>See the Pen <a href='http://codepen.io/amos/pen/veshd/'>veshd</a> by amos (<a href='http://codepen.io/amos'>@amos</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>