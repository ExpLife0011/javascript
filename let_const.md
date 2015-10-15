# let 和 const

> 建议使用 let 和 const 代替 var

## let

let用于声明变量

### 块级作用域(大括号)

	'use strict'
	
	{
		let a = 1
		var b = 2
	}
	console.log(a) // a is not defined
	console.log(b)

### 不存在变量提升

	'use strict'
	
	if (true) {
		console.log(a)
		console.log(b) // b is not defined
		
		var a = 1
		let b = 2
	}

### 相同作用域内，不允许重复声明

	'use strict'
	
	let a = 1;
	let a = 2; // Identifier 'a' has already been declared
	
	if (true) {
		let a = 3; // 可以在这声明
	}

### 暂时性死区

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响

ES6明确规定，如果区块中存在 let 和 const 命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些命令，就会报错

	'use strict'
	
	var a = 1
	
	if (true) {
		a = 2 // a is not defined
		let a = 2
	}

## const

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
