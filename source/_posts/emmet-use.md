title: Emmet简明用法
date: 2013-01-18 23:58
tags: ['Emmet','Zen coding']
categories: 效率
-----------------------------

##简介
Emmet的前身是大名鼎鼎的Zen coding，如果你从事Web前端开发的话，对该插件一定不会陌生。它使用仿CSS选择器的语法来生成代码，大大提高了HTML/CSS代码编写的速度，比如下面的演示：
![Emmet演示](/img/201401/emmet-demo.gif)

###sublime下安装
`shift+ctrl+p`调出全局设置框，输入'install'，选择'package control:install package',搜索'emmet',选中后回车就会开始安装。

看状态条，装好后，就可以使用了，如果不能使用请重启sublime。

###使用
在编辑html文件的时候有两种方式：
1. `ctrl+alt+ENTER`调出一个abbreviation的交互命令窗口
2. 输入一段abbreviation后，按TAB键，前面的abbreviation就会扩展为完整的html片段

--------------------------------------------------------------------------------------------

##编写HTML代码 

###初始一个html文档 

HTML文档需要包含一些固定的标签，比如`<html>、<head>、<body>`等，现在你只需要1秒钟就可以输入这些标签。比如输入`!`或`html:5`，扩展后为：
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
</body>
</html>
```
html:5 或!：用于HTML5文档类型
html:xt：用于XHTML过渡文档类型
html:4s：用于HTML4严格文档类型

这些都是snippets，snippets是片段生成器。其他snippets比如：`c、cc、 cc:ie6、 cc:ie、 cc:noie`

###添加类、id、文本和属性 

连续输入元素名称和ID，Emmet会自动为你补全，比如`p.bar#foo`扩展为： 
```html
<p class="bar" id="foo"></p>
```

下面来看看如何定义HTML元素的内容和属性。你可以输入`h1{foo}+a[href=#]`，然后扩展为：
```html
<h1>foo</h1>
<a href="#"></a>
```
内容用`{}`、属性用`[]`包起来

###嵌套 

现在你只需要1行代码就可以实现标签的嵌套。 

+ `>`：子元素符号，表示嵌套的元素
+ `+`：同级标签符号
+ `^`：使标签提升一级

比如`p>span+div^div` 扩展为：
```html
<p>
	<span></span>
	<div></div>
</p>
<div></div>
```

###分组 

Emmet使用`()`来分组dom子树

你可以通过嵌套和括号来快速生成一些代码块，比如`(.foo>h1)+(.bar>h2)`，会扩展为： 
```html
<div class="foo">  
  <h1></h1>  
</div>  
<div class="bar">  
  <h2></h2>  
</div>  
```

###隐式标签 

省略标签名，只输入class，Emmet能根据父标签进行判定，然后生成需要的带class的标签。比如在外层输入`.item`会生成`<div class="item"></div>`。而在`<ul>`中输入`.item`，则会生成`<li class="item"></li>`。 

下面是所有的隐式标签名称： 
+ li：用于ul和ol中
+ tr：用于table、tbody、thead和tfoot中
+ td：用于tr中
+ option：用于select和optgroup中

###定义多个元素
要定义多个元素，可以使用`*`符号。比如，`ul>li*3`可以生成如下代码： 
```html 
<ul>  
  <li></li>  
  <li></li>  
  <li></li>  
</ul>  
```

还可以使用`$`给属性计数，比如`ul>li.item$$e#item$*3`生成：
```html
<ul>
	<li class="item01e" id="item1"></li>
	<li class="item02e" id="item2"></li>
	<li class="item03e" id="item3"></li>
</ul> 
```

还可以使用`@-`改变计数方向，`@N`改变计数起始数字，并且它们可以组合使用，比如`ul>li.item$@-3*5`生成：
```html
<ul>
    <li class="item7"></li>
    <li class="item6"></li>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
</ul>
```

###Lorem ipsum
"Lorem ipsum"是一段无意义的文本用于测试页面会如何显示，Emmet提供了一个"Lorem ipsum"生成器，非常方便好用。比如`ul.generic-list>lorem10.item*4`生成：
```html
<ul class="generic-list">
	<li class="item">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iure, maiores?</li>
	<li class="item">Repellat quia expedita ullam minima cum consectetur itaque sit quo.</li>
	<li class="item">Labore maiores, minus unde itaque repellat quis delectus, ipsa dolore.</li>
	<li class="item">Perferendis harum nulla quas necessitatibus nobis, amet dolorum unde aut!</li>
</ul>
```
lorem生成器后面的10表示的是单词数。

--------------------------------------------------------------------------------------------

##CSS缩写 

###值 

比如要定义元素的宽度，只需输入`w100`，即可生成 
```css
width: 100px;  
```

除了px，也可以生成其他单位，比如输入`h10p+m5e`，结果如下： 
```css
height: 10%;  
margin: 5em;  
```

单位别名： 
+ p --> %
+ e --> em
+ x --> ex

###附加属性 

可能你之前已经了解了一些缩写，比如 `@f`，可以生成： 
```css
@font-face {  
  font-family:;  
  src:url();  
}  
```

一些其他的属性，比如`background-image、border-radius、font、@font-face,text-outline、text-shadow`等额外的选项，可以通过"+"符号来生成，比如输入`@f+`，将生成： 
```css 
@font-face {  
  font-family: 'FontName';  
  src: url('FileName.eot');  
  src: url('FileName.eot?#iefix') format('embedded-opentype'),  
     url('FileName.woff') format('woff'),  
     url('FileName.ttf') format('truetype'),  
     url('FileName.svg#FontName') format('svg');  
  font-style: normal;  
  font-weight: normal;  
}  
```

###模糊匹配 

如果有些缩写你拿不准，Emmet会根据你的输入内容匹配最接近的语法，比如输入ov:h、ov-h、ovh和oh，生成的代码是相同的： 
```css
overflow: hidden;  
```

###浏览器厂商前缀 

如果输入非W3C标准的CSS属性，Emmet会自动加上浏览器厂商前缀，比如输入`trf`，则会生成:
```css
-webkit-transform: ;  
-moz-transform: ;  
-ms-transform: ;  
-o-transform: ;  
transform: ;  
```

你也可以在任意属性前加上"-"符号，也可以为该属性加上前缀。比如输入`-super-foo`： 
```css
-webkit-super-foo: ;  
-moz-super-foo: ;  
-ms-super-foo: ;  
-o-super-foo: ;  
super-foo: ;  
```

如果不希望加上所有前缀，可以使用缩写来指定，比如`-wm-trf`表示只加上-webkit和-moz前缀：
```css
-webkit-transform: ;  
-moz-transform: ;  
transform: ;  
```

前缀缩写如下： 
+ w 表示 -webkit-
+ m 表示 -moz-
+ s 表示 -ms-
+ o 表示 -o-

###渐变 
输入`lg(left, #fff 50%, #000)`，会生成如下代码： 
```css
background-image: -webkit-gradient(linear, 0 0, 100% 0, color-stop(0.5, #fff), to(#000));  
background-image: -webkit-linear-gradient(left, #fff 50%, #000);  
background-image: -moz-linear-gradient(left, #fff 50%, #000);  
background-image: -o-linear-gradient(left, #fff 50%, #000);  
background-image: linear-gradient(left, #fff 50%, #000);  
```

##定制 

你还可以定制Emmet插件： 

添加新缩写或更新现有缩写，可修改snippets.json文件,参考：[snippets.json](https://github.com/sergeche/emmet-sublime/blob/master/emmet/snippets.json)

更改Emmet过滤器和操作的行为，可修改preferences.json文件

定义如何生成HTML或XML代码，可修改syntaxProfiles.json文件

##针对不同编辑器的插件 

Emmet支持的编辑器如下:
+ [Sublime Text](https://github.com/sergeche/emmet-sublime) 
+ [Atom](https://github.com/emmetio/emmet-atom)
+ [Eclipse](https://github.com/emmetio/emmet-eclipse)
+ [Notepad++](https://github.com/emmetio/npp)
+ [NetBeans](https://github.com/emmetio/netbeans)
+ [更多>>](http://emmet.io/download/)