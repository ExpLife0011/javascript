# 语句和声明

## 流程控制

### 语句块

    {
      statement_1;
      statement_2;
      ...
      statement_n;
    }

### break、continue

    break [label];
    continue [label];
    
### 空语句

空语句用来表明没有语句, 尽管JavaScript语法希望有语句会被执行

    ;

### if...else

注意，在JavaScript中没有 elseif (一个单词)关键字

    if (condition1)
       statement1
    else if (condition2)
       statement2
    else if (condition3)
       statement3
    ...
    else
       statementN

### switch

    switch (expression) {
      case value1:
        // 当 expression 的结果与 value1 匹配时，从此处开始执行
        statements1；
        [break;]
      case value2:
        // 当 expression 的结果与 value2 匹配时，从此处开始执行
        statements2;
        [break;]
      ...
      case valueN:
        // 当 expression 的结果与 valueN 匹配时，从此处开始执行
        statementsN;
        [break;]
      default:
        // 如果 expression 与上面的 value 值都不匹配时，执行此处的语句
        statements_def;
        [break;]
    }

### throw

throw 语句用来抛出用户自定义异常。当前函数的执行将会被中止（throw之后的语句将会得不到执行），接着执行流程会转移到第一个 catch 语句块。如果在调用方函数中没有任何catch语句块，那么程序将会被中止。

    throw "Error2"; // 抛出了一个值为字符串的异常
    throw 42;       // 抛出了一个值为整数42的异常
    throw true;     // 抛出了一个值为true的异常

### try...catch

无论是否有异常抛出或捕获这些语句都将执行finally。

    try {
       try_statements
    }
    [catch (exception_var_1 if condition_1) { // non-standard
       catch_statements_1
    }]
    ...
    [catch (exception_var_2) {
       catch_statements_2
    }]
    [finally {
       finally_statements
    }]


## 声明

var、let、const，参考http://www.javascript-zh.com/variable_const.html

## 函数和类

在直接量中没有函数直接量和类直接量，原来在这里。

### function

### function*

### return

### class

## 循环

### do...while

### for

### for...in

以任意序迭代一个对象的可枚举属性。每个不同的属性，语句都会被执行一次。

    for (variable in object) {
      ...
    }

### for...of

ES6 新增。注意与 for...in 的区别

    let arr = [ 3, 5, 7 ];
    arr.foo = "hello";
    
    for (let i in arr) {
       console.log(i); // logs "0", "1", "2", "foo"
    }
    
    for (let i of arr) {
       console.log(i); // logs "3", "5", "7"
    }

### while

## 其他

### debugger

调用任何一个可用的调试器，如果没有调试器可用，则该语句没有任何效果。

    function potentiallyBuggyCode() {
        debugger;
        // do potentially buggy stuff to examine, step through, etc.
    }

当debugger被调用时, 执行暂停在 debugger 语句的位置。就像在脚本源代码中的断点一样。

### export

ES6 新增。

### import

ES6 新增。

### label

标记语句（labeled statement）可以和 break 或 continue 语句一起使用。标记就是在一条语句前面加个可以引用的标识符（identifier）。

    label :
       statement

### with

不推荐使用。