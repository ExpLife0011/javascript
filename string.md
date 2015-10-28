# String

## 字符串类型

JavaScript的字符串类型用于表示文本数据。它是一组16位的无符号整数值的“元素”。在字符串中的每个元素占据了字符串的位置。第一个元素的索引为0，下一个是索引1，依此类推。字符串的长度是它的元素的数量。

不同于类 C 语言，JavaScript 字符串是不可更改的。这意味着字符串一旦被创建，就不能被修改。但是，可以基于对原始字符串的操作来创建新的字符串。

和其他语言不同，javascript不区分单引号和双引号字符串，所以不论是单引号还是双引号的字符串，转义字符都能运行。

## 包装对象

    new String(thing)
    
在非构造器上下文中 (如：没有 new 操作符)，String 能被用来执行类型转换。