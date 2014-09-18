title: javascript魔法--语法
date: 2012-6-10 19:20:00
tags: ['前端','javascript']
categories: javascript
---

一门语言最基础的部分无非是数据类型、运算、控制语句。

##数据类型
javascript有5种基本数据类型 undefined 、 null 、  blooean 、 number 、 string。
null和undefined的区别：

|   比较     |  null     |   undefined  |
|-----------: |----------:|-------------:|
|  typeof    | object    |  undefined   |
| Number()   | 0         | NaN          |
| isNaN()    | false     |   true       |
| isFinite() |  true     |   false      |


##运算

###数学运算
即`+`、`-`、`*`、`/`、`%`。

对于五种数据类型以及对象都可以作为数学运算的操作数。5种基本类型先用`Number()`转化为数值;对象用`valueOf()`或`toString()`返回的值计算。Infinity与-Infinity的计算结果无法预计的时候为NaN,另外`Infinity*0 == NaN`。

另外需要注意：`+`是重载的，在有一个操作数是字符串的情况下，是字符串拼接符，而不是加运算。

另外鲜有人知道的是，Date类型与其他操作数进行`+`的时候,总是用toString转换为字符串而不是用valueOf转化为数值。

###位运算
`&`、`|`、 `^` 、`<<` 、`>>` 操作数也是任意，执行的时候会先转化为数值，
NaN,-Infinite ,Infinite会变为0，位移操作左操作数强制截取为32位整数，位移操作右操作数强制截取为（0-31）即5位整数。

###逻辑运算
&& 和 || 都是短路操作不一定返回布尔值，而是根据短路的情况返回值。例如：
```javascript
1 && ({});
// {}
0 && ({});
// 0
1 || ({});
// 1
0 || ({});
// {}
```
`~`按位非的本质是负值-1 即 `~num == -num -1 ;` 

###比较
比较操作符有`<`、`>`、`<`、`=>`、`=`、`==`、`!=` 、`===` 、`!==`。

两者都是字符串时，比较编码。其他情况统统比较数值，也就说想把两个比较的操作数转化为数值。

`==`、`!=`
除两者是对象，对象比较是否同一个引用，其他统统进行数值比较。但null、undefined、NaN特殊，跟其他比较时并不转化为数值。NaN != 任何，NaN与任何比较都是false。null==undefined。
```javascript
NaN != NaN;
// true
NaN == NaN;
// false
```

空字符串,false,0，null,undefined,NaN 的 `Boolean()`为false，即它们的逻辑值为false,其他任何为true。

##控制语句
javascript中的if、else匹配规则是，else总是和就近的if语句匹配。

`switch()`中表达式和case的比较是用的`===`。

`for(variable in object)`，首先执行的赋值，将object可枚举的属性名赋值给variable。

只有continue和break可以使用标签，标签的控制范围不能跨越函数边界。

`try{}catch()finally{}` 如果没有catch 异常会往上抛，传递给外层函数。

with语句块，块内变量优先尝试是否with对象的属性。对性能有损耗。


