深层复制问题
```js
// 变量的引用问题
var obj = {name: 'jack'};
var obj2 = obj;
// 此时的obj2和obj共用一个内存块，指向同一内存地址，一改皆改，不能达到复制效果
// 需要用到深层复制，比如 
var obj3 = $.extend(true,{},obj);

// 字符串是不可变的，也就是说，表面上看，字符串每次发生了变化，其实都是新的字符串，开了新的内存存储
// 以此为hack
var obj4 = JSON.parse( JSON.stringify( obj ) )
```
数组push多个数据
```js
// 利用apply参数特性，数组自动解析为单个
var arr = ['x','y','z'];
Array.prototype.push.apply( arr, [1,2,3] )
```
