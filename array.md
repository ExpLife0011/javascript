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
    a // []
    a.length // 1
    
    var a = new Array(2);
    a // []
    a.length // 2
    
    var a = new Array(1,2);
    a // [1,2]
    a.length // 2
    
没有参数时，返回一个空数组；使用一个参数时，返回一个指定长度的空数组；使用多个参数，返回一个指定成员的数组。所以，建议总是直接采用方括号创建数组。

## 数组的空位

数组的空位是指没有元素(不是undefined，就是没有元素)

    // arr 和 arr2 完全等价
    var arr = [, , , ,];
    var arr2 = new Array(3);

与下面的不同
    
    // 有3个元素
    var arr3 = [undefined, undefined, undefined];

arr、arr2、arr3的长度相等。arr 和 arr2 完全等价，虽有长度，但没有元素。arr3 有3个元素。

## 数组元素的访问

对象有两种读取成员的方法：“点”结构（object.key）和方括号结构（object[key]）。但是，对于数字的键名，不能使用点结构，arr.0的写法不合法，因为单独的数字不能作为标识符（identifier）。所以，数组成员只能用方括号arr[0]表示（方括号是运算符，可以接受数值）。例外见非数字索引。

## 数组与对象的关系

数组也属于对象

    // 数组只是一种特殊的对象
    typeof [1, 2, 3] // "object"

"特殊"是指

(1) 数组不用为每个元素指定键名，而对象的每个成员都必须指定键名。数组的键默认是按次序排列的整数（0，1，2...）。

(2) 对象以字符串来识别键名，非字符串的键名会被转为字符串。数组的键名其实也是字符串，所有的整数键名默认都会转为字符串。

    var arr = ['a', 'b', 'c'];
    
    arr['0'] // 'a'
    arr[0] // 'a'

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
    
如果人为设置length大于当前元素个数，则数组的成员数量会增加到这个值，新增的位置填入空元素。

    var a = ['a'];
    
    a.length = 3;
    a // ["a", undefined × 2]

当length属性设为大于数组个数时，新增的位置都填充为undefined。

如果人为设置length为不合法的值，JavaScript会报错。

## 非数字索引

由于数组本质上是对象的一种，所以我们可以为数组添加属性，但是这不影响length属性的值。

    var arr = ['a', 'b'];
    arr['c'] = 'c';
    arr.d = 'd';
    console.log(arr);
    console.log(arr.c); // c
    console.log(arr['c']); // c
    console.log(arr.d); // d
    console.log(arr['d']); // d

