# 模块

Node程序由许多个模块组成，每个模块就是一个文件。Node模块采用了CommonJS规范。

根据CommonJS规范，一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在一个文件定义的变量（还包括函数和类），都是私有的，对其他文件是不可见的。

如果想在多个文件分享变量，必须定义为global对象的属性。

    global.warning = true;

## module

每个模块内部，都有一个module对象，代表当前模块。

## module.exports

CommonJS规定，每个文件的对外接口是module.exports对象。这个对象的所有属性和方法，都可以被其他文件导入。

其他文件加载该模块，实际上就是读取module.exports变量。

## exports

为了方便，Node为每个模块提供一个exports变量，指向module.exports。这等同在每个模块头部，有一行这样的命令。

    var exports = module.exports;

注意，不能直接将exports变量指向一个值，因为这样等于切断了exports与module.exports的联系。

    exports = function(x) {console.log(x)};

上面这样的写法是无效的，因为exports不再指向module.exports了。

## require

Node.js使用CommonJS模块规范，内置的require命令用于加载模块文件。

require命令的基本功能是，读入并执行一个JavaScript文件，然后返回该模块的exports对象。如果没有发现指定模块，会报错。

**加载规则**

require命令用于加载文件，后缀名默认为.js。

    var foo = require('foo');
    //  等同于
    var foo = require('foo.js');

根据参数的不同格式，require命令去不同路径寻找模块文件。

（1）如果参数字符串以“/”开头，则表示加载的是一个位于绝对路径的模块文件。比如，require('/home/marco/foo.js')将加载/home/marco/foo.js。

（2）如果参数字符串以“./”开头，则表示加载的是一个位于相对路径（跟当前执行脚本的位置相比）的模块文件。比如，require('./circle')将加载当前脚本同一目录的circle.js。

（3）如果参数字符串不以“./“或”/“开头，则表示加载的是一个默认提供的核心模块（位于Node的系统安装目录中），或者一个位于各级node_modules目录的已安装模块（全局安装或局部安装）。

举例来说，脚本/home/user/projects/foo.js执行了require('bar.js')命令，Node会依次搜索以下文件。

    /usr/local/lib/node/bar.js
    /home/user/projects/node_modules/bar.js
    /home/user/node_modules/bar.js
    /home/node_modules/bar.js
    /node_modules/bar.js

require.main