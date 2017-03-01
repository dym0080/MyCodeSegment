

# JS1.判断是否是数组最佳代码
```
var isArray = function(obj) { 
return Object.prototype.toString.call(obj) === '[object Array]'; 
}
```
