# Number

## 数字类型

根据 ECMAScript 标准，JavaScript 中只有一种数字类型：基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(253 -1) 到 253 -1）。

## 包装对象

    new Number(value)
    
如果参数无法被转换为数字，则返回 NaN。

在非构造器上下文中 (如：没有 new 操作符)，Number 能被用来执行类型转换。