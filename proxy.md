# 设置代理

如果公司使用代理服务器，Node.js就需要设置代理，否则用`npm`下载什么都不好使

    npm config set proxy http://server:port
    npm config set https-proxy http://server:port

如果代理需要认证的话可以这样来设置

    npm config set proxy http://username:password@server:port
    npm config set https-proxy http://username:pawword@server:port

如果代理不支持https或者觉得https慢，可以设置npm的获取地址

    npm config set registry "http://registry.npmjs.org/"

清除npm的代理

    npm config delete http-proxy
    npm config delete https-proxy
