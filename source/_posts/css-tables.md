title: css之table
date: 2012-6-21 19:10:00
tags: ['前端','css']
categories: css
---

##概述
一个表格由行(row)、列(column)、表格说明(caption)组成，行和列又是由一个个单元格(cell)组成。具体如下：
>table    { display: table }
>tr       { display: table-row }
>thead    { display: table-header-group }
>tbody    { display: table-row-group }
>tfoot    { display: table-footer-group }
>col      { display: table-column }
>colgroup { display: table-column-group }
>td, th   { display: table-cell }
>caption  { display: table-caption }

如图：
![tbl-layers.png](/images/201206/tbl-layers.png)

###Table Borders
可以设置table、td、th的border属性，值有：  
none | *hidden | dotted | dashed | solid | double | groove | ridge | *inset | *outset   
hidden跟none一样，但在合并边框模式下，也会隐藏其他border  
inset在边框分离模式下，整个表格看起来嵌入了页面，但在边框合并模式下，跟'ridge'一样  
outset在边框分离模式下，整个表格看起来凸出页面，但在边框合并模式下，跟'groove'一样

###Collapse Borders
设置边框是否合并，语法：
```css
border-collapse:collapse | separate | inherit
```
设置在table上，默认是separate。

collapse模式下，如果一个单元格被多个样式设置了边框，如何解决冲突呢？
1. border-style:hidden 是优先于其他边框设置，即边框会被隐藏
2. border-style:none 是最低的优先级，及有其他边框非hidden的style的时候的，这个单元格就会有边框
3. 如果有多种border-style时，优先选择border-width更大的，如果border-width都一样，则按以下顺序：'double', 'solid', 'dashed', 'dotted', 'ridge', 'outset', 'groove',  'inset'
4. 如果边框的颜色又有多种时，按以下优先决定：row, row group, column, column group , table。

separate模式下，可以设置table的border-spacing属性来设置边框的间距，语法：
```css
border-spacing:	<length> <length>? | inherit
```
如图所示：
![border-spacing](/images/201206/tbl-spacing.png)

separate模式下，可以设置table的empty-cells来控制空的cell是否显示border和background,语法：
```css
empty-cells:	show | hide | inherit
```

###Table Width and Height
比如设置表格的宽度为100%，th的高度为50px；
```css
table {
    width: 100%;
}

th {
    height: 50px;
}
```

###Table Text Alignment
设置单元格文本的水平对齐，例如： left, right,  center
```css
td {
    text-align: right;
}
```

设置单元格文本的垂直对齐，例如：baseline,top, bottom, middle
```css
td {
    height: 50px;
    vertical-align: bottom;
}
```
不能对cell的vertical-align设为sub, super, text-top, text-bottom, `<length>`, `<percentage>`

###Table Padding
设置文本内容和边框的间距，例如：
```css
td {
    padding: 15px;
}
```

###caption
设置cpation的位置，语法：
```css
capiton{
	caption-side:top | bottom | inherit
}

```


