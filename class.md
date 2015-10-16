# 类

ES6 提供了更接近传统语言的写法，引入了Class（类）。但需要注意的是，这并不是说：JavaScript 从此变得像其它基于类的面向对象语言一样，有了一种全新的继承模型。JavaScript 中的类只是 JavaScript 现有的、基于原型的继承模型的一种语法包装（语法糖），它能让我们用更简洁明了的语法实现继承。

类体中的代码都强制在严格模式中执行，即便没有写 "use strict"。

## 定义类

    'use strict';
    
    class A {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }
      
      say() {
        return this.name + ', ' + this.age;
      }
    }

**类表达式**

类表达式是定义类的另外一种方式，就像函数表达式一样，在类表达式中，类名是可有可无的。如果定义了类名，则该类名只有在类体内部才能访问到。

    // 匿名类表达式
    var Polygon = class {
      constructor(height, width) {
        this.height = height;
        this.width = width;
      }
    };
    
    // 命名类表达式
    var Polygon = class Polygon {
      constructor(height, width) {
        this.height = height;
        this.width = width;
      }
    };

ES6 中的类实际上就是个函数

    typeof A // function

## 类成员

类成员包括类构造器和类方法（包括静态方法和实例方法）。

**构造器**

constructor 方法是一个特殊的类方法，它既不是静态方法也不是实例方法，它仅在实例化一个类的时候被调用。一个类只能拥有一个名为 constructor 的方法，否则会抛出 SyntaxError 异常。

在子类的构造器中可以使用 super 关键字调用父类的构造器。

**静态方法**

`static`关键字用来定义类的静态方法。 静态方法是指那些不需要对类进行实例化，使用类名就可以直接访问的方法。静态方法经常用来作为工具函数。

    class Point {
        constructor(x, y) {
            this.x = x;
            this.y = y;
        }
    
        static distance(a, b) {
            const dx = a.x - b.x;
            const dy = a.y - b.y;
    
            return Math.sqrt(dx*dx + dy*dy);
        }
    }
    
    const p1 = new Point(5, 5);
    const p2 = new Point(10, 10);
    
    console.log(Point.distance(p1, p2));

## 变量提升

类声明和函数声明不同的一点是，函数声明存在变量提升现象，而类声明不会。也就是说，你必须先声明类，然后才能使用它，否则代码会抛出 ReferenceError 异常。


    
