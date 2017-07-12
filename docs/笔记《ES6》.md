#### 块级作用域
```txt
ES5只有全局作用域和函数作用域，没有块级作用域，这带来很多不合理的场景
ES6 引入了块级作用域，明确允许在块级作用域之中声明函数。
```
#### 变量提升
ES6 规定，块级作用域之中，函数声明语句的行为类似于let，在块级作用域之外不可引用。
```js
function f() { console.log('I am outside!'); }
(function () {
  if (false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }
  f();
}());
```
等同于
```js
function f() { console.log('I am outside!'); }
(function () {
  var f = undefined;
  if (false) {
    function f() { console.log('I am inside!'); }
  }
  f();
}());
```
```txt

ES5 if内声明的函数f会被提升到函数头部
```
#### 暂时性死区
###### 只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
````javascript
var tmp = 123;
if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
````
#### 对象冻结，不可改变 Object.freeze
```js
var constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach( (key, value) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
```
#### window与全局变量
```txt
ES5中 var a = 1;自动挂载在window.a 属性
ES6中，let const class等全局声明的变量，与window脱节
```
```js
// ES5 
var a = 1;
window.a // 1
// ES6
let a = 1;
window.a // undefined
```
