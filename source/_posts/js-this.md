title: javascript与this
date: 2012-6-19 19:10:00
tags: ['前端','javascript']
categories: javascript
---

this跟arguments一样是函数执行时，活动对象的一部分。即this是动态的，函数执行时候绑定。
大概有这几种情况：
##五种this
###函数
当作为函数执行时，this等于window。
```javascript
var fn = function(){
	return this==window;
};
fn(); 
//true
```
不管函数fn在任何地方定义，是顶层函数还是嵌套，this都等于window。

###方法
当作为对象的方法执行时，this等于obj。
```javascript
var obj = {};
obj.fn = function(){
	return this==obj;
};
obj.fn();
//true
```

###定时器
setTimeout和setInterval的回调中，this总是等于window。
```javascript
var fn = function(){
	console.log(this==window);
};
setTimeout(fn,0); 
//true

var obj = {};
obj.fn = fn;
setTimeout(obj.fn,0); 
//true
```

###call,apply
call,apply将函数or方法绑定给了对象，this等于obj
```javascript
var obj = {};
var fn = function(){
	console.log(this==obj);
};
fn();
//false

fn.call(obj);
//true
```

###事件
在DOM0级事件属性绑定的回调中，this等于事件对象。
chrome等现代浏览器的事件处理程序中，this等于事件对象。
IE事件处理程序中，this等于window。
```javascript
//DOM0
btn.onclick = function(){
	console.log(this==btn);
}; //true
//chrome

btn.addEventListener("click",function(){
    console.log(this==btn);        //true
},false);

//IE
btn.attachEvent("onclick",function(){
    console.log(this==window);   //true
});
```
