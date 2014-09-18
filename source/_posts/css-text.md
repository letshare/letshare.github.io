title: css之text
date: 2012-6-21 19:10:00
tags: ['前端','css','text']
categories: css
---

##css之text属性
是指文本格式的css属性，它们定义了文本如何呈现，比如文本颜色、大小写、对齐、缩进、字母间距、行高等。

###color
设置文本的颜色，比如：
```css
body {
    color: blue;
}
```
一个页面的默认文本颜色是由body指定的，其他元素的颜色继承自它。

###text-align
设置文本的水平对齐方式。语法:
```css
text-align : left | right | center | justify | initial | inherit ;
```
left左对齐,right右对齐,center居中,justify两端对齐。

###vertical-align
设置对象内容的垂直对齐方式。语法：
```css
vertical-align: baseline|length|sub|super|top|text-top|middle|bottom|text-bottom|initial|inherit ;
```

baseline对象的baseline跟父元素的baseline对齐。sub设置元素为下标。super设置元素为上标。top设置为文本对齐到元素内最高的子元素。text-top设置为文本对齐到父元素文字的顶部。

###text-decoration
添加或移除一个元素的文本装饰，主要用于移除链接的下划线。

<table>
	<thead>
		<tr>
			<th>值</th>
			<th>描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>none</td>
			<td>无装饰</td>
		</tr>
		<tr>
			<td>underline</td>
			<td>下划线</td>
		</tr>
		<tr>
			<td>overline</td>
			<td>上划线</td>
		</tr>
		<tr>
			<td>line-through</td>
			<td>删除线</td>
		</tr>
		<tr>
			<td>initial</td>
			<td>默认值，更多关于<a href="http://www.w3schools.com/cssref/css_initial.asp">默认值</a></td>
		</tr>
		<tr>
			<td>inherit</td>
			<td>继承自父元素的值，更多关于<a href="http://www.w3schools.com/cssref/css_inherit.asp">继承值</a></td>
		</tr>
	</tbody>
</table>

###text-transform
用于控制文本的大小写。text-transform属性有四个可选值：  
1. capitalize    
将每个单词的首字母转换为大写。例如：“john doe”将被转换为“John Doe”。
2. uppercase    
所有字母都转换为大写。例如：“john doe”将被转换为“JOHN DOE”。
3. lowercase    
所有字母都转换为小写。例如：“JOHN DOE”将被转换为“john doe”。
4. none    
不作任何转换——文本怎么写的就怎么显示。

###text-indent
语法:
```css
text-indent: length|%|initial|inherit;
```
百分比数字,是相对于父元素的宽度的百分比。length由浮点数字和单位标识符组成的长度值。它们都允许为负值。

###direction 
定义文本的书写方向，是从左往右，还是从右往左。语法：
```css
direction: ltr|rtl|initial|inherit;
```
ltr表示从左往右，是默认值。  
需要跟 unicode-bidi 一起使用

###unicode-bidi
跟direction属性一起决定是否应该被重写以支持多语言同一文档中一起使用。语法：
```css
unicode-bidi: normal|embed|bidi-override|intitial|inherit;
```
embed打开一个新的嵌入式，bidi-override打开一个新的嵌入层并重排序文字，比如：
```css
h1{
	direction:ltr;
	unicode-bidi:bidi-override;
}
```
```html
<h1>你好！</h1>
```
效果如下：
```html
!好你
```

###letter-spacing
增加或减少字符间的间距。语法：
```css
letter-spacing: normal|length|initial|inherit;
```

###word-spacing
增加或减少单词间的间距.语法：
```css
word-spacing: normal|length|initial|inherit;
```

###white-space
设置文本的空白如何处理。语法：
```css
white-space: normal|nowrap|pre|pre-line|pre-wrap|initial|inherit;
```  
normal是默认值，表示连续的空白会合并为一个空白，会自动换行。   
nowrap,连续的空白会合并，但不会自动换行。  
pre,既不合并也不会自动换行。  
pre-line,会合并空白但保留换行符，会自动换行。  
pre-wrap,不会合并，会自动换行

###line-length
设置文本的行高。语法：
```css
line-height: normal|number|length|%|initial|inherit;
``` 

###text-shadow
设置文字的阴影。语法：
```css
text-shadow: h-shadow v-shadow blur color|none|initial|inherit;
``` 
h-shadow是阴影相对于于文字的水平位置，必须。  
v-shadow是阴影相对于于文字的垂直位置，必须。  
blur是模糊效果的距离，可选。  
color是阴影的颜色，默认是文字的颜色，可选。  
这是**CSS3**属性，ie9及更早的版本不支持。  