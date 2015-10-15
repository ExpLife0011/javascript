# 解构赋值

## 数组的解构赋值

	var [a, b, c] = [1, 2, 3]
	a // 1
	b // 2
	c // 3
	
	let [foo, [[bar], baz]] = [1, [[2], 3]]
	foo // 1
	bar // 2
	baz // 3
	
	let [,,third] = ["foo", "bar", "baz"]
	third // "baz"
	
	let [x, , y] = [1, 2, 3]
	x // 1
	y // 3
	
	let [head, ...tail] = [1, 2, 3, 4]
	head // 1
	tail // [2, 3, 4]
	
	不完全解构
	let [x, y] = [1, 2, 3]
	x // 1
	y // 2
	
	var [bar, foo] = [1]
	bar // 1
	foo // undefined
	
	指定默认值
	var [x, y='b'] = ['a']
	// x='a', y='b'
	var [x = 1] = [undefined]
	x // 1
	[x, y='b'] = ['a', undefined]
	// x='a', y='b'

## 对象的解构赋值

对象的解构与数组有一个重要的不同，变量必须与属性同名

	var { foo, bar } = { foo: "aaa", bar: "bbb" }
	foo // "aaa"
	bar // "bbb"

如果变量名与属性名不一致，必须写成下面这样

	var { foo: baz } = { foo: "aaa", bar: "bbb" }
	baz // "aaa"
	
	let obj = { first: 'hello', last: 'world' }
	let { first: f, last: l } = obj
	f // 'hello'
	l // 'world'

和数组一样，解构也可以用于嵌套结构的对象

	var obj = {
	  p: [
	    "Hello",
	    { y: "World" }
	  ]
	}
	
	var { p: [x, { y }] } = obj
	x // "Hello"
	y // "World"

对象的解构也可以指定默认值

	var {x = 3} = {}
	x // 3
	
	var {x, y = 5} = {x: 1}
	console.log(x, y) // 1, 5
	
	var { message: msg = "Something went wrong" } = {}
	console.log(msg); // "Something went wrong"

默认值生效的条件是，对象的属性值严格等于undefined

	var {x = 3} = {x: undefined}
	x // 3
	
	var {x = 3} = {x: null}
	x // null

如果要将一个已经声明的变量用于解构赋值，必须非常小心

	var x
	{x} = {x:1}
	// SyntaxError: syntax error

因为JavaScript引擎会将{x}理解成一个代码块，从而发生语法错误。只有不将大括号写在行首，避免JavaScript将其解释为代码块，才能解决这个问题

	// 正确的写法
	({x} = {x:1})

## 字符串的解构赋值

	const [a, b, c, d, e] = 'hello'
	a // "h"
	b // "e"
	c // "l"
	d // "l"
	e // "o"

类似数组的对象都有一个length属性

	let {length : len} = 'hello'
	len // 5

## 函数参数的解构赋值

	function add([x, y]){
	  return x + y
	}
	
	add([1, 2]) // 3

函数参数的解构也可以使用默认值

	function move({x = 0, y = 0} = {}) {
	  return [x, y]
	}
	
	move({x: 3, y: 8}) // [3, 8]
	move({x: 3}) // [3, 0]
	move({}) // [0, 0]
	move() // [0, 0]
