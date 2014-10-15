title: css之position
date: 2012-6-25 19:10:00
tags: ['前端','css']
categories: css
---

##Positioning

定位属性决定了如何定位一个元素，以及如果元素的内容过大时如何处理。
主要有4种定位的方式。

###Static Positioning
即静态定位，是元素的默认定位方式。此时元素在正常的文档流中，这种情况下无法使用static。top，left，bottom，right属性。

###Fixed Positioning
即固定定位，元素的定位是相对于浏览器窗口的，页面滚动的时候，元素并不会跟着滚动。此时元素脱离了正常的文档流，其他元素的布局跟这个元素没有了关系，就像这个元素不存在。这个元素可以在其他元素上重叠。
```css
p.pos_fixed {
    position: fixed;
    top: 30px;
    right: 5px;
}
```
> IE7 和 IE8 只有在页面申明了 '!DOCTYPE '使用fixed才有效

###Relative Positioning
即相对定位，元素的位置是相对于其在文档流中的正常位置的，它可以移动和覆盖在其他元素上。其他元素不会受到它位置改变的影响，因为它在原来文档流的占有的空间不变。
```css
h2.pos_left {
    position: relative;
    left: -20px;
}

h2.pos_right {
    position: relative;
    left: 20px;
}
```

###Absolute Positioning
即绝对定位，元素的位置是相对于，它的第一个位置不是static position的父元素。如果没有父元素是非static position的，则的位置相对于`<html>`。
元素脱离了正常的文档流，可以覆盖在其他元素上，其他元素就像这个元素不存在一样布局。
```css
h2 {
    position: absolute;
    left: 100px;
    top: 150px;
}
```

###Overlapping Elements
当元素不在正常文档流的位置时，它可以跟其他元素重合。

z-index属性决定了一个元素的堆叠顺序，根据它和其他元素的堆叠顺序的比较，最终确定谁显示在上面，谁显示在下面(z-index值越大显示在越前面)。

> 如果两个元素都没有定义z-index属性，那么出现在html文档更后的元素显示在更上面。

###top、right、bottom、left
这4个属性在position为static的时候无效，它们值的正负如图所示：
![position](/img/201206/position.png)

水平方向，right的值跟left的值是相反的，垂直方向上，top的值跟bottom的值是相反的。  
left表示元素左边框相对某位置(abusolte是父元素左边框，fixed是浏览器窗口左边框，relative是元素自身左边框)向右偏移多少，而right相反表示元素右边框相对某位置向左偏移多少。

###其他

####clip
clip让你定义了矩形框剪切一个绝对定位的元素，矩形框的四个位置点是以元素左上角为原点的。

```css
clip: auto|shape|initial|inherit;
```
auto和initial 是默认值，不剪切，shape的值只能是 `rect (top, right, bottom, left)`  
例如剪切一个图片：

<p data-height="533" data-theme-id="8440" data-slug-hash="gchHD" data-default-tab="result" data-user="brucecai" class='codepen'>See the Pen <a href='http://codepen.io/brucecai/pen/gchHD/'>gchHD</a> by brucecai (<a href='http://codepen.io/brucecai'>@brucecai</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

> IE中 ie8及更新版本才支持