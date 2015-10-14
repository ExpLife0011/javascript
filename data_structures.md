# 数据结构

编程语言都具有内建的数据结构，它们可以用来构建其他的数据结构。

## 动态类型

JavaScript 是一种弱类型或者说动态语言。这意味着你不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。这也意味着你可以使用同一个变量保存不同类型的数据

    var foo = 42;    // foo is a Number now
    var foo = "bar"; // foo is a String now
    var foo = true;  // foo is a Boolean now

## 数据类型

最新的 ECMAScript 标准定义了 7 种数据类型

    6种原始类型
    
        Boolean
        Null
        Undefined
        Number
        String
        Symbol (ECMAScript 6 新增)
        
    和 
    
        Object

## 原始值

除 Object 以外的所有类型都是不可变的（值本身无法被改变）。例如，与 C 语言不同，JavaScript 中字符串是不可变的（译注：如，JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变）。我们称这些类型的值为“原始值”。

 JavaScript 是大小写敏感的，因此 true、false、null、undefined 区分大小写，只能是全小写。

### 布尔类型

布尔表示一个逻辑实体，可以有两个值：true 和 false。区分大小写。

### Null 类型

Null 类型只有一个值： null。区分大小写。

### Undefined 类型

一个没有被赋值的变量会有个默认值 undefined。区分大小写。

### 数字类型

根据 ECMAScript 标准，JavaScript 中只有一种数字类型：基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(253 -1) 到 253 -1）。

### 字符串类型

JavaScript的字符串类型用于表示文本数据。它是一组16位的无符号整数值的“元素”。在字符串中的每个元素占据了字符串的位置。第一个元素的索引为0，下一个是索引1，依此类推。字符串的长度是它的元素的数量。

不同于类 C 语言，JavaScript 字符串是不可更改的。这意味着字符串一旦被创建，就不能被修改。但是，可以基于对原始字符串的操作来创建新的字符串。

### 符号类型

符号类型在 ECMAScript 6 中被引入Javascript。符号类型是唯一的并且是不可修改的, 并且也可以用来作为Object的key的值。

## 对象

在计算机科学中, 对象是指内存中的可以被 identifier引用的一块区域。
