title: css基础
date: 2012-6-19 19:10:00
tags: ['前端','css']
categories: css
---

##概述
css指层叠样式表 (Cascading Style Sheets)

样式定义如何显示 HTML 元素


###层叠层次
当一个HTML元素运用了多个样式定义时，按照优先级最终确定显示效果：
1. 浏览器缺省设置
2. 外链样式
3. 内联样式（位于 <head> 标签内部）
4. 行内样式（在 HTML 元素内部）

4的优先级最高。

###css规则
CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。每条声明由一个属性和一个值组成。
```css
selector {declaration1; declaration2; ... declarationN }
```
例如：
```css
h1 {color:red; font-size:14px;}
```
![示意图](/img/201206/ct_css_selector.gif)

###选择器
css选择器让你可以找到html元素(基于它们的id, classes, types, attributes, values of attributes and much more)，并可以操作它们。

主要的选择器有：
####1. 标签选择器 
```css
p {
    text-align: center;
    color: red;
}
```
根据标签名选中了所有的p标签。

####2. id选择器
根据id名称，可以选中唯一的元素
```css
#para1 {
    text-align: center;
    color: blue;
}
```
####3. 类选择器
根据class值，可以选择某些元素
```css
.tlf {
    text-align: left;
}
```
####4. 组选择器
就是将一些定义相同的选择器组合在一起，每个选择器之间用`,`隔开
例如：
```css
h1 {
    text-align: center;
    color: red;
}

h2 {
    text-align: center;
    color: red;
}

p {
    text-align: center;
    color: red;
}
```
合并后，就是：
```css
h1, h2, p {
    text-align: center;
    color: red;
}
```

###引入css
主要有三种方式：
####1. 外部样式表
就是在head标签里link:css标签
```css
<link rel="stylesheet" type="text/css" href="mystyle.css">
```

####2. 内部样式表
就是在文档中加style标签，建议将这个标签放在head中

####3. 内联样式表
就是在标签的属性style中定义样式
```html
<h1 style="color:blue;margin-left:30px;">This is a heading.</h1>
```
####4. @import
```css
@import url (mystyle.css);
```
不要用，因为会带来很多问题，比如限制31个，firefox下不支持绝对路径，读取页面后才加载造成页面一开始没这个样式，javascript不能控制。

