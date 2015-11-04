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

## 原始类型 & 原始值

除 Object 以外的所有类型都是不可变的（值本身无法被改变）。例如，与 C 语言不同，JavaScript 中字符串是不可变的（译注：如，JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变）。我们称这些类型的值为“原始值”。

 JavaScript 是大小写敏感的，因此 true、false、null、undefined 区分大小写，只能是全小写。

## 原始类型 & 包装对象

JavaScript原生提供的三个包装对象：String、Number、Boolean。