# Number

## 数字类型

JavaScript内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相等的，而且1加上1.0得到的还是一个整数，不会像有些语言那样变成小数。

    1 === 1.0 // true
    1 + 1.0 // 2

## 包装对象

    new Number(value)
    
如果参数无法被转换为数字，则返回 NaN。

在非构造器上下文中 (如：没有 new 操作符)，Number 能被用来执行类型转换。

## 与数值相关的全局方法

### parseInt()

parseInt方法可以将字符串或小数转化为整数。如果字符串头部有空格，空格会被自动去除。

    parseInt('123') // 123
    parseInt(1.23) // 1
    parseInt('   81') // 81

将字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转化为数字的字符，就不再进行下去，返回已经转好的部分。

    parseInt('8a') // 8
    parseInt('12**') // 12
    parseInt('12.34') // 12
    parseInt('0xf00') // 3840

如果字符串的第一个字符不能转化为数字（正负号除外），返回NaN。

    parseInt('abc') // NaN
    parseInt('.3') // NaN
    parseInt('') // NaN

parseInt方法还可以接受第二个参数（2到36之间），表示被解析的值的进制。

    parseInt(1000, 2) // 8
    parseInt(1000, 6) // 216
    parseInt(1000, 8) // 512

如果第二个参数不是数值，会被自动转为一个整数。通过，这个整数只有在2到36之间，才能得到有意义的结果，超出这个范围，则返回NaN。如果第二个参数是0、undefined和null，则直接忽略。

    parseInt(10, 37) // NaN
    parseInt(10, 1) // NaN
    parseInt(10, 0) // 10
    parseInt(10, null) // 10
    parseInt(10, undefined) // 10

如果第一个参数为字符串，且以0x或0X开头，而第二个参数省略或为0，则parseInt自动将第二个参数设为16。

### parseFloat()

## Number对象的属性

（1）Number.POSITIVE_INFINITY

表示正的无限，指向关键字Infinity。

（2）Number.NEGATIVE_INFINITY

表示负的无限，指向-Infinity。

（3）Number.NaN

表示非数值，指向NaN。

（4）Number.MAX_VALUE

表示最大的正数，相应的，最小的负数为-Number.MAX_VALUE。

（5）Number.MIN_VALUE

表示最小的正数（即最接近0的正数，在64位浮点数体系中为5e-324），相应的，最接近0的负数为-Number.MIN_VALUE。

## Number对象实例的方法

### Number.prototype.toString()

Number对象部署了单独的toString方法，可以接受一个参数，表示将一个数字转化成某个进制的字符串。

    (10).toString() // "10"
    (10).toString(2) // "1010"
    (10).toString(8) // "12"
    (10).toString(16) // "a"

之所以要把10放在括号里，是为了表明10是一个单独的数值，后面的点表示调用对象属性。如果不加括号，这个点会被JavaScript引擎解释成小数点，从而报错。
    
    10.toString(2) 
    // SyntaxError: Unexpected token ILLEGAL

但是，在10后面加两个点，JavaScript会把第一个点理解成小数点（即10.0），把第二个点理解成调用对象属性，从而得到正确结果。

    10..toString(2) 
    // "1010"

### Number.prototype.toFixed()

将一个数转为指定位数的小数。

    (10).toFixed(2)
    // "10.00"
    // 10必须放在括号里，否则后面的点运算符会被处理小数点，而不是表示调用对象的方法。
    
    (10.005).toFixed(2)
    // "10.01"
    
### Number.prototype.toExponential()

将一个数转为科学计数法形式。
    
    (10).toExponential(1)
    // "1.0e+1"
    
    (1234).toExponential(1)
    // "1.2e+3"

toExponential方法的参数表示小数点后有效数字的位数，范围为0到20，超出这个范围，会抛出一个RangeError。

### Number.prototype.toPrecision()

将一个数转为指定位数的有效数字。

    (12.34).toPrecision(1)
    // "1e+1"
    
    (12.34).toPrecision(2)
    // "12"
    
    (12.34).toPrecision(3)
    // "12.3"
    
    (12.34).toPrecision(4)
    // "12.34"
    
    (12.34).toPrecision(5)
    // "12.340"