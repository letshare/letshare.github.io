title: javascript魔法--DOM
date: 2012-7-1 22:20:20
tags: ['前端','javascript']
categories: javascript
---

DOM（Document Object Model，文档对象模型）是一个通过和JavaScript进行内容交互的API。Javascript和DOM一般经常作为一个整体，因为Javascript通常都是用来进行DOM操作和交互的。

##DOM查找
###方法
主要有两个查找节点的方法：

1. document.getElementById(domid)
	因为domid唯一，所以返回唯一的节点
2. document.getElementsByTagName(tagname)
	
###属性
DOM API提供了大量的节点属性让我们来往上或者往下查询节点。

1. Node.parentNode: 访问当前节点的父节点，父节点只能有一个，祖节点可以用`Node.parentNode.parentNode`的形式来访问。
2. Node.childNodes: 访问一个单元素下所有的直接子节点元素，可以是一个可循环的类数组对象。该节点集合可以保护不同的类型的子节点（比如text节点或其他元素节点）。
3. Node.firstChild: 与`childNodes`数组的第一个项(`Element.childNodes[0]`)是同样的效果，仅仅是快捷方式。
4. Node.lastChild: 与'childNodes'数组的最后一个项(`Element.childNodes[Element.childNodes.length-1]`)是同样的效果，仅仅是快捷方式。shortcut。
5. Node.nextSibling: 访问DOM树上与当前节点同级别的下一个节点。
6. Node.previousSibling: 访问DOM树上与当前节点同级别的上一个节点。

![节点属性示意图](/images/201206/dom-find.png)

元素之间不能有空格，如果ul和li之间有空格的话，就会被认为是内容为空的text node节点，这样ul.childNodes[0]就不是第一个li元素了。相应地，`<p>`的下一个节点也不是`<ul>`，因为`<p>`和`<ul>`之间有一个空行的节点，一般遇到这种情况需要遍历所有的子节点然后判断nodeType类型，1是元素，2是属性，3是text节点，详细的type类型如下：
```javascript
Node.ELEMENT_NODE == 1
Node.ATTRIBUTE_NODE == 2
Node.TEXT_NODE == 3
Node.CDATA_SECTION_NODE == 4
Node.ENTITY_REFERENCE_NODE == 5
Node.ENTITY_NODE == 6
Node.PROCESSING_INSTRUCTION_NODE == 7
Node.COMMENT_NODE == 8
Node.DOCUMENT_NODE == 9
Node.DOCUMENT_TYPE_NODE == 10
Node.DOCUMENT_FRAGMENT_NODE == 11
Node.NOTATION_NODE == 12
```
javascript中的所有节点类型都继承自Node类型。表示nodeType的Node常量在IE中无效，必须用数字表示。

###NodeList
NodeList对象是一个节点的集合,是由Node.childNodes and the querySelectorAll返回的。每个节点都有一个NodeList属性保存了子节点，可以用索引可以用item访问单个子节点。非IE可以用Array.prototype.slice将NodeList转化为数组，而IE是将NodeList实现为COM对象，不可以转化为数组。

大多数情况下,NodeList对象都是个live集合。意思是说,如果文档中的节点树发生变化,则已经存在的NodeList对象也可能会变化。但如果该NodeList对象是由document.querySelectorAll(或者Element.querySelectorAll)方法返回的, 则它是非live的(就算把页面内的所有节点清空,links.length还等于2)。

---------------------------------------------------------------------------------------
##ELEMENT操作
###创建节点
document.createElement();

###是否包含子节点
判断元素是否含有某个子节点 parent.contains(child) ，firefox不支持。

###操作子节点
```javascript
parent.appendChild(childNode)  //添加子节点到parent下
new.insertBefore(parent,front)   //添加子节点new到parent下的front前面
parent.replaceChild(new,old)   //替换new节点替换掉old节点
parent.removeChild(node)      //移除子节点node
cloneNode = srcNode.cloneNode(true) //递归复制其子节点，false则不复制其子节点
```


###操作内容
`innerText、outerText 、innerHTML、outerHTML`四个属性可以直接读写，相应内容会发生改变

区别在于xxxText是去除了标签的纯文本，xxxHTML是HTML内容。

firefox中用textContent对应innerText,firefox不支持outerText。

读取的时候 innerText等于outerText，但写的时候inner 只会替换子节点 ，而outer会替换元素自身。

innerHTML写入`<script>`时只有ie支持，且要加defer，且认为是作用域外，必须在前面加一个作用域内元素才行，例如：文本，`<input type='hidden'/>`，`<div>&nbsp;</div>`


---------------------------------------------------------------------------------------
##几种NODE
###ELEMENT 
其nodeType等于1。

操作属性的方法：getAttribute、setAttribute、removeAttribut。属性名不区分大小写，使用标准的属性名即使是javascript保留字。

W3C规范还有一个方法 hasAttribute 用于判断是否含有某属性

###Text
其nodeType等于3。

创建一个Text节点document.createTextNode();

操作Text节点内容的方法有：
```javascript
var box = document.createElement('div');
box.id = 'box';
var text1 = document.createTextNode('Mr.');
var text2 = document.createTextNode('Cai!);
box.appendChild(text1);
box.appendChild(text2);
document.body.appendChild(box);
alert(box.childNodes.length);                             //2，两个文本节点
box.normalize();                                          //合并成一个节点
alert(box.childNodes.length);        //1
box.firstChild.splitText(3);       //分离一个节点，参数表示分离位置
alert(box.childNodes.length);        //2
box.firstChild.deleteData(0,2);                         //删除从0位置的2个字符
box.firstChild.insertData(0,'Hello.');                  //从0位置添加指定字符
box.firstChild.replaceData(0,2,'Miss');               //从0位置替换掉2个指定字符
box.firstChild.substringData(0,2);                    //从0位置获取2个字符，直接输出
alert(box.firstChild.nodeValue);                         //Missllo..
```
另外Text和CDATASection 都是CharacterData的子类型，可以用data和nodeValue属性获取文本

###DocumentFragment  
其nodeType等于11。

创建一个片段document.createDocumentFragment();  

将片段添加到文档中时，只会把片段的子节点添加进去，它本身不会成为文档树的一部分

---------------------------------------------------------------------------------------
##其他
###document
document代表整个文档
html == document.documentElement;
body == document.body;
document几个常用的属性
titile URL domain referrer

###节点的集合
document.images document.forms document.links document.anchors

###呈现模式
如何判断呈现模式是标准还是混杂？
```javascript
document.compatMode == "CSS1Compat"  //标准模式
document.compatMode == "BackCompat"  //混杂模式
```
ie8还有一个属性 document.documentMode，用于判断渲染模式，有以下值:
+ 5   表示 “in IE5 mode”
+ 7   表示 “in IE7 mode”
+ 8   表示 “in IE8 mode”
+ 9   表示 “in IE9 mode”

###滚动，让元素可视
element.scrollIntoView()滚动浏览器滚动条使得元素显示在视图 。 

属性scrollLeft、scrollTop 可用于设置有滚动条元素的滚动条位置。

window.scrollTo(xpos,ypos) 把内容滚动到指定的坐标。

window.scrollBy(xpos,ypos)如果有滚动条，将横向滚动条移动到相对于当前横向滚动条的x个像素的位置(就是向左移动x像素)，将纵向滚动条移动到相对于当前纵向滚动条高度为y个像素的位置(就是向下移动y像素)。


