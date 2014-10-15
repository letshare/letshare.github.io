title: css之flex
date: 2013-07-23 19:10:00
tags: ['前端','css']
categories: css
---

##flex
flex是css3新增的display值，它是为了更加复杂的web布局而生的。一般中文翻译为伸缩布局。长期以来人们都是使用表格、浮动、行内块元素和其他 CSS 属性来布局网站内容。要实现在使用了居左对齐、居右对齐、两端对齐、居中对齐、顶端对齐、底部对齐常常比较麻烦，处理项目之间的空白和项目宽度、高度的伸缩也很让人头疼。而使用flex属性之后，这些都可以简单的设置到。

w3组织提到flex让我们轻易地可以实现这些：
+ 可以以任何伸缩方向（向左、向右、向下，甚至是向上！）配置
+ 可以在样式层（也就是视觉顺序可以跟源码、语音顺序无关）调换、重排显示顺序
+ 可以沿着单一（主）轴线性配置或是沿着第二（侧）轴折行
+ 可以因为可用空间的存在扩展内容的尺寸
+ 可以沿着容器或彼此对齐
+ 可以在保持侧轴长度不变之下动态折叠或反折叠

##概念和术语
一个设有「display:flex」或「display:inline-flex」的元素是一个伸缩容器，伸缩容器的子元素被称为伸缩项目，这些子元素使用伸缩布局模型来排版。

与布局计算偏向使用书写模式方向的块布局与行内布局不同，伸缩布局偏向使用伸缩流的方向。为了让描述伸缩布局变得更容易，本章节定义一系列相对于伸缩流的术语。「flex-flow」的值决定了这些术语如何对应到物理方向（上／右／下／左）、物理轴（垂直／水平）、物理大小（宽度／高度）。
![一个row伸缩容器中各种方向与大小术语的示意图。](/img/201307/flex-intro.png)

**主轴、主轴方向**  
	浏览器沿着一个伸缩容器的主轴渲染伸缩项目，主轴是主轴方向的延伸。

**主轴起点、主轴终点**  
	伸缩项目的配置从容器的主轴起点边开始，往主轴终点边结束。

**主轴长度、主轴长度属性**  
	伸缩项目的在主轴方向的宽度或高度就是项目的主轴长度，伸缩项目的主轴长度属性是「width」或「height」属性，由哪一个对着主轴方向决定。

**侧轴、侧轴方向**  
	与主轴垂直的轴称作侧轴，是侧轴方向的延伸。

**侧轴起点、侧轴终点**  
	填满项目的伸缩行的配置从容器的侧轴起点边开始，往侧轴终点边结束。

**侧轴长度、侧轴长度属性**  
	伸缩项目的在侧轴方向的宽度或高度就是项目的侧轴长度，伸缩项目的侧轴长度属性是「width」或「height」属性，由哪一个对着侧轴方向决定。

##伸缩容器
```css
.container {
  display: flex; /* 或 inline-flex */
}
```

这定义了一个伸缩容器。

伸缩容器会为其内容建立新的伸缩格式化上下文(flex formatting context)。除了使用伸缩排版而不块排版以外，伸缩格式化上下文与块级格式化上下文(block formatting context)根元素相同 ― 浮动不会闯入伸缩容器，且伸缩容器的边界不与其内容的边界叠加。

伸缩容器不是块容器，因此有些设计用来控制块布局的属性，在伸缩布局中不适用。column-*、float、clear、vertical-align在伸缩布局中不适用。

###flex-direction
![](/img/201307/flex-direction1.svg)
这个主要用来创建主轴，从而定义了伸缩项目放置在伸缩容器的方向。
```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```
+ `row`(默认值)：在`ltr`排版方式下从左向右排列；在`rtl`排版方式下从右向左排列。
+ `row-reverse`：与`row`排列方向相反，在`ltr`排版方式下从右向左排列；在`rtl`排版方式下从左向右排列。
+ `column`：类似 于`row`，不过是从上到下排列
+ `column-reverse`：类似于`row-reverse`，不过是从下到上排列。

###flex-wrap
![](/img/201307/flex-wrap.svg)
默认伸缩容器是单行显示，你可以这个定义属性决定伸缩容器里是单行还是多行显示，侧轴的方向决定了新行堆放的方向。
```css
.container{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```
+ `nowrap`(默认值)：伸缩容器单行显示，`ltr`排版下，伸缩项目从左到右排列；`rtl`排版上伸缩项目从右向左排列。
+ `wrap`：伸缩容器多行显示，`ltr`排版下，伸缩项目从左到右排列；`rtl`排版上伸缩项目从右向左排列。
+ `wrap-reverse`：伸缩容器多行显示，`ltr`排版下，伸缩项目从右向左排列；`rtl`排版下，伸缩项目从左到右排列。（和`wrap`相反）

###flex-flow
是flex-direction和flex-wrap的复合属性。
```css
.container{
  flex-flow: <‘flex-direction’> || <‘flex-wrap’>
}
```

###justify-content
![](/img/201307/justify-content.svg)
这个是用来定义伸缩项目沿着主轴线的对齐方式。当一行上的所有伸缩项目都不能伸缩或可伸缩但是已经达到其最大长度时，这一属性才会对多余的空间进行分配。当项目溢出某一行时，这一属性也会在项目的对齐上施加一些控制。
```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```
+ `flex-start`(默认值)：伸缩项目向一行的起始位置靠齐。
+ `flex-end`：伸缩项目向一行的结束位置靠齐。
+ `center`：伸缩项目向一行的中间位置靠齐。
+ `space-between`：伸缩项目会平均地分布在行里。第一个伸缩项目一行中的最开始位置，最后一个伸缩项目在一行中最终点位置。
+ `space-around`：伸缩项目会平均地分布在行里，两端保留一半的空间。

###align-items
![](/img/201307/align-items.svg)
这个主要用来定义伸缩项目可以在伸缩容器的当前行的侧轴上对齐方式。可以把他想像成侧轴（垂直于主轴）的“justify-content”。
```css
.container {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```
+ `flex-start`：伸缩项目在侧轴起点边的外边距紧靠住该行在侧轴起始的边。
+ `flex-end`：伸缩项目在侧轴终点边的外边距靠住该行在侧轴终点的边 。
+ `center`：伸缩项目的外边距盒在该行的侧轴上居中放置。
+ `baseline`：伸缩项目根据他们的基线对齐。
+ `stretch`（默认值）：伸缩项目拉伸填充整个伸缩容器。此值会使项目的外边距盒的尺寸在遵照「min/max-width/height」属性的限制下尽可能接近所在行的尺寸。

###align-content
![](/img/201307/align-content.svg)
这个属性主要用来调准伸缩行在伸缩容器里的对齐方式。类似于伸缩项目在主轴上使用“justify-content”一样。
> **注**：请注意本属性在只有一行的伸缩容器上没有效果。

+ `flex-start`：各行向伸缩容器的起点位置堆叠。
+ `flex-end`：各行向伸缩容器的结束位置堆叠。
+ `center`：各行向伸缩容器的中间位置堆叠。
+ `space-between`：各行在伸缩容器中平均分布。
+ `space-around`：各行在伸缩容器中平均分布，在两边各有一半的空间。
+ `stretch`（默认值）：各行将会伸展以占用剩余的空间。

##items
上一个章节介绍都是伸缩容器的属性，下面介绍一些伸缩项目的属性。

###order
默认情况下，伸缩项目是按照文档流出现先后顺序排列。然而，“order”属性可以控制伸缩项目在他们的伸缩容器出现的顺序。
```css
.item {
  order: <integer>;
}
```

###flex-grow
剩余空间是正值的时候此伸缩项目相对于伸缩容器里其他伸缩项目能分配到空间比例。

如果所有伸缩项目的`flex-grow`设置了"1"，那么每个伸缩项目将设置为一个大小相等的剩余空间。如果你给其中一个伸缩项目设置了`flex-grow`值为"2"，那么这个伸缩项目所占的剩余空间是其他伸缩项目所占剩余空间的两倍。
```css
.item {
  flex-grow: <number>; /* default 0 */
}
```
负值同样生效。

###flex-shrink
剩余空间是负值的时候此伸缩项目相对于伸缩容器里其他伸缩项目能收缩的空间比例。
```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```
负值同样生效。

###flex-basis
这个用来设置伸缩基准值，在分配剩余空间前，决定伸缩项的默认尺寸。负长度不合法
```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

###flex
这是`flex-grow`、`flex-shrink`和`flex-basis`三个属性的缩写。其中第二个和第三个参数（`flex-shrink`、`flex-basis`）是可选参数。默认值为"0 1 auto"。
```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
####flex的常见值
1. 「flex: 0 auto」「flex: initial」        
与「flex: 0 1 auto」相同。（这也就是初始值。）根据「width」／「height」属性决定元素的尺寸。（如果项目的主轴长度属性的计算值为「auto」，则会根据其内容来决定元素尺寸。）当剩余空间为正值时，伸缩项目无法伸缩，但当空间不足时，伸缩项目可收缩至其最小值。网页作者可以用对齐相关的属性以及「margin」属性的「auto」值控制伸缩项目沿着主轴的对齐方式。
2. 「flex: auto」    
与「flex: 1 1 auto」相同。根据「width」／「height」属性决定元素的尺寸，但是完全可以伸缩，会吸收主轴上剩下的空间。如果所有项目均为「flex: auto」、「flex: initial」或「flex: none」，则在项目尺寸决定后，剩余的正空间会被平分给是「flex: auto」的项目。
3. 「flex: none」  
与「flex: 0 0 auto」相同。根据「width」／「height」属性决定元素的尺寸，但是完全不可伸缩。其效果与「initial」类似，但即使在空间不够而溢出的情况下，伸缩项目也不能收缩。
4. 「flex: `<positive-number>`」  
与「flex: <positive-number> 1 0px」相同。该值使元素可伸缩，并将伸缩基准值设置为零，导致该项目会根据设置的比率占用伸缩容器的剩余空间。如果一个伸缩容器里的所有项目都使用此模式，则它们的尺寸会正比于指定的伸缩比率。

默认状态下，伸缩项目不会收缩至比其最小内容尺寸（最长的英文词或是固定尺寸元素的长度）更小。网页作者可以靠设置「min-width」或「min-height」属性来改变这个默认状态。

###align-self
用来在单独的伸缩项目上覆写默认的对齐方式。  
属性值的介绍请参阅“align-items”的属性值。
```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```


##浏览器的支持情况如下：

<table>
	<thead>
		<tr>
			<th>Chrome</th>
			<th>Safari</th>
			<th>Firefox</th>
			<th>Opera</th>
			<th>IE</th>
			<th>Android</th>
			<th>iOS</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>20- (old)<br>21+ (new)</td>
			<td>3.1+ (old)<br>6.1+ (new)</td>
			<td>2-21 (old)<br>22+ (new)</td>
			<td>12.1+ (new)</td>
			<td>10 (tweener)<br>11+ (new)</td>
			<td>2.1+ (old)<br>4.4+ (new)</td>
			<td>3.2+ (old)<br>7.1+ (new)</td>
		</tr>
	</tbody>
</table>

+ (new) 意味着使用最新的语法 ( 例如：display: flex;)
+ (tweener)意味着使用自2011年的老的非官方的语法 (例如：display: flexbox;)
+ (old) 意味着使用自2009年的老的语法 (例如：display: box;)

##示例
考虑使用6个列表项，并且为了视觉审美给他设置了一个固定大小尺寸，但他们也有可能可以自动获取尺寸大小。我们希望他们能均匀的、很好的分布在水平轴上，就算当我们调整浏览器，他们也依然显示得很好（不使用媒体查询）。
```css
.flex-container {
  /* 我们第一步要创建一个flex文档流（创建伸缩容器） */
  display: flex;
  
  /* 然后我们定义伸缩流方向，并且可以换行
   * 记得我们要这样设置:
   * flex-direction: row;
   * flex-wrap: wrap;
   */
  flex-flow: row wrap;
  
  /* 然后我们定义了如何分配伸缩容器的剩余空间 */
  justify-content: space-around;
}	
```
完成。其他的一切都不过是一些美化外观样式。下面是在codepen上展示的一个例子。到codepen上查看，并试着调整你浏览器窗口去看发生什么事？

<p data-height="268" data-theme-id="0" data-slug-hash="LklCv" data-default-tab="result" data-user="HugoGiraudel" class='codepen'>See the Pen <a href='http://codepen.io/HugoGiraudel/pen/LklCv/'>Demo Flexbox 1</a> by Hugo Giraudel (<a href='http://codepen.io/HugoGiraudel'>@HugoGiraudel</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

让我们试试别的。假设我们网站顶部有一个右对齐的导航，但是我们希望它在小屏幕和小型设备中能单列居中显示。非常简单。
```css
/* Large */
.navigation {
  display: flex;
  flex-flow: row wrap;
  /* 所有列面向主轴终点位置靠齐 */
  justify-content: flex-end;
}

/* Medium screens */
@media all and (max-width: 800px) {
  .navigation {
    /* 当在中等屏幕中, 导航项目居中显示，并且剩余空间平均分布在列表之间 */
    justify-content: space-around;
  }
}

/* Small screens */
@media all and (max-width: 500px) {
  .navigation {
    /* 在小屏幕下, 我们没有足够空间行排列，但我们可以换成列排列 */
    flex-direction: column;
  }
}	
```
<p data-height="268" data-theme-id="0" data-slug-hash="pkwqH" data-default-tab="result" data-user="HugoGiraudel" class='codepen'>See the Pen <a href='http://codepen.io/HugoGiraudel/pen/pkwqH/'>Demo Flexbox 2</a> by Hugo Giraudel (<a href='http://codepen.io/HugoGiraudel'>@HugoGiraudel</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

让我们尝试一些更灵活性的伸缩项目！关于移动先行，3列布局与页眉页脚全屏。和独立的文档顺序。
```css
.wrapper {
  display: flex;
  flex-flow: row wrap;
}

/* 设置所有标签宽度为100% */
.header, 
.main, 
.nav, 
.aside, 
.footer {
  flex: 1 100%;
}

/* 我们利用文档流顺序，考虑移动端先行
 * 在这个例子中的顺序:
 * 1. header
 * 2. nav
 * 3. main
 * 4. aside
 * 5. footer
 */

/* Medium screens */
@media all and (min-width: 600px) {
  /* 两个边栏在同一行 */
  .aside { flex: 1 auto; }
}

/* Large screens */
@media all and (min-width: 800px) {
  /* 设置左边栏在主内容左边
   * 设置主内容区域宽度是其他两个侧边栏宽度的两倍
   */
  .main { flex: 2 0px; }
  
  .aside-1 { order: 1; }
  .main    { order: 2; }
  .aside-2 { order: 3; }
  .footer  { order: 4; }
}	
```
<p data-height="268" data-theme-id="0" data-slug-hash="qIAwr" data-default-tab="result" data-user="HugoGiraudel" class='codepen'>See the Pen <a href='http://codepen.io/HugoGiraudel/pen/qIAwr/'>Demo Flexbox 3</a> by Hugo Giraudel (<a href='http://codepen.io/HugoGiraudel'>@HugoGiraudel</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

###参考
+ [http://css-tricks.com/using-flexbox/](http://css-tricks.com/using-flexbox/)
+ [http://css-tricks.com/snippets/css/a-guide-to-flexbox/](http://css-tricks.com/snippets/css/a-guide-to-flexbox/)
+ [http://www.w3cplus.com/css3/a-guide-to-flexbox.html](http://www.w3cplus.com/css3/a-guide-to-flexbox.html)
+ [http://www.w3.org/html/ig/zh/wiki/Css3-flexbox/zh-hans](http://www.w3.org/html/ig/zh/wiki/Css3-flexbox/zh-hans)
