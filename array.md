# 数组

## 定义

**(1) 使用数组直接量**

    var arr = ['a', 'b', 'c'];

数组也可以先定义后赋值

    var arr = [];
    
    arr[0] = 'a';
    arr[1] = 'b';
    arr[2] = 'c';
    
    // 不能出现这样的(PHP可以)
    //arr[] = 'd';
    
任意一种类型的数据，都可以放入数组

    var arr = [
      {a: 1},
      [1, 2, 3],
      function() {return true;}
    ];
    
    arr[0] // Object {a: 1}
    arr[1] // [1, 2, 3]
    arr[2] // function (){return true;}
    
如果数组的元素还是数组，就形成了多维数组

    var a = [[1, 2], [3, 4]];
    a[0][1] // 2
    a[1][1] // 4

**(2) 使用 Array 构造函数**

    var a = new Array();
    a // []
    a.length // 0
    
    var a = new Array(1);
    a // [,]
    a.length // 1
    
    var a = new Array(2);
    a // [, ,]
    a.length // 2
    
    var a = new Array(1,2);
    a // [1,2]
    a.length // 2
    
没有参数时，返回一个空数组；使用一个参数时，返回一个指定长度的空数组；使用多个参数，返回一个指定成员的数组。所以，建议总是直接采用方括号创建数组。

## 没有元素的情况

没有元素不是指元素值为undefined，而是指此位置上没有任何元素。访问时因没有元素而返回undefined。

    // arr 和 arr2 完全等价
    var arr = [, , , ,];
    var arr2 = new Array(3);

与下面的不同
    
    // 有3个元素
    var arr3 = [undefined, undefined, undefined];

arr、arr2、arr3的长度相等。arr 和 arr2 完全等价，虽有长度，但位置上没有元素。arr3 有3个元素。

使用`delete`命令，就会出现位置上没有元素的情况。没有元素但是仍然有位置，所以`delete`命令不影响length属性。

## 数组元素的访问

对象有两种读取成员的方法：“点”结构（object.key）和方括号结构（object[key]）。但是，对于数字的键名，不能使用点结构，arr.0的写法不合法，因为单独的数字不能作为标识符（identifier）。如果给数组添加了属性，则可以用“点”访问属性。

## 数组与对象的关系

数组也属于对象

    // 数组只是一种特殊的对象
    typeof [1, 2, 3] // "object"

数组不用为每个元素指定键名，而对象的每个成员都必须指定键名。数组的键默认是按次序排列的整数（0，1，2...）。

对象以字符串来识别键名，非字符串的键名会被转为字符串。数组的键名其实也是字符串，所有的整数键名默认都会转为字符串。

    var arr = ['a', 'b', 'c'];
    
    arr['0'] // 'a'
    arr[0] // 'a'

## 为数组添加属性

由于数组本质上是对象的一种，所以我们可以为数组添加属性，但是这不影响length属性的值。

    var arr = ['a', 'b'];
    arr['c'] = 'c';
    arr.d = 'd';
    console.log(arr);
    console.log(arr.c); // c
    console.log(arr['c']); // c
    console.log(arr.d); // d
    console.log(arr['d']); // d

使用`for in`时，先输出元素，再输出添加的属性。

    var arr = ['a', 'b'];
    arr['e'] = 'e';
    arr[2] = 'd';
    arr['c'] = 'c';
    arr[3] = 'f';
    for (var i in arr) {
      console.log(arr[i]); // a, b, d, f, e, c
    }

## length 属性

数组的 length 属性是一个动态的值，等于键名中的最大整数加上1。

    var arr = ['a', 'b'];
    arr.length // 2
    
    arr[2] = 'c';
    arr.length // 3
    
    arr[9] = 'd';
    arr.length // 10
    
    arr[1000] = 'e';
    arr.length // 1001

数组的数字键不需要连续，length属性的值总是比最大的那个整数键大1。

length属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员会自动减少到length设置的值。

    var arr = [ 'a', 'b', 'c' ];
    arr.length // 3
    
    arr.length = 2;
    arr // ["a", "b"]
    
将数组清空的一个有效方法，就是将length属性设为0。

    var arr = [ 'a', 'b', 'c' ];
    
    arr.length = 0;
    arr // []
    
如果人为设置length大于当前元素个数，新增的位置上没有元素(仍然有位置)。

    var a = ['a'];
    
    a.length = 3;
    a // ["a", , ,] 长度为3

如果人为设置length为不合法的值，JavaScript会报错。

## 数组函数

    // 构造函数
    Array // 生成新的数组。见上文
    
    // 静态函数
    Array.isArray // 判断是否是数组。有一个参数
    
    // 实例函数
    valueOf // 返回数组本身。没有参数
    toString // 返回数组的字符串形式。没有参数
    push // 在数组的末端添加一个或多个元素，并返回添加后的数组的长度。
    pop // 用于删除数组的最后一个元素，并返回该元素。没有参数
    join // 以参数作为分隔符，将所有数组成员组成一个字符串返回。如果不提供参数，默认用逗号分隔。
    concat // 将新数组的成员，添加到原数组的尾部，然后返回一个新数组
    shift // 删除数组的第一个元素，并返回该元素。没有参数
    unshift // 在数组的第一个位置添加元素，并返回添加新元素后的数组长度。
    reverse // 颠倒数组中元素的顺序，返回改变后的原数组
    slice // 返回指定位置的数组成员组成的新数组，原数组不变。
    splice // 用于删除元素，并可以在被删除的位置添加入新的数组元素。它的返回值是被删除的元素。该方法会改变原数组。
    sort // 对数组元素进行排序，默认是按照字典顺序排序。排序后，原数组将被改变
    
    // ES5新增
    map // 对数组的所有成员依次调用一个函数，根据函数结果返回一个新数组
    forEach // 遍历数组的所有成员，执行某种操作。没有返回值
    filter // 依次对所有数组成员调用一个测试函数，返回结果为true的成员组成一个新数组返回。
    some // 对所有元素调用一个测试函数，只要有一个元素通过该测试，就返回true，否则返回false。
    every // 对所有元素调用一个测试函数，只有所有元素通过该测试，才返回true，否则返回false。
    reduce
    reduceRight
    indexOf // 返回给定元素在数组中第一次出现的位置，如果没有出现则返回-1
    lastIndexOf // 返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1。

### valueOf 和 toString

    var a = [1,2,3];
    a.valueOf()
    // [1,2,3]
    
    var a = [1,2,3,[4,5,6]];
    a.toString()
    // "1,2,3,4,5,6"

### push

    a.push("a") // 2
    a.push(true, {}) // 4

### concat

    ['hello'].concat(['world'])
    // ["hello", "world"]
    
    ['hello'].concat(['world'], ['!'])
    // ["hello", "world", "!"]
    
    [1, 2, 3].concat(4, 5, 6)
    // [1, 2, 3, 4, 5, 6]

### slice

它的第一个参数为起始位置（从0开始），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。

    var a = ["a","b","c"];
    
    a.slice(1,2) // ["b"]
    a.slice(1) // ["b", "c"]
    a.slice(0) // ["a","b","c"]
    a.slice(-2) // ["b", "c"]
    a.slice(4) // []
    a.slice(2, 6) // ["c"]
    a.slice(2, 1) // []

### splice

splice的第一个参数是删除的起始位置，第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素。

    var a = ["a","b","c","d","e","f"];
    
    a.splice(4,2,1,2)
    // ["e", "f"]
    
    a
    // ["a", "b", "c", "d", 1, 2]
    
如果只是单纯地插入元素，splice方法的第二个参数可以设为0

    var a = [1,1,1];
    
    a.splice(1,0,2)
    // []
    
    a
    // [1, 2, 1, 1]

如果只提供第一个参数，则实际上等同于将原数组在指定位置拆分成两个数组

    var a = [1,2,3,4];
    
    a.splice(2)
    // [3, 4]
    
    a
    // [1, 2]

### sort

    ["d","c","b","a"].sort()
    // ["a", "b", "c", "d"]
    
可以传入一个函数作为参数，表示按照自定义方法进行排序。该函数本身又接受两个参数，表示进行比较的两个元素。如果返回值大于0，表示第一个元素排在第二个元素后面；其他情况下，都是第一个元素排在第二个元素前面。

    [10111,1101,111].sort(function (a,b){
      return a-b;
    })
    // [111, 1101, 10111]
    
    [
      { name: "张三", age: 30 },
      { name: "李四", age: 24 },
      { name: "王五", age: 28  }
    ].sort(function(o1, o2) {
      return o1.age - o2.age;
    })
    // [
    //   { name: "李四", age: 24 },
    //   { name: "王五", age: 28  },
    //   { name: "张三", age: 30 }
    // ]

### map

map方法的回调函数依次接受三个参数，分别是当前的数组成员、当前成员的位置和数组本身。原数组没有变化。

### reduce 和 reduceRight

reduce方法和reduceRight方法的作用，是依次处理数组的每个元素，最终累计为一个值。这两个方法的差别在于，reduce对数组元素的处理顺序是从左到右（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员），其他地方完全一样。

reduce方法的第一个参数是一个处理函数。该函数接受四个参数，分别是：

* 用来累计的变量（即当前状态），默认值为0
* 数组的当前元素
* 当前元素在数组中的序号（从0开始）
* 原数组

前两个是必须的，后两个则是可选的。

    [1, 2, 3, 4, 5].reduce(function(x, y){
        return x+y;
    });
    // 15

如果要对累计变量指定初值，可以把它放在reduce方法的第二个参数

    [1, 2, 3, 4, 5].reduce(function(x, y){
      return x+y;
    }, 10);
    // 25

### indexOf 和 lastIndexOf

    var a = ['a','b','c'];
    
    a.indexOf('b')
    // 1
    
    a.indexOf('y')
    // -1

indexOf方法还可以接受第二个参数，表示搜索的开始位置。

    ['a','b','c'].indexOf('a', 1)
    // -1
