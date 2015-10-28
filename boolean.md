# Boolean

## 原始值

布尔表示一个逻辑实体，可以有两个值：true 和 false。区分大小写。

## 包装对象

Boolean对象是一个包装了布尔值的对象。

    new Boolean([value])
    
如果Boolean构造函数的参数不是一个布尔值，则该参数会被转换成一个布尔值。如果参数是 0, -0, null, false, NaN, undefined, 或者空字符串 ("")，生成的Boolean对象的值为false。其他任何值，包括任何对象或者字符串"false"，都会创建一个值为true的Boolean对象。

不要将原始值true false 和值为true false的Boolean对象相混淆。

任何值为 undefined 或者 null的对象，包括值为false的Boolean对象，在条件语句中,其值都将作为 true 来判断。