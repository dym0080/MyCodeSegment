

- #### JS1.判断是否是数组最佳代码
```
var isArray = function(obj) { 
return Object.prototype.toString.call(obj) === '[object Array]'; 
}
```
- #### JS2.获取数组中的最大值最小值
```
	Array.prototype.max = function() {
		return Math.max.apply({}, this);
	};
	Array.prototype.min = function() {
		return Math.min.apply({}, this);
	};
```
- #### 判断是否是一个函数
```
function isFunction(obj) {
   return Object.prototype.toString.call(obj)=== '[object Function]';
}
```
