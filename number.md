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