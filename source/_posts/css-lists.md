title: css之lists
date: 2012-6-22 19:10:00
tags: ['前端','css','lists']
categories: css
---

##列表类型
ul表示无序列表。ol表示无序列表

###list-style-type
列表项目前的标记，ul和ol可用的标记不一样，如下：
```css
ul.a {list-style-type: circle;}
ul.b {list-style-type: disc;}
ul.c {list-style-type: square;}

ol.d {list-style-type: armenian;}
ol.e {list-style-type: cjk-ideographic;}
ol.f {list-style-type: decimal;}
ol.g {list-style-type: decimal-leading-zero;}
ol.h {list-style-type: georgian;}
ol.i {list-style-type: hebrew;}
ol.j {list-style-type: hiragana;}
ol.k {list-style-type: hiragana-iroha;}
ol.l {list-style-type: katakana;}
ol.m {list-style-type: katagana-iroha;}
ol.n {list-style-type: lower-alpha;}
ol.o {list-style-type: lower-greek;}
ol.p {list-style-type: lower-latin;}
ol.q {list-style-type: lower-roman;}
ol.r {list-style-type: upper-alpha;}
ol.s {list-style-type: upper-latin;}
ol.t {list-style-type: upper-roman;}

ol.u {list-style-type: none;}
ol.v {list-style-type: inherit;}
```

###list-style-image
使用图片作为列表项目前的标记。语法：
```css
ul {
   list-style-image: url();
}
```
使用图片作为标记在并不是所有的浏览器显示效果一样，可以使用以下方法作为替代：
```css
ul {
    list-style-type: none;
    padding: 0px;
    margin: 0px;
}

ul li {
    background-image: url(sqpurple.gif);
    background-repeat: no-repeat;
    background-position: 0px 5px; 
    padding-left: 14px; 
}
```

###list-style-position
设置列表项的标记应该显示在内容外面还是里面，语法:
```css
list-style-position: inside|outside|initial|inherit;
```

###list-style
list-style-type、list-style-position、list-style-image可以写在一个属性list-style里面，比如：
```
ul {
    list-style: square inside url("sqpurple.gif");
}
```
可以省略某个属性，但要保持这样的顺序：list-style-type、list-style-position、list-style-image。