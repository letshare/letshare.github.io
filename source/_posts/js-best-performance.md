title: 高性能javascript编程
date: 2013-3-15 19:20:00
tags: ['前端','javascript']
categories: javascript
---

##优化代码

1. 不用使用二次编译代码，即将字符串编译为代码，javascript中有4中方式可以使用字符串形式的代码：
1. eval 2. Function 3. setTimeout 4. setInterval ,二次编译的时候会占用更多时间执行代码。

2. 使用对象和数组直接量，就是说不要使用new Object 和 new Array 而直接使用{}和[] 。

3. 不用做重复的工作，比如下面这段代码，
```javascript
function addHandler(target, eventType, handler){ 
	if (target.addEventListener){ //DOM2 Events
		target.addEventListener(eventType, handler, false); 
	} else { //IE 
		target.attachEvent("on" + eventType, handler); 
	} 
} 
```
每次调用的时候都会进行能力测试。我们可以通过以下两种方式改造：
1.延迟加载
延迟加载，简单来说就是需要的时候才加载：
```javascript
function addHandler(target, eventType, handler){ 
	//overwrite the existing function 
	if (target.addEventListener){ //DOM2 Events 
		addHandler = function(target, eventType, handler){ 
			target.addEventListener(eventType, handler, false); 
		}; 
	} else { //IE 
	 	addHandler = function(target, eventType, handler){ 
	 		target.attachEvent("on" + eventType, handler); 
		}; 
	}
	//call the new function
 	removeHandler(target, eventType, handler); 
}
```
2.条件预加载
它在脚本加载之前提前进行检查，而不等待函数调用。
```javascript
var addHandler = document.body.addEventListener ? 
function(target, eventType, handler){ 
	target.addEventListener(eventType, handler, false); 
}: 
function(target, eventType, handler){ 
	target.attachEvent("on" + eventType, handler); 
}; 
```
4. 数学运算的时候，优先考虑使用位操作，提高速度。位操作有： `&`、`|` 、`^`、 `~`。比如某些情况下可以用 `i&1`代替`i%1`。

5. 原生方法总是比JavaScript写的东西要快。尽量使用原生方法。

##优化web项目

1. 合理利用缓存，包括这个地方出现的缓存，浏览器、服务端、数据库。

2. 合并资源，比如小的javascript文件合并为大的javascript文件，这样可以减少HTTP请求数，发起HTTP请求是有损耗的，特别是在移动端。

3. jsmin ，压缩js文件，去除不必要的空格换行以及将局部变量名变短等，使得不改变js的功能下将js文件大小减小。

4. 开启gzip压缩，如果不能开启，大部分是有请求报文中缺少`Accept-Encoding`的HTTP头。

5. 使用CDN优化你的静态文件访问速度

