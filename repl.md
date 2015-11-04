# REPL环境

在命令行键入node命令，后面没有文件名，就进入一个Node.js的REPL环境（Read–eval–print loop，"读取-求值-输出"循环），可以直接运行各种JavaScript命令

    $ node
    > 1+1
    2
    >
    
如果使用参数 --use_strict，则REPL将在严格模式下运行

    node --use_strict
    
特殊变量下划线（_）表示上一个命令的返回结果

    > 1+1
    2
    > _+1
    3
    
在REPL中，如果运行一个表达式，会直接在命令行返回结果。如果运行一条语句，就不会有任何输出(输出undefined)，因为语句没有返回值。

    > x = 3
    3
    > var a = 3
    undefined
    >