第三章 小结
---------------
`getElementById`

`getElementsByTagName(节点标签名)`返回数组 如果使用通配符==*==，则返回所有 ==元素节点==

`getElementsByClassName(节点class名)`返回数组

`getAttribute(节点属性)`

`setAttribute(属性，值)`


第四章 小结
--------------
`childNodes` 返回数组


`nodeType` 返回 1（元素节点）、2（文本节点）、3（属性节点）

`nodeValue` 

`firstChild` = childNodes[0]

`lastChild` = childNodes[节点.childNodes.length - 1]

第五章 小结
--------------
"javascript:" 伪协议：一种非标准化的协议
`<a href="javascript:popUp(...);"> Example</a>`

**平稳退化：**用户禁用了浏览器的javascript功能时


**分离javascript**分离到外部文件中

**向后兼容**使老牌、不支持更多功能的浏览器能够正常访问

尽量少访问DOM和尽量减少标记

合并脚本，减少请求次数

压缩脚本，精简版本的文件名加上 **min**
`<script src="scripts/scriptName.min.js"></script>`

第六章
---------------
**共享onload事件：**需要绑定的函数较多时，可以一个一个添加（弹性十足）

```javascript
	function addLoadEvent(func){
		var oldonload = window.onload;
		if(typeof oldonload != "function") {
			window.onload = func;
		}else {
			window.onload = function() {
				oldonload();
				func();
			}
		}
	}
	
	//如果想要添加函数可以直接添加到队列里面
	//addLoadEvent(func1)  addLoadEvent(func2)
```

==往后插入一个节点==

```javascript
	function insertAfter(newElement, targetElement) {
		var parentNode = targetElement.parentNode;
		if (parentNode.lastChild == targetElement) {
			parentNode.appendChild(newElement);
		}else {
			targetElement.insertBefore(newElement, targetElement.nextSibling);
		}
}
```

第七章
------------

`document.write()`

`innerHTML`

`createElement`

`createTextNode`

`appendChild`

`insertBefore`

`insertAfter`

==创建节点对象后将这些DocumentFragment对象插入文档的节点树==

第八章
-----------
==缩略语列表==  文档中的缩略语`<abbr title="w  w  w">W3C</abbr>`

```
<dl>
	<dt>W3C</dt>
	<dd>lalala</dd>
</dl>
```

为每段文献节选生成一个==文献来源链接==：
文献一般加上 cite="http://www.w3.org/DOM/" 属性

```javascript
	<sup>		//sup显示 上标 的效果
		<a>source</a>
	</sup>	
```

将文档所支持的快捷键显示为一份==快捷键清单==：
可以为个别标签添加 accesskey="1" 属性

第九章（DOM）
---------------

通过==style==属性改变文档样式

- 根据元素在节点树里面的位置设置他们的样式
（通过子元素  父元素 查找对应元素，并设定样式）
- 遍历一个节点集合设置有关元素的样式
（通过==*==可以得到所有 ==元素文本==）
- 在事件发生时设置有关元素的样式
（事件对象）

第十章（动画）
---------
"动画"：随时间变化而改变某个元素在浏览器窗口里的显示位置

```javascript
	function moveElement (elementID, final_x, final_y, interval) {
		//检查是否支持方法
		if (!document.getElementById) return false;
		if (!document.getElementById(elementID)) return false;

		var elem = document.getElementById(elementID);
		if (elem.movement) {			//防止来回移动，在下一下移动触发时清除movement
			clearTimeout(elem.movement);
		};
		if (!elem.style.left) {
			elem.style.left = "0px";
		}
		if (!elem.style.top) {
			elem.style.top = "0px";
		};
		var xpos = parseInt(elem.style.left);
		var ypos = parseInt(elem.style.top);
		if (xpos == final_x && ypos == final_y) {
			return true;
		}

		var dlist = 0;
		if (xpos < final_x) {
			dlist = Math.ceil((final_x-xpos)/10);
			xpos += dlist;
		}
		if (xpos > final_x) {
			dlist = Math.ceil((xpos-final_x)/10);
			xpos -= dlist;
		}
		if (ypos < final_y) {
			dlist = Math.ceil((final_y-ypos)/10);
			ypos += dlist;
		}
		if (ypos > final_y) {
			dlist = Math.ceil((ypos-final_y)/10);
			ypos -= dlist;
		}
		elem.style.left = xpos + "px";
		elem.style.top = ypos + "px";
		var repeat = "moveElement('" + elementID + "'," + final_x +","+ final_y+"," + interval + ")";	//参数为字符串，而且加括号
		elem.movement = setTimeout(repeat, interval);	//将setTime作为属性赋给elem，然后清除的时候可以清除属性，防止作为全局变量时无法定时清除，作为局部变量时不能全局
	}
```