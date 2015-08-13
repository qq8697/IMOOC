1、事件流 页面中接受事件的顺序
a)冒泡
b)捕获
2、添加/删除事件处理程序
a)HTML事件处理程序
<input type="button" value="按钮" onclick="showMessage()">
i.缺点：html和js耦合
b)DOM0级事件处理程序（先获取元素，再让事件以元素属性的形式出现并赋值给一个函数）
		var btn=document.getElementById("btn");
		btn.onclick=function(){}
//btn.onclick=null;
i.优点：跨浏览器 给一个元素添加多个事件处理程序。
ii.赋值为null即为清空事件处理程序。
c)DOM2级事件处理程序 addEventListener removeEventListener
		btn.addEventListener('click',handler,false);
btn.removeEventListener('click',handler,false);
i.参数：false是冒泡阶段，true是捕获阶段。
ii.优点：给一个元素添加多个事件处理程序。
iii.注意：通过addEventListener添加的事件只能由removeEventListener删除。
d)IE事件处理程序 
btn.attachEvent("onclick",handler);
		btn.detachEvent("onclick",handler);
3、事件对象 event
a)DOM中事件对象
i.type 事件类型
ii.target 事件目标
iii.stopPropagation()方法 阻止事件冒泡
iv.preventDefault()方法 阻止默认行为
b)IE中事件对象
i.type
ii.srcElement
iii.cancelBubble属性
iv.returnValue属性
4、跨浏览器（能力检测DOM2-->IE-->DOM0）
a)注意：
i.element['on'+type]=handler;
ii.方法判断的时候写成属性的形式。
iii.IE8以下window.event
var eventUtil = {
	addHandler: function(element, type, handler) {
		if (element.addEventListener) {
			element.addEventListener(type, handler, false);
		} else if (element.attachEvent) {
			element.attachEvent('on' + type, handler);
		} else {
			element['on' + type] = handler;
		}
	},
	removeHandler: function(element, type, handler) {
		if (element.removeEventListener) {
			element.removeEventListener(type, handler, false);
		} else if (element.detachEvent) {
			element.detachEvent('on' + type, handler);
		} else {
			element['on' + type] = null;
		}
	},
	getEvent: function(event) {
		return event ? event : window.event;
	},
	getType: function(event) {
		return event.type;
	},
	getElement: function(event) {
		return event.target || event.srcElement;
	},
	preventDefault: function(event) {
		if (event.preventDefault) {
			event.preventDefault();
		} else {
			event.returnValue = false;
		}
	},
	stopPropagation: function(event) {
		if (event.stopPropagation) {
			event.stopPropagation();
		} else {
			event.cancelBubble = true;
		}
	}
}
5、事件类型
a)QQ面板拖拽效果&抽奖系统

1、给一个元素添加多个事件处理程序，各浏览器的触发顺序？
2、支持IE事件处理程序的浏览器是IE和OPERA?
3、复习疯狂js的相关内容
4、事件在参数列表中可以写成event吗？