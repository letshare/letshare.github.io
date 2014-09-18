title: css之box model和BFC
date: 2012-6-21 19:10:00
tags: ['前端','css']
categories: css
---

##box model
文档中的每个元素被描绘为矩形盒子。确定其大小，属性——比如颜色、背景、边框，及其位置是渲染引擎的目标。

CSS下这些矩形盒子由标准盒模型描述。这个模型描述元素内容占用空间。盒子有四个边界：外边距边界margin edge, 边框边界border edge, 内边距边界padding edge 与 内容边界content edge。如图所示：
![box-model](/images/201206/box-model.gif)

每部分的含义如下：
+ Content - 真正包含元素内容的区域。文本和图片出现的地方。
+ Padding - 内容及可能的边框之间的空白区域。它是透明的。
+ Border - A border that goes around the padding and content 包围Content和Padding的边框。
+ Margin - 边框外部的空白区域，它是透明的。 

###width和height
元素的总width = width + left padding + right padding + left border + right border + left margin + right margin

元素的总height = height + top padding + bottom padding + top border + bottom border + top margin + bottom margin

###兼容问题
Internet Explorer 8 及更早的版本, padding and border 包含在 width中。
To fix this problem, add a <!DOCTYPE html> to the HTML page.

##块级元素和内联元素
一个 block 元素通常被叫做块级元素。一个 inline 元素通常被叫做内联元素(又称行内元素)。你无法设置width和height去控制一个内联元素的宽高，行内元素的宽高是根据它的内容来定的。

