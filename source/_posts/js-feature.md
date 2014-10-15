title: javascript魔法--特性
date: 2012-6-18 17:20:20
tags: ['前端','javascript']
categories: javascript
---

javascript特性中要重点理解的是函数、作用域、闭包。

##函数

javascript中函数也是一等对象，其原型最终继承于Object。

###声明和表达式的区别

函数表达式function后面可以不是函数名，最重要的判断依据是看上下文，是否执行了，比如这个函数表达式求值了者赋值给了左表达式，执行了的才就是函数表达式。比如：
```javascript
//下面是一个函数表达式
var func = function foo(){
	//do something;
}
//下面是一个函数声明
function foo(){
	//do something;
}
```

函数表达式function后面的函数名，变成了函数内部的局部变量，函数外部访问不到。
```javascript
var foo = function bar() {
    bar(); // 正常运行
}
bar(); // 出错：ReferenceError
```
bar在函数外是不可见的，这是因为我们已经把函数赋值给了foo。然而在bar内部依然可见。这是由于javascript 的命名处理所致，函数名在函数内总是可见的。

###变量查找
当访问函数内的`foo`变量时，javascript会按照下面顺序查找：
1. 当前作用域内是否有`var foo `的定义。
2. 函数形式参数是否有使用`foo`名称的。
3. 函数自身是否叫做`foo`。
4. 回溯到上一级作用域，然后从 #1 重新开始。

##作用域

很多人认为作用域是在函数执行时创建的，这是有偏差的理解！

###两种作用域
作用域分为词法作用域和动态作用域：
1. 词法作用域是在函数定义的时候创建的，作用域的本质是创建它的外层函数的调用对象组成的对象链，函数内部属性`[[scope]]`指向此作用域。
2. 当调用函数时，会创建一个**调用对象**（有些地方称**活动对象**），这个调用对象保存了函数参数和局部变量。将此调用对象推入词法作用域的前端，因此执行时作用域发生了变化，称为动态作用域。

###作用域链
实质上作用域只有一个，都是内部属性`[[scope]]`,词法作用域和动态作用域是时间上的不同造成的划分。作用域链是一条对象链，函数自己的活动对象，接着是父函数的活动对象，接着是祖父函数的活动对象......函数执行时，是沿着作用域链去寻找标识符的值的，先从自己的活动对象开始。with、catch 会改变动态作用域，将with的对象和catch的对象压入作用域链前端。
![作用域示意图](/img/201206/function-chains.png)

###变量查找效率
```javascript
var a,b,c;
var fn = function(){
    var d,e,f;
    return function(){ 
        var h,j,k; 
        return typeof nothing; 
        //nothing这个变量查找了整条作用域链，直到查询到window中这个变量，才返回"undefined".
    };    
};
```


为更好理解作用域，请尝试回答下下面的例子：
```javascript
var obj = {a:1,b:2};
var fn = function(){
	var c=3;
	var a = 5;
	console.log(a);   //a等于多少?
	with(obj){
		a=6;                        
		return function(){return a+c;};
	}
}(); 
fn();     //结果是多少?
```

##闭包

所谓**闭包**，指的是一个拥有许多变量和绑定了这些变量的环境的表达式（通常是一个内部函数），因而这些变量也是该表达式的一部分。

简单的看就是内部函数可以访问外部函数的变量。

###内存回收

当有闭包，且内部函数赋给了外部变量引用时，要特别注意内存。没有赋给外部变量时，代码执行完后执行环境销毁，不会有变量贮存内存。但赋给了外部变量时，闭包的词法作用域链会持有外层函数的活动对象，使得外部的变量不会回收。为了有效回收应该将变量设为null，断开引用。
```javascript
var fn = function(){
    var div = document.getElementById("div");
    return function(){};    
};  //div不会销毁
```





