prototype and __proto__
```js
var Animal = function(){
	this.top = 'god';
	this.name = 'animal';
}
Animal.prototype.info = function(){
	console.log('四条腿+一个脑袋')
}

var Dog = function(){
	this.name = 'dog';
}
/**
 * constructor 属性返回对创建此对象的函数的引用
 */
Animal.prototype
	Objcet{}
		constructor: function(){
			name: 'Animal'
		}
		info
		__proto__

Dog.prototype
	Objcet{}
		constructor: function(){
			name: 'Dog'
		}
		__proto__
var animal = new Animal()
animal
	top: 'god'
	name: 'animal'
	__proto__
		Animal.prototype
+++++++++++++++++++++++++
Dog.prototype = Animal.prototype;
Dog.prototype.constructor = Dog;
```

```js
var Bird = function(type){this.name = 'name';this.type = type}
==>
  undefined
var bird = new Bird('niao')
bird
==>
  Bird {name: "name", type: "niao"}
    name: "name"
    type: "niao"
    __proto__: 
Bird.prototype.fly = 'fei qi lai'
bird
==>
  Bird {name: "name", type: "niao"}
    name: "name"
    type: "niao"
    __proto__: 
      contructor
      fly: 'fei qi la'
      __proto__
```
