title: javascript的ajax技术
date: 2012-07-05 20:45:18
tags: ['javascript','ajax','跨域']
categaries: javascript
-------------------------------------------
##跨域
###什么是跨域？
简单地理解就是因为JavaScript同源策略的限制，a.com 域名下的js无法操作b.com或是c.a.com域名下的对象。更详细的说明可以看下表：
![跨域图示](/img/201206/cross-domain.jpg)

---------------------------------------------------------------
##Ajax
###什么是AJAX?
即“Asynchronous Javascript And XML[1] ”（异步JavaScript和XML[1] ），是指一种创建交互式网页应用的网页开发技术。通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

###XHR
Ajax技术的核心是XMLHttpRequest对象（简称XHR）。IE7+和现代浏览器都支持，IE6及早期的IE用的是XMLHttp 的对象。我们可以这样来创建一个兼容的XHR。
```javascript
function createXHR(){
	if (typeof XMLHttpRequest != "undefined") {
        return new XMLHttpRequest();
    } else if (window.ActiveXObject) {
    //XMLHttp版本越新，性能越好，所以我们优先选用最新的
      var aVersions = [ "MSXML2.XMLHttp.5.0",
        "MSXML2.XMLHttp.4.0","MSXML2.XMLHttp.3.0",
        "MSXML2.XMLHttp","Microsoft.XMLHttp"
      ];

      for (var i = 0; i < aVersions.length; i++) {
        try {
            var oXmlHttp = new ActiveXObject(aVersions[i]);
            return oXmlHttp;
        } catch (oError) {
            //Do nothing
        }
      }
    }
    throw new Error("XMLHttp object could be created.");
}
```
###发送请求
创建xhr后我们就可以用来向服务器发送请求了。
```javascript
var xhr = createXHR();
xhr.open("get","example.php",false);
xhr.send(null);
```
open(method,url,async)方法有三个参数：
+ method：请求的类型；GET 或 POST
+ url：请求地址
+ async：true（异步）或 false（同步）

GET 和 POST发送请求的时候都可以带上参数，主要的区别的是，GET带数据参数的时候数据量受限于浏览器对URL长度的限制，而POST没有数据量的限制。

异步和同步的区别在于是否会阻塞代码的执行，同步的情况下，代码会等到服务器响应之后再继续执行。在收到响应之后，响应的数据会自动填充XHR对象的属性。而异步的情况下不会阻塞代码执行，通过事件监听去获得响应情况，在收到响应后数据会自动填充XHR对象的属性。响应数据的属性有：
responseText、responseXML，如果响应的内容类型是“text/xml”或“text/application”，这个属性中将保存包含着响应数据的XML DOM文档。如果响应内容是字符串则会填充到responseText中。

####onreadystatechange事件

这个事件对异步有作用，每当 readyState 改变时，就会触发 onreadystatechange 事件。readyState 属性存有 XMLHttpRequest 的状态信息。从 0 到 4 发生变化。
+ 0: 请求未初始化
+ 1: 服务器连接已建立
+ 2: 请求已接收
+ 3: 请求处理中
+ 4: 请求已完成，且响应已就绪
你的代码中应该少涉及到状态0-2的使用，因为有些浏览器并不支持。

另外还有一个属性表示响应码status，比如：
+ 200: "OK"
+ 404: 未找到页面

于是结合readyState == 4 && status==200，我们可以得知请求得到了正确响应，可以获取响应内容。
```javascript
xhr.onreadystatechange = function(){
	if(xmlhttp.readyState==4 && xmlhttp.status==200){
    	document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```

####HTTP头部信息
默认情况下，发送XHR请求的同时，会发送以下头部：
`Accept 、Accept-Charset 、 Accept-Encoding 、 Accept-Language 、Connection 、Cookie 、Host、 Referer 、User-Agent `
xhr.setRequestHeader(header,value)可以修改头部信息
xhr.getResponseHeader(header)可以取得响应头部信息
xhr.getAllResponseHeaders()可以取得一个包含所有头部信息的长字符串

####浏览器差异
ie8有ontimeout事件，可以处理超时，xhr.timeout设置超时。

在firefox某些版本利用onreadystatechange事件监听readystate==4会有一定概率fail，这是它的一个bug
[Firefox 3.5/Firebug XMLHttpRequest and readystatechange bug](http://www.nczonline.net/blog/2009/07/09/firefox-35firebug-xmlhttprequest-and-readystatechange-bug/)
但是它支持W3C的事件比如load、error、abort 、progress，所以可以用onload替换
```javascript
var xhr = new XMLHttpRequest();
if (firefox3_5){
    xhr.onload = xhr.onerror = xhr.onabort = function(){
        processResponse(xhr);
    };
} else {
    xhr.onreadystatechange = function(){
        if (xhr.readyState == 4){
            processResponse(xhr);
        }
    };
}
xhr.open("get", "/url", true);
xhr.send(null);
```
onload事件，相当于readystate==4的 onreadystatechange事件，还有个onprogress事件，获取接收数据进度，event对象的position表示已经接收到的字节数，totalSize表示根据Content-Length响应头部确定的预期字节数。

--------------------------------------------------------------
##跨域请求

###CORS

当前几乎所有的浏览器（Internet Explorer 8+， Firefox 3.5+， Safari 4+和 Chrome）都可通过名为Cross-Origin Resource Sharing（CORS）的协议支持ajax跨域调用。

对一个简单的请求，没有自定义头部，要么使用GET，要么使用POST，它的主体是text/plain,请求用一个名叫Orgin的额外的头部发送。Origin头部包含请求页面的头部（协议，域名，端口），这样服务器可以很容易的决定它是否应该提供响应。

Origin: http://www.nczonline.net

如果服务器确定请求被通过，它将发送一个Access-Control-Allow-Origin头部响应发送请求的同一个源，如果是一个公共资源，则返回“*”。如：

Access-Control-Allow-Origin: http://www.nczonline.net

先前提到的所有浏览器都支持这些简单的请求。FF3.5 +，Safari 4和chrome以及IE9+通过使用XMLHttpRequest对象支持其使用。当尝试在不同域打开一个资源时，不需任何代码，这个行为会自动触发。如：
```javascript
var xhr = new XMLHttpRequest();
xhr.open("get", "http://www.nczonline.net/some_resource/", true);
xhr.onload = function(){  //instead of onreadystatechange
    //do something
};
xhr.send(null);
```
在IE8你需要用到XDomainRequest，所以一个通用的代码可以这样：
```javascript
function createCORSRequest(method, url){
    var xhr = new XMLHttpRequest();
    if ("withCredentials" in xhr){
        xhr.open(method, url, true);
    } else if (typeof XDomainRequest != "undefined"){
        xhr = new XDomainRequest();
        xhr.open(method, url);
    } else {
        xhr = null;
    }
    return xhr;
}

var request = createCORSRequest("get", "http://www.nczonline.net/");
if (request){
    request.onload = function(){
        //do something with request.responseText
    };
    request.send();
}

```
我们需要用到“withCredentials”去检测 XMLHttpRequest 对象是否支持跨域请求。Firefox, Safari, and Chrome和IE8+通用的属性和方法有：
+ abort()——用来终止已在进程中请求。
+ onerror()——替代onreadystatechange方法来探测错误。
+ onload()——替代onreadystatechange方法来探测成功。
+ responseText——用来取得响应地文本。
+ send()——用来发送请求。

###Preflighted请求
除了GET或POST，通过一种称之为preflighted请求的服务器透明验证机制，CORS允许使用自定义的头部和方法，以及不同主体内容类型。当你尝试使用高级选项中的一个来试着建立一个请求时，这时就建立了一个preflighted请求。该请求使用可选的方法，并发送如下头部：
+ Origin——与简单请求相同。
+ Access-Control-Request-Method   ——请求将要使用的方法。
+ Access-Control-Request-Headers  ——（可选）一个逗号分开的正被使用的自定义头部列表。

在请求期间，服务器能决定是否允许这类请求。服务器通过在响应中发送以下头部来与浏览器通信。
+ Access-Control-Allow-Origin  ——与简单请求相同。
+ Access-Control-Allow-Methods ——用逗号分开的可接受的方法列表。
+ Access-Control-Allow-Headers ——用逗号分开的服务器可接受的头部列表。
+ Access-Control-Max-Age  ——preflighted 请求应该被缓存的时间。

**IE8不支持**

###Credentialed请求
默认状态下，跨域请求不提供证书（cookie、HTTP身份验证、客户端SSL证书）。你可以规定一个请求应该通过设置withCredentials属性为true来发送证书。如果服务器允许credentialed请求，那么它将用下面的头部作出响应：
> Access-Control-Allow-Credentials: true

如果一个credentialed请求被发送，这个头部不会作为响应地一部分被发送。浏览器不会将响应传递给JavaScript(responseText是一个空字符串，状态为 0，onerror()被调用)。注意，服务器也能发送这个HTTP头部作为preflight响应的一部分，以此来表明该源允许发送 credentialed请求。

**IE8不支持**

###对比

ie8的XDomainRequest与同域XHR的不同之处：
1. cookie不会随着请求发送，也不会随响应返回
2. 只能设置请求头部信息中的Content-Type字段，xhr.contentType = xxx，设置Content-Type字段
3. 不能访问响应头部信息
4. 只支持GET和POST请求
5. XDR只能访问Access-Control-Allow-Origin头部字段设置为*资源。
6. 用onload事件和onerror事件代替onreadystatechange事件

XMLHttpRequest的跨域请求，与同域XHR的不同之处：
1. 不能使用setRequestHeader()设置自定义头部，只能请求contentType为"text/plain"的资源
2. 不会发送也不会接收cookie
3. getAllResponseHeaders()方法只能返回空字符串
4. 要求远程资源设置Access-Control-Allow-Origin决定此域是否可以访问远程资源，但不限于"*"

##参考阅读
+ [XMLHttp Requests for Ajax](http://www.wrox.com/WileyCDA/Section/id-291289.html)  
+ [利用跨域资源共享（CORS）实现ajax跨域调用](http://www.weste.net/2011/4-27/75028.html)