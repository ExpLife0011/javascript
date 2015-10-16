# package.json

每个项目的根目录下面，一般都有一个package.json文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。`npm install`命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

    {
        "name": "Hello World",
        "version": "0.0.1",
        "author": "张三",
        "description": "第一个node.js程序",
        "keywords":["node.js","javascript"],
        "repository": {
            "type": "git",
            "url": "https://path/to/url"
        },
        "license":"MIT",
        "engines": {"node": "0.10.x"},
        "bugs":{"url":"http://path/to/bug","email":"bug@example.com"},
        "contributors":[{"name":"李四","email":"lisi@example.com"}],
        "scripts": {
            "start": "node index.js"
        },
        "dependencies": {
            "express": "latest",
            "mongoose": "~3.8.3",
            "handlebars-runtime": "~1.0.12",
            "express3-handlebars": "~0.5.0",
            "MD5": "~1.2.0"
        },
        "devDependencies": {
            "bower": "~1.2.8",
            "grunt": "~0.4.1",
            "grunt-contrib-concat": "~0.3.0",
            "grunt-contrib-jshint": "~0.7.2",
            "grunt-contrib-uglify": "~0.2.7",
            "grunt-contrib-clean": "~0.5.0",
            "browserify": "2.36.1",
            "grunt-browserify": "~1.3.0",
        }
    }

package.json文件可以手工编写，也可以使用`npm init`命令自动生成。

    npm init

## scripts字段

scripts指定了运行脚本命令的npm命令行缩写，比如start指定了运行`npm run start`时，所要执行的命令。

    npm run start
    # 相当于
    node index.js

## dependencies字段，devDependencies字段

dependencies和devDependencies两项，分别指定了项目运行所依赖的模块、项目开发所需要的模块。

直接使用`npm install`命令，就会在当前目录中安装所需要的模块。

    npm install
