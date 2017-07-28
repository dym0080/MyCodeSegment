## 1.字符串操作
#### 1.1使用+将字符串转换成数字
这个技巧非常有用，其非常简单，可以交字符串数据转换成数字，不过其只适合用于字符串数据，否则将返回`NaN`，比如下面的示例：
```js
function toNumber(strNumber) {
    return +strNumber;
}
console.log(toNumber("1234")); // 1234 
console.log(toNumber("ACB")); // NaN
```
这个也适用于Date，在本例中，它将返回的是时间戳数字：
`console.log(+new Date()) // 1461288164385`

#### 1.2使用||运算符
在ES6中有默认参数这一特性。为了在老版本的浏览器中模拟这一特性，可以使用`||`操作符，并且将将默认值当做第二个参数传入。如果第一个参数返回的值为`false`，那么第二个值将会认为是一个默认值。如下面这个示例：
```js
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
#### 1.3去除字符串空格
```js
//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
function trim(str,type){
    switch (type){
        case 1:return str.replace(/\s+/g,"");
        case 2:return str.replace(/(^\s*)|(\s*$)/g, "");
        case 3:return str.replace(/(^\s*)/g, "");
        case 4:return str.replace(/(\s*$)/g, "");
        default:return str;
    }
}
```
#### 1.4字母大小写切换
```js
/*type
1:首字母大写   
2：首页母小写
3：大小写转换
4：全部大写
5：全部小写
 * */
//changeCase('asdasd',1)
//Asdasd
function changeCase(str,type)
{
    function ToggleCase(str) {
        var itemText = ""
        str.split("").forEach(
            function (item) {
                if (/^([a-z]+)/.test(item)) {
                    itemText += item.toUpperCase();
                }
                else if (/^([A-Z]+)/.test(item)) {
                    itemText += item.toLowerCase();
                }
                else{
                    itemText += item;
                }
            });
        return itemText;
    }

    switch (type) {
        case 1:
            return str.replace(/^(\w)(\w+)/, function (v, v1, v2) {
                return v1.toUpperCase() + v2.toLowerCase();
            });
        case 2:
            return str.replace(/^(\w)(\w+)/, function (v, v1, v2) {
                return v1.toLowerCase() + v2.toUpperCase();
            });
        case 3:
            return ToggleCase(str);
        case 4:
            return str.toUpperCase();
        case 5:
            return str.toLowerCase();
        default:
            return str;
    }
}
```
#### 1.5字符串循环复制
```js
//repeatStr(str->字符串, count->次数)
//repeatStr('123',3)
//"123123123"
function repeatStr(str, count) {
    var text = '';
    for (var i = 0; i < count; i++) {
        text += str;
    }
    return text;
}
```
#### 1.6字符串替换
```js
//字符串替换(字符串,要替换的字符,替换成什么)
function replaceAll(str,AFindText,ARepText){
　　　raRegExp = new RegExp(AFindText,"g");
　　　return str.replace(raRegExp,ARepText);
}
```
#### 1.7字符串替换*
```js
//replaceStr(字符串,字符格式, 替换方式,替换的字符（默认*）)
function replaceStr(str, regArr, type,ARepText) {
    var regtext = '', Reg = null,replaceText=ARepText||'*';
    //replaceStr('18819322663',[3,5,3],0)
    //188*****663
    //repeatStr是在上面定义过的（字符串循环复制），大家注意哦
    if (regArr.length === 3 && type === 0) {
        regtext = '(\\w{' + regArr[0] + '})\\w{' + regArr[1] + '}(\\w{' + regArr[2] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = repeatStr(replaceText, regArr[1]);
        return str.replace(Reg, '$1' + replaceCount + '$2')
    }
    //replaceStr('asdasdasdaa',[3,5,3],1)
    //***asdas***
    else if (regArr.length === 3 && type === 1) {
        regtext = '\\w{' + regArr[0] + '}(\\w{' + regArr[1] + '})\\w{' + regArr[2] + '}'
        Reg = new RegExp(regtext);
        var replaceCount1 = repeatSte(replaceText, regArr[0]);
        var replaceCount2 = repeatSte(replaceText, regArr[2]);
        return str.replace(Reg, replaceCount1 + '$1' + replaceCount2)
    }
    //replaceStr('1asd88465asdwqe3',[5],0)
    //*****8465asdwqe3
    else if (regArr.length === 1 && type == 0) {
        regtext = '(^\\w{' + regArr[0] +  '})'
        Reg = new RegExp(regtext);
        var replaceCount = repeatSte(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
    //replaceStr('1asd88465asdwqe3',[5],1,'+')
    //"1asd88465as+++++"
    else if (regArr.length === 1 && type == 1) {
        regtext = '(\\w{' + regArr[0] +  '}$)'
        Reg = new RegExp(regtext);
        var replaceCount = repeatSte(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
}
```
#### 1.8检测字符串
```js
//checkType('165226226326','phone')
//false
//大家可以根据需要扩展
function checkType (str, type) {
    switch (type) {
        case 'email':
            return /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/.test(str);
        case 'phone':
            return /^1[3|4|5|7|8][0-9]{9}$/.test(str);
        case 'tel':
            return /^(0\d{2,3}-\d{7,8})(-\d{1,4})?$/.test(str);
        case 'number':
            return /^[0-9]$/.test(str);
        case 'english':
            return /^[a-zA-Z]+$/.test(str);
        case 'chinese':
            return /^[\u4E00-\u9FA5]+$/.test(str);
        case 'lower':
            return /^[a-z]+$/.test(str);
        case 'upper':
            return /^[A-Z]+$/.test(str);
        default :
            return true;
    }
}
```
#### 1.9检测密码强度
```js
//checkPwd('12asdASAD')
//3(强度等级为3)
function checkPwd(str) {
    var nowLv = 0;
    if (str.length < 6) {
        return nowLv
    }
    ;
    if (/[0-9]/.test(str)) {
        nowLv++
    }
    ;
    if (/[a-z]/.test(str)) {
        nowLv++
    }
    ;
    if (/[A-Z]/.test(str)) {
        nowLv++
    }
    ;
    if (/[\.|-|_]/.test(str)) {
        nowLv++
    }
    ;
    return nowLv;
}
```
#### 1.10随机码([toString详解](http://www.runoob.com/jsref/jsref-tostring-number.html))
```js
//count取值范围0-36

//randomNumber(10)
//"2584316588472575"

//randomNumber(14)
//"9b405070dd00122640c192caab84537"

//Math.random().toString(36).substring(2);
//"83vhdx10rmjkyb9"
function randomNumber(count){
   return Math.random().toString(count).substring(2);
}
```
#### 1.11查找字符串
可能标题会有点误导，下面我就简单说明一个需求，在字符串'sad44654blog5a1sd67as9dablog4s5d16zxc4sdweasjkblogwqepaskdkblogahseiuadbhjcibloguyeajzxkcabloguyiwezxc967'中找出'blog'的出现次数。代码如下
```js
function countStr (str,strSplit){
    return str.split(strSplit).length-1
}
var strTest='sad44654blog5a1sd67as9dablog4s5d16zxc4sdweasjkblogwqepaskdkblogahseiuadbhjcibloguyeajzxkcabloguyiwezxc967'
//countStr(strTest,'blog')
//6
```
#### 1.12使用+将字符串转换成数字
这个方法是在太多了，我之前写的文章([js数组操作--使用迭代方法替代for循环](https://segmentfault.com/a/1190000009870199),[js关键词变色](https://segmentfault.com/a/1190000009827940)，[数组打乱](https://segmentfault.com/a/1190000009827940)，[数组去重的实现和封装](https://segmentfault.com/a/1190000009827940))也有提到，我今天这里就写一种之前没用过的方法。
```js
//ES6新增的Set数据结构，类似于数组，但是里面的元素都是唯一的 ，其构造函数可以接受一个数组作为参数
//let arr=[1,2,1,2,6,3,5,69,66,7,2,1,4,3,6,8,9663,8]
//let set = new Set(array);
//{1,2,6,3,5,69,66,7,4,8,9663}
//ES6中Array新增了一个静态方法from，可以把类似数组的对象转换为数组
//Array.from(set)
//[1,2,6,3,5,69,66,7,4,8,9663]
function removeRepeatArray(arr){
    return Array.from(new Set(arr))
}
```

## 2.数组操作

#### 2.1判断是否是数组最佳代码
```js
var isArray = function(obj) { 
return Object.prototype.toString.call(obj) === '[object Array]'; 
}
```
#### 2.2获取数组中的最大值最小值
```js
	Array.prototype.max = function() {
		return Math.max.apply({}, this);
	};
	Array.prototype.min = function() {
		return Math.min.apply({}, this);
	};
```
#### 2.3在循环中缓存array.length
这个技巧很简单，这个在处理一个很大的数组循环时，对性能影响将是非常大的。基本上，大家都会写一个这样的同步迭代的数组：
```js
for (var i = 0; i < array.length; i++) {
    console.log(array[i]);
}
```
如果是一个小型数组，这样做很好，如果你要处理的是一个大的数组，这段代码在每次迭代都将会重新计算数组的大小，这将会导致一些延误。为了避免这种现象出现，可以将array.length做一个缓存：
```js
var length = array.length;
for (var i = 0; i < length; i++) {
    console.log(array[i]);
}
```
你也可以写在这样：
```js
for (var i = 0, length = array.length; i < length; i++) {
    console.log(array[i]);
}
```
#### 2.4获取数组中最后一个元素
`Array.prototype.slice(begin,end)`用来获取`begin`和`end`之间的数组元素。如果你不设置`end`参数，将会将数组的默认长度值当作end值。但有些同学可能不知道这个函数还可以接受负值作为参数。如果你设置一个负值作为`begin`的值，那么你可以获取数组的最后一个元素。如：
```js
var array = [1, 2, 3, 4, 5, 6];
console.log(array.slice(-1)); // [6] 
console.log(array.slice(-2)); // [5,6] 
console.log(array.slice(-3)); // [4,5,6]
```
#### 2.5数组截断
这个小技巧主要用来锁定数组的大小，如果用于删除数组中的一些元素来说，是非常有用的。例如，你的数组有`10`个元素，但你只想只要前五个元素，那么你可以通过`array.length=5`来截断数组。如下面这个示例：
```js
var array = [1, 2, 3, 4, 5, 6];
console.log(array.length); // 6
array.length = 3; 
console.log(array.length); // 3
console.log(array); // [1,2,3]
```
#### 2.6合并数组
如果你要合并两个数组，一般情况之下你都会使用`Array.concat()`函数：
```js
var array1 = [1,2,3]; 
var array2 = [4,5,6]; 
console.log(array1.concat(array2)); // [1,2,3,4,5,6];
```
然后这个函数并不适合用来合并两个大型的数组，因为其将消耗大量的内存来存储新创建的数组。在这种情况之个，可以使用`Array.pus().apply(arr1,arr2)`来替代创建一个新数组。这种方法不是用来创建一个新的数组，其只是将第一个第二个数组合并在一起，同时减少内存的使用：
```js
var array1 = [1,2,3]; 
var array2 = [4,5,6]; 
console.log(array1.push.apply(array1, array2)); // [1,2,3,4,5,6];
```
#### 2.7数组顺序打乱
```js
function upsetArr(arr){
    return arr.sort(function(){ return Math.random() - 0.5});
}
```
#### 2.8数组求和，平均值
```js
//这一块的封装，主要是针对数字类型的数组
//求和
function sumArr(arr){
    var sumText=0;
    for(var i=0,len=arr.length;i<len;i++){
        sumText+=arr[i];
    }
    return sumText
}
//平均值,小数点可能会有很多位，这里不做处理，处理了使用就不灵活了！
function covArr(arr){
    var sumText=sumArr(arr);
    var covText=sumText/length;
    return covText
}
```
#### 2.9从数组中随机获取元素
```js
//randomOne([1,2,3,6,8,5,4,2,6])
//2
//randomOne([1,2,3,6,8,5,4,2,6])
//8
//randomOne([1,2,3,6,8,5,4,2,6])
//8
//randomOne([1,2,3,6,8,5,4,2,6])
//1
function randomOne(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
}
```
#### 2.10返回数组（字符串）一个元素出现的次数
```js
//getEleCount('asd56+asdasdwqe','a')
//3
//getEleCount([1,2,3,4,5,66,77,22,55,22],22)
//2
function getEleCount (obj, ele) {
    var num = 0;
    for (var i = 0, len = obj.length; i < len; i++) {
        if (ele == obj[i]) {
            num++;
        }
    }
    return num;
}
```
#### 2.11返回数组（字符串）出现最多的几次元素和出现次数
```js
//arr, rank->长度，默认为数组长度，ranktype，排序方式，默认降序
function getCount(arr, rank，ranktype){ 
    var obj = {}, k, arr1 = []
    //记录每一元素出现的次数
    for (var i = 0, len = arr.length; i < len; i++) {
        k = arr[i];
        if (obj[k]) {
            obj[k]++;
        }
        else {
            obj[k] = 1;
        }
    }
    //保存结果{el-'元素'，count-出现次数}
    for (var o in obj) {
        arr1.push({el: o, count: obj[o]});
    }
    //排序（降序）
    arr1.sort(function (n1, n2) {
        return n2.count - n1.count
    });
    //如果ranktype为1，则为升序，反转数组
    if(ranktype===1){
        arr1=arr1.reverse();
    }
    var rank1 = rank || arr1.length;
    return arr1.slice(0,rank1);
}
```
#### 2.12得到n1-n2下标的数组
```js
//getArrayNum([0,1,2,3,4,5,6,7,8,9],5,9)
//[5, 6, 7, 8, 9]

//getArrayNum([0,1,2,3,4,5,6,7,8,9],2) 不传第二个参数,默认返回从n1到数组结束的元素
//[2, 3, 4, 5, 6, 7, 8, 9]
function getArrayNum(arr,n1,n2){
    var arr1=[],len=n2||arr.length-1;
    for(var i=n1;i<=len;i++){
        arr1.push(arr[i])
    }
    return arr1;
}
```
#### 2.13筛选数组
```js
/删除值为'val'的数组元素
//removeArrayForValue(['test','test1','test2','test','aaa'],'test','%')
//["aaa"]   带有'test'的都删除
    
//removeArrayForValue(['test','test1','test2','test','aaa'],'test')
//["test1", "test2", "aaa"]  //数组元素的值全等于'test'才被删除
function removeArrayForValue(arr,val,type){
    arr.filter(function(item){return type==='%'?item.indexOf(val)!==-1:item!==val})
}
```
## 3.函数操作

#### 3.1判断是否是一个函数
```js
function isFunction(obj) {
   return Object.prototype.toString.call(obj)=== '[object Function]';
}
```
#### 3.2获取指定函数的函数名称（用于兼容IE）
```js
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
## 4.DOM操作
#### 4.1查询指定窗口的视口尺寸，如果不指定窗口，查询当前窗口尺寸
```js
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
#### 4.2获取指定window中滚动条的偏移量，如未指定则获取当前window
```js
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
#### 4.3检测对象是否有哪个类名
```js
function hasClass(obj,classStr){ 
    var arr=obj.className.split(/\s+/); //这个正则表达式是因为class可以有多个,判断是否包含 
    return (arr.indexOf(classStr)==-1)?false:true;
},
```
#### 4.4添加类名
```js
function addClass(obj,classStr){
    if (!this.hasClass(obj,classStr)){obj.className += " " + classStr};
},
```
#### 4.5删除类名
```js
function removeClass(obj,classStr){
    if (this.hasClass(obj,classStr)) {
        var reg = new RegExp('(\\s|^)' + classStr + '(\\s|$)');
        obj.className = obj.className.replace(reg, '');
    }
},
```
#### 4.6替换类名("被替换的类名","替换的类名")
```js
function replaceClass(obj,newName,oldName) {
    removeClass(obj,oldName);
    addClass(obj,newName);
}
```
#### 4.7获取兄弟节点
```js
function siblings(obj){
    var a=[];//定义一个数组，用来存o的兄弟元素 
    var p=obj.previousSibling; 
    while(p){//先取o的哥哥们 判断有没有上一个哥哥元素，如果有则往下执行 p表示previousSibling 
        if(p.nodeType===1){ 
        a.push(p); 
        } 
        p=p.previousSibling//最后把上一个节点赋给p 
    } 
    a.reverse()//把顺序反转一下 这样元素的顺序就是按先后的了 
    var n=obj.nextSibling;//再取o的弟弟 
    while(n){//判断有没有下一个弟弟结点 n是nextSibling的意思 
        if(n.nodeType===1){ 
            a.push(n); 
        } 
        n=n.nextSibling; 
    }
    return a;
},
```
#### 4.8设置样式
```js
function css(obj,json){
    for(var attr in json){
        obj.style[attr]=json[attr];
    }
}
```
#### 4.9设置文本内容
```js
function html(obj){
    if(arguments.length==0){
        return this.innerHTML;
    }
    else if(arguments.length==1){
        this.innerHTML=arguments[0];
    }
}
```
#### 4.10显示隐藏
```js
function show(obj){
    obj.style.display="";
}
function hide(obj){
    obj.style.display="none";
}
```

## 5.其他

#### 5.1使用!!操作符转换布尔值
有时候我们需要对一个变量查检其是否存在或者检查值是否有一个有效值，如果存在就返回`true`值。为了做这样的验证，我们可以使用`!!`操作符来实现是非常的方便与简单。对于变量可以使用`!!variable`做检测，只要变量的值为:`0`、`null`、`" "`、`undefined`或者`NaN`都将返回的是`false`，反之返回的是`true`。比如下面的示例：
```js
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
在这个示例中，只要`account.cash`的值大于`0`，那么`account.hasMoney`返回的值就是`true`。

#### 5.2cookie
```js
//cookie
//设置cookie
function setCookie(name,value,iDay){
    var oDate=new Date();
    oDate.setDate(oDate.getDate()+iDay);
    document.cookie=name+'='+value+';expires='+oDate;
}
//获取cookie
function getCookie(name){
    var arr=document.cookie.split('; ');
    for(var i=0;i<arr.length;i++){
        var arr2=arr[i].split('=');
        if(arr2[0]==name)
        {
            return arr2[1];
        }
    }
    return '';
}
//删除cookie
function removeCookie(name){
    setCookie(name,1,-1);
}
```
#### 5.3清除对象中值为空的属性
```js
//filterParams({a:"",b:null,c:"010",d:123})
//Object {c: "010", d: 123}
function filterParams(obj){
    let _newPar = {};
    for (let key in obj) {
        if ((obj[key] === 0 || obj[key]) && obj[key].toString().replace(/(^\s*)|(\s*$)/g, '') !== '') {
            _newPar[key] = obj[key];
        }
    }
    return _newPar;

```
#### 5.4现金额大写转换函数
```js
//upDigit(168752632)
//"人民币壹亿陆仟捌佰柒拾伍万贰仟陆佰叁拾贰元整"
//upDigit(1682)
//"人民币壹仟陆佰捌拾贰元整"
//upDigit(-1693)
//"欠人民币壹仟陆佰玖拾叁元整"
function upDigit(n)   
{  
    var fraction = ['角', '分','厘'];  
    var digit = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'];  
    var unit = [ ['元', '万', '亿'], ['', '拾', '佰', '仟']  ];  
    var head = n < 0? '欠人民币': '人民币';  
    n = Math.abs(n);  
    var s = '';  
    for (var i = 0; i < fraction.length; i++)   
    {
        s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, ''); 
    } 
    s = s || '整';  
    n = Math.floor(n);  
    for (var i = 0; i < unit[0].length && n > 0; i++)   
    {  
        var p = '';  
        for (var j = 0; j < unit[1].length && n > 0; j++)   
        {  
            p = digit[n % 10] + unit[1][j] + p; 
            n = Math.floor(n / 10);
        }
        //s = p.replace(/(零.)*零$/, '').replace(/^$/, '零')+ unit[0][i] + s; 
        s = p+ unit[0][i] + s;
    }
    return head + s.replace(/(零.)*零元/, '元').replace(/(零.)+/g, '零').replace(/^整$/, '零元整');
} 
```
#### 5.5获取，设置url参数
```js
//获取url参数
//getUrlPrmt('segmentfault.com/write?draftId=122000011938')
//Object{draftId: "122000011938"}
function getUrlPrmt(url) {
    url = url ? url : window.location.href;
    let _pa = url.substring(url.indexOf('?') + 1), _arrS = _pa.split('&'), _rs = {};
    for (let i = 0, _len = _arrS.length; i < _len; i++) {
        let pos = _arrS[i].indexOf('=');
        if (pos == -1) {
            continue;
        }
        let name = _arrS[i].substring(0, pos), value = window.decodeURIComponent(_arrS[i].substring(pos + 1));
        _rs[name] = value;
    }
    return _rs;
}

//设置url参数
//setUrlPrmt({'a':1,'b':2})
//a=1&b=2
function setUrlPrmt(obj) {
    let _rs = [];
    for (let p in obj) {
        if (obj[p] != null && obj[p] != '') {
            _rs.push(p + '=' + obj[p])
        }
    }
    return _rs.join('&');
}
```
#### 5.6随机返回一个范围的数字
```js
function randomNumber(n1,n2){
    //randomNumber(5,10)
    //返回5-10的随机整数，包括5，10
    if(arguments.length===2){
        return Math.round(n1+Math.random()*(n2-n1));
    }
    //randomNumber(10)
    //返回0-10的随机整数，包括0，10
    else if(arguments.length===1){
        return Math.round(Math.random()*n1)
    }
    //randomNumber()
    //返回0-255的随机整数，包括0，255
    else{
        return Math.round(Math.random()*255)
    }  
}
```
#### 5.7 随进产生颜色
```js
function randomColor(){
    //randomNumber是上面定义的函数
    //写法1
    return 'rgb(' + randomNumber(255) + ',' + randomNumber(255) + ',' + randomNumber(255) + ')';
    
    //写法2
    return '#'+Math.random().toString(16).substring(2).substr(0,6);
    
    //写法3
    var color='#';
    for(var i=0;i<6;i++){
        color+='0123456789abcdef'[randomNumber(15)];
    }
    return color;
}
```
#### 5.8 Date日期时间部分
```js
/到某一个时间的倒计时
//getEndTime('2017/7/22 16:0:0')
//"剩余时间6天 2小时 28 分钟20 秒"
function getEndTime(endTime){
    var startDate=new Date();  //开始时间，当前时间
    var endDate=new Date(endTime); //结束时间，需传入时间参数
    var t=endDate.getTime()-startDate.getTime();  //时间差的毫秒数
    var d=0,h=0,m=0,s=0;
    if(t>=0){
      d=Math.floor(t/1000/3600/24);
      h=Math.floor(t/1000/60/60%24);
      m=Math.floor(t/1000/60%60);
      s=Math.floor(t/1000%60);
    } 
    return "剩余时间"+d+"天 "+h+"小时 "+m+" 分钟"+s+" 秒";
}
```
#### 5.9 适配rem
```js
function getFontSize(){
    var doc=document,win=window;
    var docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
    recalc = function () {
        var clientWidth = docEl.clientWidth;
        if (!clientWidth) return;
        //如果屏幕大于750（750是根据我效果图设置的，具体数值参考效果图），就设置clientWidth=750，防止font-size会超过100px
        if(clientWidth>750){clientWidth=750}
        //设置根元素font-size大小
        docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
    };
    //屏幕大小改变，或者横竖屏切换时，触发函数
    win.addEventListener(resizeEvt, recalc, false);
    //文档加载完成时，触发函数
    doc.addEventListener('DOMContentLoaded', recalc, false);
}
//使用方式很简单，比如效果图上，有张图片。宽高都是100px;
//样式写法就是
img{
    width:1rem;
    height:1rem;
}
//这样的设置，比如在屏幕宽度大于等于750px设备上，1rem=100px；图片显示就是宽高都是100px
//比如在iphone6(屏幕宽度：375)上，375/750*100=50px;就是1rem=50px;图片显示就是宽高都是50px;
```
#### 5.10 封装成形
写了这么多的操作，小伙伴应该发现了一问题，全局函数太多了
```js
//这样的话，封装了几个操作，就增加了几个全局函数，污染了全局变量，在开发中应该尽量避免全局变量。不说别的，如果一个项目，几个人开发，很有可能会造成命名的冲突。

function setUrlPrmt(obj){..}
function getUrlPrmt(url){..}
function upsetArr(obj){..}


//所以，建议的封装姿势是
var myJS={
    setUrlPrmt:function(obj){..},
    getUrlPrmt:function(url){..},
    upsetArr:function(arr){..},
}
这样就算别人也写这样的函数,也不会造成冲突。全局变量也只有一个，加上别人也不会很多！
var otherJS={
    setUrlPrmt:function(obj){..},
    getUrlPrmt:function(url){..},
    upsetArr:function(arr){..},
}


//最后，封装的效果是
var myJS={
    //去除字符串空格
    trim:function(obj){..},
    //字母大小写切换
    changeCase:function(obj){..},
    //字符串循环复制
    repeatStr:function(str){..},
    .....
}

//如果是es6的模块化开发，大家也可以
let myJS={
    //去除字符串空格
    trim:function(obj){..},
    //字母大小写切换
    changeCase:function(obj){..},
    //字符串循环复制
    repeatStr:function(str){..},
    .....
}
//暴露模块，里面的方式大家也可以用es6方式实现，代码至少会少一点！
export {myJS}
```
> 可能有小伙伴会有疑问，这样封装，调用有点麻烦，为什么不直接在原型上面封装，调用方便。比如下面的栗子！
```js
String.prototype.trim=function(type){
    switch (type){
        case 1:return this.replace(/\s+/g,"");
        case 2:return this.replace(/(^\s*)|(\s*$)/g, "");
        case 3:return this.replace(/(^\s*)/g, "");
        case 4:return this.replace(/(\s*$)/g, "");
        default:return this;
    }
}
//'  12345 6 8 96  '.trim(1)
//"123456896"
//比这样trim('  12345 6 8 96  ',1)调用方便。
//但是，这样是不推荐的做法，这样就污染了原生对象String,别人创建的String也会被污染，造成不必要的开销。
//更可怕的是，万一自己命名的跟原生的方法重名了，就被覆盖原来的方法了
//String.prototype.substr=function(){console.log('asdasd')}  
//'asdasdwe46546'.substr()
//asdasd 
//substr方法有什么作用，大家应该知道，不知道的可以去w3c看下
```
所以在原生对象原型的修改很不推荐！至少很多的公司禁止这样操作！


## 本文收集来源
- [编写自己的代码库（javascript常用实例的实现与封装）](https://segmentfault.com/a/1190000010225928),[对应的GITHUB地址](https://github.com/chenhuiYj/ec-do/blob/master/ec-do.js)

