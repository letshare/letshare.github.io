title: markdown简明使用
date: 2013-05-13 20:08:20
categories: 效率
tags: ['markdown']
---

##使用markdown的好处

>	1. 专心于写作，而不是排版
>	2. 语法简洁
>	3. 有github的支持
>	4. 逼格高，有个东东叫markdown+R，用于科技写作，RStudio

****************************

<!--more-->

##语法特点

###特殊符号
对特殊符号&、< 的处理是自动的。

&是html实体标签标识的时候不会被markdown处理，而作为普通字符的时候会被转换为`&amp;`。

<是html标签起始符的时候不会被markdown出来，而作为普通字符的时候会被转换为`&lt;`。

###内嵌html
块元素前后有空行、第一个标签前不能有缩进和空格。

```html
<div>
	<p>我是块元素</p>
</div>
```

<div>
	<p>我是块元素</p>
</div>

行元素随意嵌入。<a href="http://www.baidu.com" title="小心点会跳到百度">弄个链接试试</a>

*********************************************
##区块元素

###段落与换行
用空白行分割段落。markdown文档中的换行不会实际的插入`</br>`，如果确实想的话，可以在插入的地方加入两个以上空格  
然后换行

###标题
html中h1-h6表示，markdown中用#表示
```html
#h1
##h2
######h6
还可以这样：
一级标题
==========
二级标题
----------
```

###区块
写好一段文本，断好行，然后在每行最前面加>
````
>This is a blockquote with two paragraphs.

>Lorem ipsum dolor sit amet, consectetuer adipiscing elit.

>Aliquam hendrerit mi posuere lectus.

````
>This is a blockquote with two paragraphs.

>Lorem ipsum dolor sit amet, consectetuer adipiscing elit.

>Aliquam hendrerit mi posuere lectus.



###列表
支持无序列表和有序列表

无序列表在最前头加+、-或*，然后用空格隔开
```
+ 无
- 序
* 列
+ 表
```
 + 无
 - 序
 * 列
 + 表

无序列表在最前头加 数字及.

```
1. 有
2. 序
4. 列
8. 表
```
1. 有
2. 序
4. 列
8. 表

###代码块
一个空行隔开然后，开头4个空格或一个tab

	这里有代码块

###表格
```html
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
不加冒号是左对齐，两边有冒号表示中间对齐，冒号在右边表示右对齐
```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

###分割线
三个以上星号、减号或底号组成的行
````
***************

-------------

________________
````
##区段元素

###链接
```
行内式：
[链接文字](链接  'title')

参考式：
[链接文字][标识]
然后在另外一个地方定义标识
[标识]: 链接 'title'

```

###图片
跟链接很相似只有一个区别，在前面加!

###强调
\*或\_隔开， _奇_ 数个是`<em>`，**偶** 数个是`<strong>`

###行内代码
反引号\`隔开，`伪代码`。













