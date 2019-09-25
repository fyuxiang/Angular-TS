#TSlib.ts

*首先，angular是基于ts开发的，所以ts的一些方法库必须要先弄明白，用到的方法主要有以下 *
*[git连接地址](https://github.com/microsoft/tslib/blob/master/tslib.js)*
*我们直接看es6的语法*
**继承**
 - 静态方法继承
 静态方法的继承肯定是相对于class而言的，对象本身不存在静态方法
 ```
 function Class(){};
 Class.method = function(){};
 ```
 method就是构造函数Class的静态方法；
 在ES6中定义了静态的概念，即static修饰符；既然有了静态方法，那么es5中的继承方法就不应用于class的继承，所以这里首先要扩展静态属性继承的函数。
 ```
 var extendStatics = function(d, b) {
    extendStatics = Object.setPrototypeOf ||
        ({ __proto__: [] } instanceof Array && function (d, b) { d.__proto__ = b; }) ||
        function (d, b) { for (var p in b) if (b.hasOwnProperty(p)) d[p] = b[p]; };
    return extendStatics(d, b);
};
 ```
 方法首先调用的就是Object的setPrototypeOf，从而直接实现方法的继承，因为class本质是function，同样也是对象，所以静态方法也就是class构造器本身的实例方法，所以能够直接通过原型链来继承。
 { __proto__: [] } instanceof Array判断是否支持___proto_隐式继承，如果支持，就直接将父b通过隐形链传递上去，
 如果不支持，就通过遍历赋值，通过if代码块我们可以看到，这里只继承了class自身的可遍历的实例属性。
 -类继承
 ```
export function __extends(d, b) {
    extendStatics(d, b);
    function __() { this.constructor = d; }
    d.prototype = b === null ? Object.create(b) : (__.prototype = b.prototype, new __());
}
 ```
 步骤一：静态方法继承；
 步骤二：prototype继承，即原型实例继承； 在ts中class中的方法都是原型上的方法，属性则是实例属性。所以这里的继承属于原型式的继承，参考Object.create方法，只实现了原型的继承。对于实例属性的继承，需要开发者自己在constructor中super调用才能够完成。具体的继承实现步骤如下例所示
 __例子：__
 在ts中继承转es后的代码如下
  ```
var Child = (function(_super){
    __extend(Child, _super);
    function Child(){
        var _this = _super.call(this) ||this;
        return _this;
    }
    return Child;
}(Parent))
 ```
