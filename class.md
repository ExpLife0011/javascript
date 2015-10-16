# 类

ES6 提供了更接近传统语言的写法，引入了Class（类）。但需要注意的是，这并不是说：JavaScript 从此变得像其它基于类的面向对象语言一样，有了一种全新的继承模型。JavaScript 中的类只是 JavaScript 现有的、基于原型的继承模型的一种语法包装（语法糖），它能让我们用更简洁明了的语法实现继承。

类体中的代码都强制在严格模式中执行，即便没有写 "use strict"。

## 定义类

## 变量提升

类声明和函数声明不同的一点是，函数声明存在变量提升现象，而类声明不会。也就是说，你必须先声明类，然后才能使用它，否则代码会抛出 ReferenceError 异常。

## 类表达式

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
    
## 

类成员包括类构造器和类方法（包括静态方法和实例方法）。

### 构造器

