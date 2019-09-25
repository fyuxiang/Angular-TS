# Angular-TS
#TSlib.ts

#首先，angular是基于ts开发的，所以ts的一些方法库必须要先弄明白，用到的方法主要有以下 
#[git连接地址](https://github.com/microsoft/tslib/blob/master/tslib.js)
*我们直接看es6的语法*
__继承__
 - 静态方法继承
 静态方法的继承肯定是相对于class而言的，对象本身不存在静态方法，
 function Class(){}; Class.method = function(){};
 method就是构造函数Class的静态方法；
 在ES6中定义了静态的概念，即static修饰符；既然有了静态方法，那么es5中的继承方法就不应用于class的继承，所以这里首先要扩展静态属性继承的函数。
 
