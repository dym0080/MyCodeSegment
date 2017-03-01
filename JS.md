

#### JS1.判断是否是数组最佳代码
```
var isArray = function(obj) { 
return Object.prototype.toString.call(obj) === '[object Array]'; 
}
```
#### JS2.获取数组中的最大值最小值
```
	Array.prototype.max = function() {
		return Math.max.apply({}, this);
	};
	Array.prototype.min = function() {
		return Math.min.apply({}, this);
	};
```
#### JS3.判断是否是一个函数
```
function isFunction(obj) {
   return Object.prototype.toString.call(obj)=== '[object Function]';
}
```
#### JS4.获取指定函数的函数名称（用于兼容IE）
```
    /**
    * 获取指定函数的函数名称（用于兼容IE）
    * @param {Function} fun 任意函数
    */
	function getFunctionName(fun) {
	    if (fun.name !== undefined)
	        return fun.name;
	    var ret = fun.toString();
	    ret = ret.substr('function '.length);
	    ret = ret.substr(0, ret.indexOf('('));
	    return ret;
	}
    
    //测试
    function fn1(){}
    var fn2=function(){};
    var fn3=function AAA(){};
	console.log(getFunctionName(fn1));//输出fn1
	console.log(getFunctionName(fn2));//输出空
	console.log(getFunctionName(fn3));//输出AAA
```
#### JS5. 查询指定窗口的视口尺寸，如果不指定窗口，查询当前窗口尺寸
```
	/**
	 * 查询指定窗口的视口尺寸，如果不指定窗口，查询当前窗口尺寸
	 **/
	function getViewportSize(w) {
		w = w || window;

		// IE9及标准浏览器中可使用此标准方法
		if ('innerHeight' in w) {
			return {
				width: w.innerWidth,
				height: w.innerHeight
			};
		}

		var d = w.document;
		// IE 8及以下浏览器在标准模式下
		if (document.compatMode === 'CSS1Compat') {
			return {
				width: d.documentElement.clientWidth,
				height: d.documentElement.clientHeight
			};
		}

		// IE8及以下浏览器在怪癖模式下
		return {
			width: d.body.clientWidth,
			height: d.body.clientHeight
		};
	}
    
        //test
	console.log(getViewportSize());//Object {width: 1280, height: 214}
```
#### JS6. 获取指定window中滚动条的偏移量，如未指定则获取当前window
```
/**
 * 获取指定window中滚动条的偏移量，如未指定则获取当前window
 * 滚动条偏移量
 *
 * @param {window} w 需要获取滚动条偏移量的窗口
 * @return {Object} obj.x为水平滚动条偏移量,obj.y为竖直滚动条偏移量
 */
function getScrollOffset(w) {
    w =  w || window;
    // 如果是标准浏览器
    if (w.pageXOffset != null) {
        return {
            x: w.pageXOffset,
            y: w.pageYOffset
        };
    }

    // IE 8及以下浏览器在标准模式下，根据兼容性不同访问不同元素
    var d = w.document;
    if (d.compatMode === 'CSS1Compat') {
        return {
            x: d.documentElement.scrollLeft,
            y: d.documentElement.scrollTop
        }
    }
    // IE8及以下浏览器在怪癖模式下
    return {
        x: d.body.scrollLeft,
        y: d.body.scrollTop
    };
}
```
#### JS7.使用!!操作符转换布尔值
>有时候我们需要对一个变量查检其是否存在或者检查值是否有一个有效值，如果存在就返回`true`值。为了做这样的验证，我们可以使用`!!`操作符来实现是非常的方便与简单。对于变量可以使用`!!variable`做检测，只要变量的值为:`0`、`null`、`" "`、`undefined`或者`NaN`都将返回的是`false`，反之返回的是`true`。比如下面的示例：
```
function Account(cash) {
    this.cash = cash;
    this.hasMoney = !!cash;
}
var account = new Account(100.50);
console.log(account.cash); // 100.50
console.log(account.hasMoney); // true
var emptyAccount = new Account(0);
console.log(emptyAccount.cash); // 0
console.log(emptyAccount.hasMoney); // false
```
>在这个示例中，只要`account.cash`的值大于`0`，那么`account.hasMoney`返回的值就是`true`。
#### JS8.使用+将字符串转换成数字
这个技巧非常有用，其非常简单，可以交字符串数据转换成数字，不过其只适合用于字符串数据，否则将返回`NaN`，比如下面的示例：
```
function toNumber(strNumber) {
    return +strNumber;
}
console.log(toNumber("1234")); // 1234 
console.log(toNumber("ACB")); // NaN
```
这个也适用于Date，在本例中，它将返回的是时间戳数字：
`console.log(+new Date()) // 1461288164385`

#### JS9.使用||运算符
在ES6中有默认参数这一特性。为了在老版本的浏览器中模拟这一特性，可以使用||操作符，并且将将默认值当做第二个参数传入。如果第一个参数返回的值为`false`，那么第二个值将会认为是一个默认值。如下面这个示例：
```
function User(name, age) {
    this.name = name || "Oliver Queen";
    this.age = age || 27;
}
var user1 = new User();
console.log(user1.name); // Oliver Queen 
console.log(user1.age); // 27 
var user2 = new User("Barry Allen", 25); 
console.log(user2.name); // Barry Allen 
console.log(user2.age); // 25
```
#### JS10.在循环中缓存array.length
这个技巧很简单，这个在处理一个很大的数组循环时，对性能影响将是非常大的。基本上，大家都会写一个这样的同步迭代的数组：
```
for (var i = 0; i < array.length; i++) {
    console.log(array[i]);
}
```
如果是一个小型数组，这样做很好，如果你要处理的是一个大的数组，这段代码在每次迭代都将会重新计算数组的大小，这将会导致一些延误。为了避免这种现象出现，可以将array.length做一个缓存：
```
var length = array.length;
for (var i = 0; i < length; i++) {
    console.log(array[i]);
}
```
你也可以写在这样：
```
for (var i = 0, length = array.length; i < length; i++) {
    console.log(array[i]);
}
```
