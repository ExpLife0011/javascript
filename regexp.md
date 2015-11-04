# 正则表达式

## 定义

**(1) 使用用字面量**

    var regex = /xyz/;
    var regex = /xyz/i;

**(2) 也可以用构造函数**

    var regex = new RegExp('xyz');
    var regex = new RegExp('xyz', "i"); // 第二个参数表示修饰符
    
