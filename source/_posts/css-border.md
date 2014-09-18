title: css之border和outline
date: 2012-6-22 19:10:00
tags: ['前端','css']
categories: css
---

##border
元素盒子模型中的边框。

###Border Style
border-style设置border的类型，它是border-xxx-style的复合属性，xx表示"top","right","bottom","left"。
有以下这些border-style。

<p style="border:none;">none border</p>
<p style="border:dotted 10px #98bf21;padding:3px;">a dotted border</p>
<p style="border:dashed 10px #98bf21;padding:3px;">a dashed border</p>
<p style="border:solid 10px #98bf21;padding:3px;">a solid border</p>
<p style="border:double 10px #98bf21;padding:3px;">a double border</p>
<p style="border:groove 10px #98bf21;padding:3px;">a groove border</p>
<p style="border:ridge 10px #98bf21;padding:3px;">a ridge border</p>
<p style="border:inset 10px #98bf21;padding:3px;">a inset border</p>
<p style="border:outset 10px #98bf21;padding:3px;">a outset border</p>
<p style="border:hidden;">A hidden border.</p>

border-style可以设置1-4个值，表示不同的方向的border的类型：

+ border-style: dotted solid double dashed;
	* top border is dotted
	* right border is solid
	* bottom border is double
	* left border is dashed
+ border-style: dotted solid double;
	* top border is dotted
	* right and left borders are solid
	* bottom border is double
+ border-style: dotted solid;
	* top and bottom borders are dotted
	* right and left borders are solid
+ border-style: dotted;
	* all four borders are dotted

###Border Width
border-width设置border的宽度，如果border-style:none会无效。语法：
```css
border-width: thin | medium | thick | length | inherit;
```
border-width是border-xx-width的复合属性，xx表示"top","right","bottom","left"。border-width同样可以设置1-4个值，跟border-style类似。

###Border Color
border-color设置border的颜色。border-color是border-xx-color的复合属性，xx表示"top","right","bottom","left"。border-color同样可以设置1-4个值，跟border-style类似。

###Border - Shorthand property
border是border-style、border-width、border-color 的复合属性，它们可以省略某项而且顺序不重要。比如：
```css
border: red dotted 4px 5px 3px;
```

border-top、border-right、border-bottom、border-left是设置不同方向的border的复合属性，可以省略某项而且顺序不重要。比如：
```css
border-top: red dotted 4px;
```

##outline
元素的轮廓，它不属于盒子模型的任意一部分，所以不算在元素总的width和height。它在border的外面,如果有margin是在margin上面的。

它跟border一样有三个复合属性outline-style、outline-color、outline-width，它们的值跟border一样，不同的是它们只能设置一个值，不能针对单个方向设置，所以方向的轮廓都是一样的。