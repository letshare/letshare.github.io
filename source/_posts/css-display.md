title: css之display和visibility
date: 2012-6-23 19:10:00
tags: ['前端','css']
categories: css
---

##display
display 属性规定元素应该生成的框的类型。
支持的类型有：

|值	                 | 描述
|:-------------------|:----------------
|none	             | 此元素不会被显示。
|block	             | 此元素将显示为块级元素，此元素前后会带有换行符。
|inline	             | 默认。此元素会被显示为内联元素，元素前后没有换行符。
|inline-block	     | 行内块元素。（CSS2.1 新增的值）
|list-item	         | 此元素会作为列表显示。
|run-in              | 此元素会根据上下文作为块级元素或内联元素显示。
|table	             | 此元素会作为块级表格来显示（类似 `<table>` ），表格前后带有换行符。
|inline-table        | 此元素会作为内联表格来显示（类似 `<table>`），表格前后没有换行符。
|table-row-group     | 此元素会作为一个或多个行的分组来显示（类似 `<tbody>`）。
|table-header-group	 | 此元素会作为一个或多个行的分组来显示（类似 `<thead>`）。
|table-footer-group  | 此元素会作为一个或多个行的分组来显示（类似 `<tfoot>`）。
|table-row           | 此元素会作为一个表格行显示（类似 `<tr>`）。
|table-column-group	 | 此元素会作为一个或多个列的分组来显示（类似 `<colgroup>`）。
|table-column	     | 此元素会作为一个单元格列显示（类似 `<col>`）
|table-cell          | 此元素会作为一个表格单元格显示（类似 `<td>` 和 `<th>`）
|table-caption	     | 此元素会作为一个表格标题显示（类似 `<caption>`）
|flex	             | 此元素将显示为块级flex元素。CSS3新增。
|inline-flex	     | 此元素将显示为内联flex元素。 CSS3新增。
|inherit             | 规定应该从父元素继承 display 属性的值。

如果规定了 !DOCTYPE，则 Internet Explorer 8 （以及更高版本）支持属性值 "inline-table"、"run-in"、"table"、"table-caption"、"table-cell"、"table-column"、"table-column-group"、"table-row"、"table-row-group"、以及 "inherit"。

inline-block结合了block和inline，它看起来像block，可以设置block盒子的所有属性，比如宽高。但是布局的时候跟inline一样显示在一行中，并不会在元素前后添加换行符。


##visibility
把 display 设置成 none 不会保留元素本该显示的空间，但是 visibility: hidden; 还会保留。