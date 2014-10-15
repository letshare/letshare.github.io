title: css之font
date: 2012-6-20 19:10:00
tags: ['前端','css']
categories: css
---

##css font
设置文本字体样式

###font-family
设置字体类型。font-family属性用来定义一个或者多个字体集名称，在定义两个或者两个以上字体集名称的时候，必须用英文半角逗号 分隔这些名称。有的字体本身含有空格或者其他符号，例如"Times New Roman"、"Lucia Consol"，则必须把这些字体名称用双引号。

所谓通用字体集名称就是统一描述一类字体样式的名称，具体如表所示。

<table>
	<thead>
		<tr>
			<th>通用字体集名称</th>
			<th>说    明</th>
			<th>示    例</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>serif</td>
			<td>有边饰字体</td>
			<td style="font-family:serif;">serif,有边饰字体</td>
		</tr>
		<tr>
			<td>sans-serif</td>
			<td>无边饰字体</td>
			<td style="font-family:sans-serif;">sans-serif,无边饰字体</td>
		</tr>
		<tr>
			<td>cursive</td>
			<td>卷曲字体</td>
			<td style="font-family:cursive;">cursive,卷曲字体</td>
		</tr>
		<tr>
			<td>fantasy</td>
			<td>花哨字体</td>
			<td style="font-family:fantasy;">fantasy,花哨字体</td>
		</tr>
		<tr>
			<td>monospace</td>
			<td>独占位字体</td>
			<td style="font-family:monospace;">monospace,独占位字体</td>
		</tr>
	</tbody>
</table>

其中这些关键字本身并不是某种确定字体的名称，例如serif有边饰字体就包括"Times New Roman"、"Georgia"等多种字体，"sans-serif"就包括"Verdana"、"Arial"等字体，因此浏览器在遇到字体集名称的时候，会自动从系统 中寻找与之匹配的字体进行显示。

使用通用字体集名称的好处就是浏览器总能够从系统中找到与之相匹配的具体字体，而不必担心某种字体甚至备用字体都不可用。所以，设计者在定义任何字体的时候，最好在最后都加上一个通用字体集，以保证字体显示万无一失。


另外需要强调的是mac、window、photoshop、linux跨平台的情况下，中文字体的视觉有差异。
![font-cross-max-win](/img/201206/font-cross-max-win.png)

所以考虑到跨平台的问题，因为每种系统自带的字体不一样，特别是对中文的支持情况，所以推荐使用以下安全字体设置：
```css
宋体：font-family:STHeiti,simsun,Arial,sans-serif; （根据需求使用，如果是中文网页则推荐写到body里）
雅黑：font-family:STHeiti,'Microsoft Yahei',Simhei,Arial,sans-serif; （根据需求使用）
黑体：font-family:STHeiti,Simhei,Arial,sans-serif; （根据需求使用）
```
另外还有一种解决方案是使用@font-face，就可以不用考虑使用安全字体设置。@font-face的语法为：
```css
@font-face {
			font-family: 'FontName';
			src: url('FileName.eot');
			src: url('FileName.eot?#iefix') format('embedded-opentype'),
				 url('FileName.woff') format('woff'),
				 url('FileName.ttf') format('truetype'),
				 url('FileName.svg#FontName') format('svg');
			font-style: ;   /* 可选*/
			font-weight: ;   /* 可选*/
}
```

**参考：**
+ [网页跨平台字体探索实践](http://ued.orzk.com/2013/01/14/%E7%BD%91%E9%A1%B5%E8%B7%A8%E5%B9%B3%E5%8F%B0%E5%AD%97%E4%BD%93%E6%8E%A2%E7%B4%A2%E5%AE%9E%E8%B7%B5/)
+ [跨平台字体效果浅析](http://isux.tencent.com/5058.html)

###font-style
设置字体是否倾斜，值有:"normal","italic","oblique".
oblique跟italic相似也是倾斜，但oblique更少支持。

###font-size
设置字体大小，有绝对和相对大小两种形式。

绝对大小是将字体大小设置为绝对单位值：px、cm,如果设置为绝对大小，在ie8及早期版本不支持字体缩放。

相对大小是设置为em、%，是相对父元素的字体大小而言的。所有大小设置为em在缩放的时候ie早期版本会出现一些问题，大的更大小的更小，将body的font-size设置为100%，其他设置为em是最好的方式。默认页面的字体大小是16px。


###font-variant
设置字体是否显示为 small-caps ，small-caps 下，所有的小写字母会被转化为大写，但比正常的大写字母要小。

###font-weight
设置字体的粗细，语法为：
```css
font-weight: normal | bold | bolder | lighter | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900
```
normal与400一样大    
bold与700一样大    
lighter是比父元素字体更细一点的字体  	
bolder是比父元素字体更粗一点的字体  





