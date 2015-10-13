# 词法文法

## Control characters

## White space

## Line terminators

## Comments

## Keywords

## Literals

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