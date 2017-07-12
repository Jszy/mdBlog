### object.create 向下兼容
```
object.create = object.create || function(obj){
  let F = function(){}
  F.prototype = obj
  return new F()
}
```