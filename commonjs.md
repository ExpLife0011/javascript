# 模块

Node程序由许多个模块组成。Node模块采用了CommonJS规范。

根据CommonJS规范，一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在一个文件定义的变量（还包括函数和类），都是私有的，对其他文件是不可见的。

有的模块是由多个模板组成的目录。详见下文。

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

require命令用于加载文件，后缀名默认为`.js`。

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

**目录的加载规则**

有时候，一个模块本身就是一个目录，目录中包含多个文件。这时候，Node在package.json文件中，寻找main属性所指明的模块入口文件。

在目录中放置一个package.json文件，并且将入口文件写入main字段。下面是一个例子。

    // package.json
    { "name" : "some-library",
      "main" : "./lib/some-library.js" }
      
require发现参数字符串指向一个目录以后，会自动查看该目录的package.json文件，然后加载main字段指定的入口文件。如果package.json文件没有main字段，或者根本就没有package.json文件，则会加载该目录下的index.js文件或index.node文件。

**模块的缓存**

第一次加载某个模块时，Node会缓存该模块。以后再加载该模块，就直接从缓存取出该模块的exports属性。

    require('./example.js');
    require('./example.js').message = "hello";
    require('./example.js').message
    // "hello"

上面代码中，连续三次使用require命令，加载同一个模块。第二次加载的时候，为输出的对象添加了一个message属性。但是第三次加载的时候，这个message属性依然存在，这就证明require命令并没有重新加载模块文件，而是输出了缓存。

如果想要多次执行某个模块，可以让该模块输出一个函数，然后每次require这个模块的时候，重新执行一下输出的函数。

注意，缓存是根据绝对路径识别模块的，如果同样的模块名，但是保存在不同的路径，require命令还是会重新加载该模块。

**require.main**

require方法有一个main属性，可以用来判断模块是直接执行，还是被调用执行。

直接执行的时候（node module.js），require.main属性指向模块本身。

    // 可以在module.js文件中做一些判断
    require.main === module
    // true
    
调用执行的时候（通过require加载该脚本执行），上面的表达式返回false。

## 自定义模块

Node模块采用CommonJS规范。只要符合这个规范，就可以自定义模块。