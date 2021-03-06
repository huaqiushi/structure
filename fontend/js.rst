JS
===========

声明变量
----
- ES5：var, function
- ES6：var, function, let, const, import, class

    - 在ES5中只有全局作用域和函数作用域，ES6中的let命令实现了块级作用域
    - let命令声明的变量不存在变量提升，存在暂时性死区（即必须先声明后使用）
    - const命令与let命令的区别在于const命令声明常量

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
主要代表为Node.js。用module.exports规定模块的对外接口，用require加载模块

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
主要代表为Require.js。

CMD
''''''''''''''''
主要代表为Sea.js。

ES6 Module
'''''''''''''''
用export规定模块的对外接口，用import输入其他模块提供的功能

.. code-block:: js

    // profile.js
    let firstName = 'Michael';
    let lastName = 'Jackson';
    let year = 1958;

    export {firstName, lastName, year};

    // main.js
    import {firstName, lastName, year} from './profile.js';

    function setName(element) {
      element.textContent = firstName + ' ' + lastName;
    }

注：export default用于指定模块的默认输出。本质上，export default就是将模块内的变量或方法赋值给default，然后在import时系统允许你为它取任意名字
