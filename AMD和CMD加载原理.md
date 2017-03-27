### 原理一：id即路径 原则。
```txt
通常我们的入口是这样的： require( [ 'a', 'b' ], callback ) 。
这里的 'a'、'b' 都是 ModuleId。通过 id 和路径的对应原则，加载器才能知道需要加载的 js 的路径。
在这个例子里，就是 baseUrl + 'a.js' 和 baseUrl + 'b.js'。
但 id 和 path 的对应关系并不是永远那么简单，比如在 AMD 规范里就可以通过配置 Paths  来给特定的 id 指配 path。
```
### 原理二：createElement('script') & appendChild
```txt
知道路径之后，就需要去请求。一般是通过 createElement('script') & appendChild 去请求。
这个大家都知道，不多说。
有时候有的加载器也会通过 AJAX 去请求脚本内容。
一般来说，需要给 <script> 设置一个属性用来标识模块 id, 作用后面会提到。
```
### 原理三：document.currentScript
```txt
a.js 里可能是 define( id, factory ) 或者是 define( factory )，后者被称为匿名模块。
那么当 define(factory) 被执行的时候，我们怎么知道当前被定义的是哪个模块呢，具体地说，这个匿名模块的实际模块 id 是什么？ 
答案是通过 document.currentScript 获取当前执行的<script>，然后通过上面给 script 设置的属性来得到模块 id。
需要注意的是，低级浏览器是不支持 currentScript 的，这里需要进行浏览器兼容。
在高级浏览器里面，还可以通过 script.onload 来处理这个事情。
```
### 原理四：依赖分析
```txt
在继续讲之前，需要先简单介绍下模块的生命周期。
模块在被 Define 之后并不是马上可以用了，在你执行它的 factory 方法来生产出最终的 export 之前，你需要保证它的依赖是可用的。
那么首先就要先把依赖分析出来。
简单来说，就是通过 toString 这个方法得到 factory 的内容，然后用正则去匹配其中的 require( 'moduleId' )。
当然也可以不用正则。这就是为什么 require( var );  
这种带变量的语句是不被推荐的，因为它会影响依赖分析。
如果一定要用变量，可以用 require( [ var ] ) 这种异步加载的方式。
```
### 原理五：递归加载
在分析出模块的依赖之后，我们需要递归去加载依赖模块。用伪代码来表达大概是这样的：
```js
Module.prototype.load = function () {
    var deps = this.getDeps();
    for (var i = 0; i < deps.length; i++) {
        var m = deps[i];
        if (m.state < STATUS.LOADED) {
            m.load();
        }
    }
    this.state = STATUS.LOADED;
}
```
```txt
上面的代码只是表达一个意思，实际上 load 方法很可能是异步的，所以递归的返回要特殊处理下。
实现一个可用的加载器并没有那么简单，比如你要处理循环依赖，还有各种各样的牵一发动全身的细节。
但要说原理，大概就是这么几条。
个人觉得，比起照着规范实现一个加载器，更加吸引人的是 AMD 或者 CommonJS 这些规范的完善和背后的设计思路。
```
