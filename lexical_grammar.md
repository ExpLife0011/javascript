# 词法文法

## Control characters

## White space

## Line terminators

## Comments

## Keywords

## 直接量

    // Null直接量
    null
    
    // 布尔直接量
    true
    false
    
    // 数字直接量
    
    
    
    // 对象直接量
    
    var o = { a: "foo", b: "bar", c: 42 };
    
    // shorthand notation. New in ES6
    var a = "foo", b = "bar", c = 42;
    var o = {a, b, c};
    // instead of
    var o = { a: a, b: b, c: c };
    
    // 数组直接量
    
    [1954, 1974, 1990, 2014]
    
    // 字符串直接量
    
    'foo'
    "bar"
    
    // 正则表达式直接量
    
    /ab+c/g
    
    // 模板直接量
    `string text`
    
    `string text line 1
     string text line 2`
    
    `string text ${expression} string text`
    
    tag `string text ${expression} string text`

---

## 分号自动插入

JavaScript 使用分号`;`将语句分隔开，但是分号是可选的。如果省略分号，JavaScript 的处理规则是：

> 如果当前语句和下一行语句无法合并解析，JavaScript 则在第一行后填补分号。

这是通用规则，但有两个例外：

* return、break、continue
* ++、--

**return、break、continue**

    return
    true

JavaScript会解析成：

    return; true;
    
而本意是：

    return true;

**++、--**

    x
    ++
    y

JavaScript会解析成：

    x; ++y;
    
而不是：

    x++; y;

---