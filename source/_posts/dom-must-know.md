title: DOM必知
date: 2012-7-3 19:20:20
tags: ['前端','javascript']
categories: javascript
---

##DOM必知

###id和name
如果在HTML文档中用id属性来为元素命名，并且如果window对象没有此名字的属性，window对象会赋予一个属性，它的名字是id属性的值，而它们的值指向表示文档元素的HTMLElement对象。
假设Id并没有被window对象使用的话，那么任何有id属性的html元素都会成为全局变量的值。以下元素如果有name属性的话，也会这么表现：
a applet area embed form frame frameset iframe img object

form img iframe applet(废弃) embed(html 5) object 会在document中创建name属性值为名字的属性，其中iframe创建的是window对象

###iframe
iframe 元素有contentWindow属性，引用该窗口的window对象，此window对象有个frameElement属性，表示此iframe 元素

全局对象处于作用域链的顶级，并且是全局变量和函数所定义的地方。事实上，全局对象会在窗口或窗口载入新内容时被替换。我们称为'window'对象实际上不是全局对象，而是全局对象的一个代理。

###data
html5为ELEMENT设计了data-xx属性 ，用element.data.xx访问

###原生选择器
ie8+，可以用querySelector和querySelectorAll传入css选择器选择节点，效果跟jQuery的选择器一样 

###模板引擎
可以将没有的src的script，type设置为某些值，text/x-custom-data 不执行，但可以用text属性植入文本。某些前端模板引擎就是利用这个，来暂存模板。

###富文本
设置HTML元素的contenteditable 可以使的元素可以编辑，还有spellcheck开启拼写检查 
设置Document元素的designMode = on 可以使得iframe 可以编辑，并可以使用命令

