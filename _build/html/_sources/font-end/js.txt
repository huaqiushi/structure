JS
===========

对象
-------

事件
-------

JS模块化
----------------
JS模块化规范：CommonJS、AMD、CMD、ES6 Module

- CommonJS是服务器模块化、同步加载模块
- AMD是浏览器模块化、异步加载模块
- ES6在语言标准上实现了模块化，旨在成为服务器和浏览器通用的模块解决方案

CommonJS
'''''''''''''''''''''
主要代表为NodeJS。用module.exports暴露模块内的接口，用require加载模块

.. code-block:: js

    // math.js
    var basicNum = 0;
    function add(a, b){
        return a + b;
    }

    module.exports = {
        add: add,
        basicNum: basicNum
    }

    // index.js
    var math = require('./math');
    var a;
    a = math.add(100, 5);
    console.log(a);
    console.log(math.basicNum);

    //Node.js command
    > node index


AMD
'''''''''''''''''

ES6 Module
''''''''''''''''
