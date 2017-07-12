## 引用
#### 对象通过引用来传递，它们永远不会被复制
````javascript
var x = stooge;//stooge是一对象
x.name = 'zhang';
var y = stooge.name;
  //因为x和stooge是指向同一个对象的引用，所以y为'zhang'

var a = {}, b = {}, c = {};
  //a b c 每个都引用一个不同的空对象
var a = b = c = {};
  //a b c 都引用同一个空对象
  
/*
 * 实战项目中经常会遇到这个问题，
 * 把后端返回的对象传递给一个函数处理下，然后再传递给别的函数
 * 处理之后的原数据也跟着变化，解决方式 深层copy
 * var dist = $.extend(true,{},src);
 */  
````
## 闭包
#### 闭包是一种有效减少全局污染的方法
````html
一个内部函数除了可以访问自己的参数和变量，
同时它也能自由访问把它嵌套在其中的父函数的参数和变量。
通过函数字面量创建的函数对象包含一个连到外部上下文的连接。
这被称为闭包
````
## this(不同的调用模式，指向不一样)
#### 方法调用模式：当一个函数被保存为对象的一个属性时，我们称它为一个方法。当一个方法被调用时，this被绑定到该对象。
````javascript
var myObject = {
  value: 0,
  increment: function(inc){
    this.value += typeof inc === "number" ? inc : 1;
  }
}
myObject.increment();
myObject.value // 1
myObject.increment(2);
myObject.value // 3
````
#### 函数调用模式：当一个函数并非一个对象的属性时，那么它就是被当做一个函数来调用的。这是语言设计上的一个错误，解决方法
````javascript
var add = function(a,b){
  return a + b;
}
// 给myObject 增加一个double方法
myObject.double = function(){
  var me = this;
  var helper = function(){
    me.value = add(me.value, me.value);
  }
  helper();
}
myObject.double();
myObject.value // 6
````
#### extend继承
```js
    function extend(Child, Parent) {
　　　　var F = function(){};
　　　　F.prototype = Parent.prototype;
　　　　Child.prototype = new F();
　　　　Child.prototype.constructor = Child;
　　　　Child.uber = Parent.prototype;
　　}
```
`Child.uber = Parent.prototype;`
```txt
意思是为子对象设一个uber属性，这个属性直接指向父对象的prototype属性。
（uber是一个德语词，意思是"向上"、"上一层"。）这等于在子对象上打开一条通道，可以直接调用父对象的方法
。这一行放在这里，只是为了实现继承的完备性，纯属备用性质。
```
#### 拷贝继承
```js
    function extend2(Child, Parent) {
　　　　var p = Parent.prototype;
　　　　var c = Child.prototype;
　　　　for (var i in p) {
　　　　　　c[i] = p[i];
　　　　　　}
　　　　c.uber = p;
　　}
```
## js声明变量尽可能的放在函数顶部
javascript确实有函数作用域，那意味着定义在函数中的变量和参数在函数外部是不可见的，而在一个函数内部任何位置定义的变量，在该函数内部任何地方都可见。  
很多现代语言都推荐尽可能的延迟声明变量。而用在javascript上的话却会成为糟糕的建议，因为它缺少块级作用域。所以，最好的做法是在`函数体的顶部声明`函数中可能用到的所有变量
## 对象( 是可变的键控集合 )
```txt
javascript中简单数据类型有 Number String Boolean null undefined，其他所有都是对象。
数字、字符串、布尔值貌似对象，因为它们拥有方法，但它们是不可变的。
对象是可变的键控集合。
数组是对象，函数是对象，正则表达式是对象，当然，对象自然也是对象。
对象的属性值是可以除了undefined之外的任何值。
正确的使用原型链，可以减少对象初始化时消耗的时间和内存。
```
## 继承
#### 伪类模式(构造器 new)本意是向面向对象靠拢，但看起来格格不入。更好的备选方案就是根本不使用new
#### 原型模式 基于原型的继承，相比来说，比基于类的继承在概念上更简单
```txt
纯粹的原型模式中，我们摒弃类，转而专注于对象
```
```js

let obj1 = {
  name: 'obj1',
  say(){
    console.log('obj1')
  }
}

let obj2 = Object.create( obj1 );
obj2.name = 'obj2';
obj2.age = 15;

obj2.say() // obj1
obj1.name // obj1
obj1.age // undefined
```
这是一种`差异化继承`，通过定制一个新的对象，我们指明它与基于的对象的区别




