# 模块

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言规格的层面上，实现了模块功能，而且实现得相当简单，完全可以取代现有的 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

## 模块的严格模式

ES6 的模块自动采用严格模式，不管有没有在模块头部加上"use strict"。

严格模式主要有以下限制：

	变量必须声明后再使用
	函数的参数不能有同名属性，否则报错
	不能使用with语句
	不能对只读属性赋值，否则报错
	不能使用前缀0表示八进制数，否则报错
	不能删除不可删除的属性，否则报错
	不能删除变量delete prop，会报错，只能删除属性delete global[prop]
	eval不会在它的外层作用域引入变量
	eval和arguments不能被重新赋值
	arguments不会自动反映函数参数的变化
	不能使用arguments.callee
	不能使用arguments.caller
	禁止this指向全局对象
	不能使用fn.caller和fn.arguments获取函数调用的堆栈
	增加了保留字（比如protected、static和interface）

上面这些限制，模块都必须遵守。


## export 和 import

模块功能主要由两个命令构成：`export`和`import`。

`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

### export

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果希望外部能够读取模块内部的某个变量，就必须使用`export`关键字输出该变量。

	export var firstName = 'Michael';
	export var lastName = 'Jackson';
	export var year = 1958;
	
	// 或
	var firstName = 'Michael'
	var lastName = 'Jackson'
	var year = 1958
	
	export {firstName, lastName, year} // export命令后面，使用大括号指定所要输出的一组变量,它与前一种写法是等价的

`export`命令除了输出变量，还可以输出函数或类。

通常情况下，`export`输出的变量就是本来的名字，但是可以使用`as`关键字重命名。

	function v1() { ... }
	function v2() { ... }
	
	export {
	  v1 as streamV1,
	  v2 as streamV2,
	  v2 as streamLatestVersion // v2可以用不同的名字输出两次
	}

`export`命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错。

### import

	import {firstName, lastName, year} from './profile';
	
	function setName(element) {
	  element.textContent = firstName + ' ' + lastName;
	}

`import`大括号里面的变量名，必须与被导入模块（profile.js）对外接口的名称相同。

如果想为输入的变量重新取一个名字，`import`命令要使用`as`关键字，将输入的变量重命名。

	import { lastName as surname } from './profile';

ES6 支持多重加载，即所加载的模块中又加载其他模块。

除了指定加载某个输出值，还可以使用整体加载，即用星号（*）指定一个对象，所有输出值都加载在这个对象上面。

	import * as circle from './circle';
	
	console.log("圆面积：" + circle.area(4));
	console.log("圆周长：" + circle.circumference(14));

`module`命令可以取代`import`语句，达到整体输入模块的作用。

	module circle from './circle';
	
	console.log("圆面积：" + circle.area(4));
	console.log("圆周长：" + circle.circumference(14));

## export default 命令

`export default`命令，为模块指定默认输出。

	// export-default.js
	export default function () {
	  console.log('foo');
	}
	
	// 或者写成
	function foo() {
	  console.log('foo');
	}
	
	export default foo;

	// import-default.js
	import customName from './export-default'; // 不使用大括号
	customName(); // 'foo'

需要注意的是，这时import命令后面，不使用大括号。

显然，一个模块只能有一个默认输出，因此`export deault`命令只能使用一次。所以，import 命令后面才不用加大括号，因为只可能对应一个方法。

如果想在一条 import 语句中，同时输入默认方法和其他变量，可以写成下面这样。

	import customName, { otherMethod } from './export-default';

## 模块的继承

模块之间也可以继承。

假设有一个circleplus模块，继承了circle模块

	export * from 'circle';
	export var e = 2.71828182846;
	export default function(x) {
	    return Math.exp(x);
	}

`export *`，表示输出circle模块的所有属性和方法，export default命令定义模块的默认方法。