title: css之background
date: 2012-6-20 19:10:00
tags: ['前端','css','background']
categories: css
---

##background
background属性用于指定一个元素的background效果。
background包括一个元素的内容+内边距(padding)+边框(border)，不包括外边距(margin)
主要的background效果有：
+ background-color
+ background-image
+ background-repeat
+ background-attachment
+ background-position

###background-color
用于指定一个元素的背景颜色，颜色的设置有6中：

1.16进制，指定方法为：#RRGGBB ，比如：
```css
#p1 {background-color: #ff0000;} / * red */
```

2.RGB，指定方法为：rgb(red, green, blue),比如：
```css
#p1 {background-color: rgb(255,0,0);} / * red */
```

3.RGBA,IE9+才支持，指定方法为: rgba(red, green, blue, alpha),比如：
```css
#p1 {background-color: rgba(255,0,0,0.3);} / * red with 0.3opacity */
```

4.HSL,IE9+才支持，指定方法为: hsl(hue, saturation, lightness),比如：
```css
#p1 {background-color: rgba(255,0,0,0.3);} /* red with 0.3opacity */  
```

5.HSLA,IE9+才支持，指定方法为：hsla(hue, saturation, lightness, alpha),比如：
```css
#p1 {background-color: rgba(255,0,0,0.3);} / * red with 0.3opacity */
```

6.颜色名，比如：'red','blue'
```css
#p1 {background-color: red;} 
```

###background-image
指定一个元素的背景图片,默认情况下图片是铺满整个元素的，即在垂直和水平方向上重复背景。
```css
body {background-image:url('paper.gif');} 
```

###background-repeat
指定背景图片的重复方式,语法为：
```css
background-repeat: repeat|repeat-x|repeat-y|no-repeat|initial|inherit;
```
repeat和initial 都是垂直和水平重复。
repeat-x --> 水平重复
repeat-y --> 垂直重复
no-repeat --> 不重复

###background-position
指定背景图片在元素的开始位置，默认情况下从左上角开始。值的形式如下表:

<table>
  <thead>
  	<tr>
  	<th style="width:18%">值</th>
  	<th>描述</th>
  	</tr>
  </thead>
  <tbody>
  <tr>
    <td>left top<br>left center<br>left bottom<br>right top<br>right center<br>right bottom<br>center top<br>center center<br>center bottom<br></td>
    <td>如果只指定一个，另一个默认为"center"</td>	
  </tr>
  <tr>
    <td><i>x% y%</i></td>
    <td>以百分比的形式指定位置，左上角是(0% 0%),右下角是(100% 100%),如果只指定x%，y%默认为50%</td>
  </tr>
  <tr>
    <td><i>xpos ypos</i></td>
    <td>xpos指定水平位置，ypos指定垂直位置，左上角的坐标为(0px 0px),xpos、ypos使用单位值，也可以使用其他<a href="css_units.asp">CSS units</a>可以跟其他指定位置的方式混合使用，如果只有xpos，ypos默认为50%</td>
  </tr>
	<tr>
    <td>initial</td>
    <td>默认值 <a href="css_initial.asp">Read about <em>initial</em></a></td>
    </tr>
	<tr>
    <td>inherit</td> 
    <td>从它的父元素继承<a href="css_inherit.asp">Read about <em>inherit</em></a></td> </tr> </tbody>
</table>

###background-attachment
设置页面滚动的时候，背景图片是否跟着移动。有以下几种值:

<table>
  <thead>
  	<tr>
  	<th style="width:18%">值</th>
  	<th>描述</th>
  	</tr>
  </thead>
  <tbody>
  <tr>
    <td>scroll</td>
    <td>背景图跟着元素滚动，这是默认值</td>	
  </tr>
  <tr>
    <td>fixed</td>
    <td>背景图固定在是否位置</td>
  </tr>
  <tr>
    <td>local</td>
    <td>背景图跟着元素内容滚动</td>
  </tr>
	<tr>
    <td>initial</td>
    <td>默认值 <a href="css_initial.asp">Read about <em>initial</em></a></td>
    </tr>
	<tr>
    <td>inherit</td> 
    <td>从它的父元素继承<a href="css_inherit.asp">Read about <em>inherit</em></a></td> </tr> </tbody>
</table>

IE8及更早版本的浏览器不支持这个属性。

###简写形式
这些background的属性可以简写到一个名称为background的属性中。比如：
```css
body {
    background: #ffffff url("img_tree.png") no-repeat right top;
}
```
这些属性是否缺了一个不重要，重要的是要保持这样的顺序：
1. background-color
2. background-image
3. background-repeat
4. background-attachment
5. background-position