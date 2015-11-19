第三章 小结
---------------
`getElementById`

`getElementsByTagName(节点标签名)`返回数组

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

