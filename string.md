# String

## 字符串类型

字符串就是若干个排在一起的字符。在字符串中的每个元素占据了字符串的位置。第一个元素的索引为0，下一个是索引1，依此类推。字符串的长度是它的元素的数量。

不同于类 C 语言，JavaScript 字符串是不可更改的。这意味着字符串一旦被创建，就不能被修改。但是，可以基于对原始字符串的操作来创建新的字符串。

和其他语言不同，javascript不区分单引号和双引号字符串，所以不论是单引号还是双引号的字符串，转义字符都能运行。

## 多行字符串

字符串默认只能写在一行内，分成多行将会报错。

    'a
    b
    c'
    // SyntaxError: Unexpected token ILLEGAL

如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠。

    var longString = "Long \
    long \
    long \
    string";
    
    longString
    // "Long long long string"

但是，这种写法有两个注意点，首先，它是ECMAScript 5新添加的，老式浏览器（如IE 8）不支持，其次，反斜杠的后面必须是换行符，而不能有其他字符（比如空格），否则会报错。

连接运算符（+）可以连接多个单行字符串，用来模拟多行字符串。

    var longString = 'Long '
      + 'long '
      + 'long '
      + 'string';

## 字符串与数组

字符串可以被视为字符数组，可以使用数组的方括号运算符，用来返回某个位置的字符，但无法改变字符串之中的单个字符。

length属性返回字符串的长度，该属性也是无法改变的。

字符串与数组的关系仅此而已。

## 字符集

JavaScript使用Unicode字符集，使用16位（即2个字节）的UTF-16格式储存。也就是说，JavaScript的单位字符长度固定为2个字节。

对于U+0000到U+FFFF之间的字符，一个16位就够了（即2个字节）；对于U+10000到U+10FFFF之间的字符，就需要2个16位（即4个字节），而且前两个字节在0xD800到0xDBFF之间，后两个字节在0xDC00到0xDFFF之间。浏览器会正确将这四个字节识别为一个字符，但是JavaScript内部的字符长度总是固定为16位，会把这四个字节视为两个字符。

    // 把字符串变成数组
    function getSymbols(string) {
        var length = string.length;
        var index = -1;
        var output = [];
        var character;
        var charCode;
        while (++index < length) {
            character = string.charAt(index);
            charCode = character.charCodeAt(0);
            if (charCode >= 0xD800 && charCode <= 0xDBFF) {
                output.push(character + string.charAt(++index));
            } else {
                output.push(character);
            }
        }
        return output;
    }

## 包装对象

    new String(thing)
    
在非构造器上下文中 (如：没有 new 操作符)，String 能被用来执行类型转换。

## 字符串函数

### String.fromCharCode()

根据Unicode编码，生成一个字符串。

    String.fromCharCode(104, 101, 108, 108, 111)
    // "hello"
    
    String.fromCharCode(0x20BB7)
    // "ஷ"
    
    String.fromCharCode(0xD842, 0xDFB7)
    // "𐮷"

### length属性

返回字符串的长度。

### charAt()

返回一个字符串的给定位置的字符。

### charCodeAt()

返回给定位置字符的Unicode编码（十进制表示）。

需要注意的是，charCodeAt方法返回的Unicode编码不大于65536（0xFFFF），也就是说，只返回两个字节。因此如果遇到Unicode大于65536的字符（根据UTF-16的编码规则，第一个字节在U+D800到U+DBFF之间），就必需连续使用两次charCodeAt，不仅读入charCodeAt(i)，还要读入charCodeAt(i+1)，将两个16字节放在一起，才能得到准确的字符。

### concat()

用于连接两个字符串。

    var s1 = "abc";
    var s2 = "def";
    
    s1.concat(s2) // "abcdef"
    s1 // "abc"
    
可以接受多个字符串。

    "a".concat("b","c")
    // "abc"

一般来说，字符串连接运算还是应该使用加号（+）运算符。

### substring()、substr()、slice()

三个函数都是返回一个字符串的子串。

它们都可以接受一个或两个参数。

第一个参数都是子字符串的开始位置。

如果省略第二个参数，则表示子字符串一直持续到原字符串结束。

第二个参数对于slice和substring方法，表示子字符串的结束位置；对于substr，表示子字符串的长度。

如果第一个参数大于第二个参数，slice和substring会自动调换参数位置。而slice方法并不会自动调换参数位置，而是返回一个空字符串。

如果参数为负，对于slice方法，表示字符位置从尾部开始计算。对于substring方法，会自动将负数转为0。对于substr方法，负数出现在第一个参数，表示从尾部开始计算的字符位置；负数出现在第二个参数，将被转为0。

### 