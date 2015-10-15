# 获取元素

## 获取元素的所有方法

	getElementById (兼容性：>=5.5)
	
	getElementsByTagName (兼容性：>=5.5)
	
	getElementsByClassName (兼容性：>=9.0)
	
	getElementsByName (有兼容性问题)

	querySelector (兼容性：>=IE8)
	
	querySelectorAll (兼容性：>=IE8)

## 说明

### getElementsByClassName 

获取所有 class 同时包括 'red' 和 'test' 的元素.

	document.getElementsByClassName('red test');

### getElementsByName

getElementsByName 有兼容性问题。在 IE & Opera 中，id 同名也会返回

如果元素不支持 name 也可以被返回

### querySelector

包含一个或是多个 CSS 选择器 ，多个则以逗号分隔

如果没有找到匹配元素，则返回 null，否则找到多个匹配元素，则返回第一个匹配到的元素

如果选择器是一个 ID，并且这个 ID 在文档中错误地使用了多次，那么返回第一个匹配该 ID 的元素

如果指定的选择器不合法，则抛出 SYNTAX_ERR 异常

不能包含 CSS伪元素（不是伪类）

如果要匹配的ID或选择器不符合 CSS 语法（比如不恰当地使用了冒号或者空格），你必须用反斜杠将这些字符转义。由于 JavaScript 中，反斜杠是转义字符，所以当你输入一个文本串时，你必须将它转义两次（一次是为 JavaScript 字符串转义，另一次是为 querySelector 转义）

	<div id="foo\bar"></div>
	<div id="foo:bar"></div>
	
	<script>
	  console.log('#foo\bar')               // "#fooar"
	  document.querySelector('#foo\bar')    // 不匹配任何元素
	
	  console.log('#foo\\bar')              // "#foo\bar"
	  console.log('#foo\\\\bar')            // "#foo\\bar"
	  document.querySelector('#foo\\\\bar') // 匹配第一个div
	
	  document.querySelector('#foo:bar')    // 不匹配任何元素
	  document.querySelector('#foo\\:bar')  // 匹配第二个div

## 建议

如果要兼容到 IE6，只能使用下面两个方法

	getElementById (兼容性：>=5.5)
	
	getElementsByTagName (兼容性：>=5.5)

如果兼容到 IE8，最好使用下面两个方法

	querySelector (兼容性：>=IE8)
	
	querySelectorAll (兼容性：>=IE8)
