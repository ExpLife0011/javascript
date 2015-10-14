# 变量

变量的名称，或称为标识符，需要遵守一定的规则。在JavaScript语言中，一个标识符必须以字母、下划线（_）或者美元（$）符号开头；后续的字符可以包含数字（0-9）。因为JavaScript语言是区分大小写的，这里所指的字母可以是（大写的）“A”到字母“Z”和（小写的）“a”到“z”。

从JavaScript 1.5版开始，你可以使用 ISO 8859-1 或 Unicode 编码的字符作标识符，例如å和ü。你也可以使用\uXXXX字样的转义序列 Unicode escape sequences作标识符。

## 声明

你可以用以下两种方式声明变量：

* 使用关键词 var。例如，var x = 42。这个语法可以同时用来声明局部和全局变量。
* 直接赋值。例如，x = 42。这样就声明了一个全局变量并会导致JavaScript编译时产生一个严格警告。因而你应避免使用这种非常规格式。

声明时未赋初值的变量，值会被设定为undefined。

## 变量的作用域

在所有函数之外声明的变量，叫做全局变量，因为它可被当前文档中的其他代码所访问。全局变量实际上是全局对象的属性。在函数内部声明的变量，叫做局部变量，因为它只能在该函数内部访问。

JavaScript没有语句块作用域；相反，语句块中声明的变量将成为语句块所在代码段的局部变量。

    if (true) {
      var x = 5;
    }
    console.log(x); // 5

## 变量声明提升

JavaScript 变量的另一特别之处在于，你可以引用稍后声明的变量，而不会引发异常。这一概念称为变量声明提升(hoisting)；JavaScript 变量感觉上是被“举起”或提升到了所有函数和语句之前。但是，未被初始化的变量仍将返回 undefined 值。

## ES6 新增：let 和 const

### let

let用于声明变量

#### 块级作用域(大括号)

	'use strict'
	
	{
		let a = 1
		var b = 2
	}
	console.log(a) // a is not defined
	console.log(b)

#### 不存在变量提升

	'use strict'
	
	if (true) {
		console.log(a)
		console.log(b) // b is not defined
		
		var a = 1
		let b = 2
	}

#### 相同作用域内，不允许重复声明

	'use strict'
	
	let a = 1;
	let a = 2; // Identifier 'a' has already been declared
	
	if (true) {
		let a = 3; // 可以在这声明
	}

#### 暂时性死区

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响

ES6明确规定，如果区块中存在 let 和 const 命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些命令，就会报错

	'use strict'
	
	var a = 1
	
	if (true) {
		a = 2 // a is not defined
		let a = 2
	}

### const

const用于声明常量，一旦声明，常量的值就不能改变，常量一般全大写+下划线。特性与let一样

	(1) 块级作用域(大括号)
	
	(2) 不存在提升现象
	
	(3) 相同作用域内，不允许重复声明
	
	(4) 暂时性死区

不可变动的引用使用const，可变动的引用使用 let

	const a = 1;
	let count = 1;
	  if (a > 0) {
	    count += 1;
	  }

## 块级作用域

在JavaScript语言中，所有全局变量都是全局对象的属性。但ES6规定，let、const、class声明的全局变量，不属于全局对象的属性

	'use strict'
	
	let a = 1
	console.log(global.a) // undefined
