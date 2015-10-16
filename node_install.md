# 安装与版本管理

检测 Node 是否能正常运行

    node --version
    # 或者
    node -v

运行JavaScript脚本

    node demo
    // 或者
    node demo.js

在文件的第一行，如果加入了解释器的位置，就可以将其作为命令行工具直接调用

    #!/usr/bin/env node
    ./foo.js arg1 arg2 ...

可以通过 n 模块进行版本管理

    sudo npm install n -g

n 模块的用法可以查看帮助

    n -h
    n --help
    
n 模块不能运行在 Windows 上