title: 魔法javascript之事件
date: 2012-07-18 23:58
tags: ['DOM','事件']
categories: javascript
-----------------------------


##鼠标事件
`click、dbclick、mousedown、mouseout、mouseover、mouseup、mousemove`7个。

所有鼠标事件都会冒泡，也可以被取消，而取消鼠标事件将影响浏览器的默认行为，比如取消一个链接的默认行为，则会打开那个链接。

###触发顺序
只有在同一元素上相继触发mousedown 和 mouseup事件，才会触发click事件；如果mousedown或mouseup中的一个被取消，就不会触发click事件。类似地，只有触发两次click事件，才会触发一次dbclick事件。它们的顺序如下：
mousedown --> mouseup --> click -->  mousedown --> mouseup --> click --> dbclick

移动鼠标会同时发出mouseover(进入目标区)、mousemove(在目标区移动)、mouseout(离开目标区)。

###鼠标坐标
鼠标事件对象event属性clientX和clientY表示鼠标指针相对视口的位置;screenX和screenY 相对屏幕的位置。
表示修改的属性`shiftKey、ctrlKey、altKey、metaKey`，属性值代表了是否同时按住了那个键盘键，(ie不支持metaKey)。

##键盘事件
`keydown keyup keypress`3个。

###触发顺序
在用户按了一下键盘上的字符键时，首先会出发keydown事件，然后紧跟着是keypress，最后是keyup。其中，keydown和keypress都是在文本框发生变化之前被触发的，而keyup则是在文本框已经发生变化之后被触发的。按下按键持续不放的话，会重复出发keydown和keypress。

###如何获取按的键
键盘事件的event对象有3个属性：keyCode(键码), which, charCode(字符编码)
 
> keydown: 获得keyCode， charCode=0
> keypress: 字符（英文区分大小写+数字  / * , .  ...等非功能键），keyCode=0 ，获取charCode值， 反之获取keyCode， charCode=0
> keyup: 获得keyCode， charCode=0
> jquery 中 event.which = original.charCode != null ? original.charCode : original.keyCode;


总结：回车、上下左右、等功能键keydown、keypress、keyup都获取keyCode，并且值相等。
开启大写情况，keydown、keypress(字母，主键盘数字、回车)、keyup，which值相等，小写kepress获取的which不同于keypress、keyup。
 
keypress事件的keyCode对字母的大小写敏感，而keydown、keyup事件不敏感
keypress事件的which值无法区分主键盘上的数字键和附键盘数字键的，而keydown、keyup的which值对主附键盘的数字键敏感。

【
IE(ie9以下)只有一个属性KeyCode属性，当为keydown和keyup 事件是，keycode属性表示你具体按下的键(也称为virtual keycode)，当捕捉的是keypress事件时keyCode属性指的是你键入的字符(character code)   
 
标准浏览器中情况有些不同，event对象包含一个keyCode属性和一个charCode属性，keydown和keyup事件的时候，keyCode表示的就是你具体按的键，charCode为0；当捕捉的是keypress事件时，keyCode为0，charCode指的是你按下的字符，鉴于IE和FF中的区别，如果你比较懒的话，建议只使用keydow和keyup事件
】

部分浏览器支持DOM3的textInput事件，当用户在可编辑区域输入字符时就会触发此事件。

任何可获得焦点的元素都可触发keypress，只有可编辑区域才触发textInput。

三、HTML事件
window上的事件  load unload resize scroll 

四、变动事件
DOMSubtreeModified DOMNodeInserted DOMNodeRemoved DOMNodeInsertedIntoDocument DOMNodeRemovedFromDocument 
DOMAttrModified DOMCharacterDataModified  

五、专有事件
1.上下文菜单
     contextmenu事件，在dom上触发，属于鼠标事件，event.preventDefault可以取消系统自带的上下文菜单。
2.卸载前事件
     window上面的beforeunload
3.鼠标滚动（mousewheel）和DOMMouseScroll事件
     mousewheel可以在任何元素上触发，event对象包含一个特殊的wheelDelta属性，当用户向前滚动鼠标滚轮时，wheelDelta是120的倍数，当用户向后滚动鼠标滚轮时，wheelDelta是-120的倍数。要注意的是Opera9.5之前的版本中，wheelDelta值的正负号是颠倒的。
Firefox支持与mousewheel很相似的DOMMouseScroll事件，保存滚动位移的event对象的dtail的属性，向前滚是-3的倍数，向后滚是3的倍数。
4.DOMContentLoaded事件
     DOMContentLoaded事件会在形成完整的DOM树之后就会触发，不理会图像、Javascript文件、css文件或其他资源是否已经下载完成。
5.就绪状态变化（readystatechange）事件
     支持readystatechange事件的每个对象会有一个readyState属性，可取的值：
     uninitialized loading loaded interactive complete 
     readyState不总是连续的，并非所有阶段都会经历，document <link> <script>一般会支持这个事件
6.页面显示（pageshow）和页面隐藏（pagehide）事件
     firefox和opera有一个特性，名叫“往返缓存”，可以在 用户使用浏览器的“后退”和“前进”按钮时加快页面的转换速度。这个缓存中不仅保存着页面数据，还保存了DOM和Javascript的状态；实际上是将整个页面都保存在了内存里。如果页面位于bfcache中，那么再次打开该页面就不会触发load事件。
     是window上触发的事件，event对象有一个persisted属性表示页面是否保存在了bfcache中。

六、移动safari支持的事件
1.方向变化（orientationchange事件）
window上触发的事件，当用户改变了设备的查看方式就会触发orientationchange，window.orientation保存了代表方向的值
2.触摸事件
touchstart touchmove touchend touchcancel 事件
event对象保存了跟踪触摸的属性
touches:表示当前跟踪的触摸操作的TOUCH对象的数组
targetTouchs:特定于事件目标的Touch对象的数组
ChangedTouches：表示自上次触摸以来发生了什么改变的Touch对象的数组
3.手势事件
gesturestart gesturechange gestureend 事件
触摸事件和手势事件之间的关系。当一个手指放在屏幕上时，会出发touchstart事件。如果另一个手指又放在了屏幕上，则会先触发gesturestart事件，随后触发基于该手指的touchstart事件。如果一个或两个手指在屏幕上面滑动，将会触发gesturechange事件。但只要一个手指移开，就会触发gestureend事件，紧接着又会触发基于该手指的touchend事件。

七、事件模拟
DOM中的事件模拟
document.createEvent(type);
type有以下值 ：Events UIEvents MouseEvents MutationEvents HTMLEvents
firefox支持KeyEvents
一般调用init**Event() 完成事件对象的初始化，这些方法前三个参数都是type、bubbles、cancelable。
element.dispatchEvent(模拟的事件对象)可以触发事件。

IE中的事件模拟
document.createEventObject();
然后手动为event对象设置属性，如event.screenX = 100;
element.fireEvent("on"+type,模拟的事件对象)触发事件



