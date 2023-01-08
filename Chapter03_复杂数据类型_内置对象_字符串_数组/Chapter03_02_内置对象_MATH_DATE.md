
# 3 内置对象
JavaScript 中的对象分为3种：自定义对象 、内置对象、 浏览器对象
内置对象就是指 JS 语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本而必要的功能
JavaScript 提供了多个内置对象：Math、 Date 、Array、String等

学习一个内置对象的使用，只要学会其常用成员的使用即可，我们可以通过查文档学习，可以通过MDN/W3C来查询
MDN: https://developer.mozilla.org/zh-CN/

查阅该方法的功能
查看里面参数的意义和类型
查看返回值的意义和类型
通过 demo 进行测试


# 1 Math对象
Math 对象不是构造函数，它具有数学常数和函数的属性和方法。跟数学相关的运算（求绝对值，取整、最大值等）可以使用 Math 中的成员。

// Math数学对象，不是一个构造函数，所以我们不需要new 来调用，而是直接使用里面的属性和方法即可

Math.PI		 			// 圆周率
Math.floor() 	 		// 向下取整
Math.ceil()             // 向上取整
Math.round()            // 四舍五入版 就近取整   注意 -3.5   结果是  -3 
Math.abs()		 		// 绝对值
Math.max()/Math.min()	// 求最大和最小值 
注意：上面的方法必须带括号


console.log(Math.PI);  
console.log(Math.max(1,99,3)); // 99


## 1.1 练习：封装自己的数学对象

利用对象封装自己的数学对象，里面有PI 最大值 和最小值
```js
var myMath = {
    PI: 3.141592653,
    max: function() {
        var max = arguments[0];
        for (var i = 1; i < arguments.length; i++) {
            if (arguments[i] > max) {
                max = arguments[i];
            }
        }
        return max;
    },
    min: function() {
        var min = arguments[0];
        for (var i = 1; i < arguments.length; i++) {
            if (arguments[i] < min) {
                min = arguments[i];
            }
        }
        return min;
    }
}
console.log(myMath.PI);
console.log(myMath.max(1, 5, 9));
console.log(myMath.min(1, 5, 9));
```



## 1.2 Math绝对值和三个取整方法
Math.abs() 取绝对值
三个取整方法：
Math.floor() : 向下取整
Math.ceil() : 向上取整
Matg.round() : 四舍五入，其他数字都是四舍五入，但是5特殊，它往大了取

```js
//1.绝对值方法
console.log(Math.abs(1));  // 1
console.log(Math.abs(-1)); // 1
console.log(Math.abs('-1')); // 1 隐式转换，会把字符串 -1 转换为数字型


//2.三个取整方法
console.log(Math.floor(1.1)); // 1 向下取整，向最小的取值 floor-地板
console.log(Math.floor(1.9)); //1

console.log(Math.ceil(1.1)); //2 向上取整，向最大的取值 ceil-天花板
console.log(Math.ceil(1.9)); //2 

//四舍五入 其他数字都是四舍五入，但是5特殊，它往大了取
console.log(Math.round(1.1)); //1 四舍五入
console.log(Math.round(1.5)); //2
console.log(Math.round(1.9)); //2
console.log(Math.round(-1.1)); // -1
console.log(Math.round(-1.5)); // -1
```


## 1.3 随机数方法random()
random() 方法可以随机返回一个小数，其取值范围是 `[0，1)，左闭右开 0 <= x < 1`
得到一个两数之间的随机整数，包括第一个数，不包括第二个数

```js
// 得到两个数之间的随机整数，并且包含这两个整数
function getRandom(min,max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(getRandom(1,10));
```


1.随机点名
var arr = ['张三', '李四','王五','秦六']；
console.log(arr[getRandom(0,arr.length - 1)]);


2.猜数字游戏
![在这里插入图片描述](https://img-blog.csdnimg.cn/c1bd0e00171448ab8ec5af0763dd9cf2.png#pic_center)
```js
function getRandom(min,max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
var random = getRandom(1,10);
while(true) { //死循环 ，需要退出循环条件
     var num = prompt('请输入1~10之间的一个整数:');
     if(num > random) {
         alert('你猜大了');
     }else if (num < random) {
         alert('你猜小了');
     }else {
         alert('你猜中了');
         break; //退出整个循环
     }
}
```


# 2 Date日期对象
Date 对象和 Math 对象不一样，他是一个构造函数，所以我们需要实例化后才能使用

Date 实例用来处理日期和时间

## 2.1 Date()方法的使用
### 2.1.1 获取当前时间必须实例化
var now = new Date();
console.log(now);

### 2.1.2 Date()构造函数的参数
如果括号里面有时间，就返回参数里面的时间。例如日期格式字符串为 ‘2019-5-1’，可以写成new Date('2019-5-1') 或者 new Date('2019/5/1')

如果Date()不写参数，就返回当前时间
如果Date()里面写参数，就返回括号里面输入的时间

```js
// 1.如果没有参数，返回当前系统的当前时间
var now = new Date();
console.log(now);


// 2.参数常用的写法 数字型 2019,10,1  字符串型 '2019-10-1 8:8:8' 时分秒
// 如果Date()里面写参数，就返回括号里面输入的时间 
var data = new Date(2019,10,1);
console.log(data);  // 返回的是11月不是10月

var data2 = new Date('2019-10-1 8:8:8');
console.log(data2);

```


## 2.2 日期格式化
我们想要 2019-8-8 8:8:8 格式的日期，要怎么办？

需要获取日期指定的部分，所以我们要手动的得到这种格式

|方法名	|说明	|代码|
|--|--|--|
|getFullYear()	|获取当年|	dObj.getFullYear()|
|getMonth()	|获取当月(0-11)	|dObj.getMonth()|
|getDate()	|获取当天日期	|dObj.getDate()|
|getDay()	|获取星期几(周日0到周六6)|	dObj.getDay()|
|getHours()	|获取当前小时	|dObj.getHours()|
|getMinutes()	|获取当前小时|	dObj.getMinutes()|
|getSeconds()	|获取当前秒钟|	dObj.gerSeconds()|


```js
var date = new Date();
console.log(date.getFullYear()); // 返回当前日期的年 2019
console.log(date.getMonth() + 1);  //返回的月份小一个月 记得月份 +1
console.log(date.getDate); //返回的是几号
console.log(date.getDay());  //周一返回1 周6返回六 周日返回0



// 写一个 2019年 5月 1日 星期三
var date = new Date(); 
var year =  date.getFullYear();
var month = date.getMonth() + 1;
var dates = date.getDate();
console.log('今天是' + year +'年' + month + '月' + dates +'日' );

// 封装一个函数返回当前的时分秒 格式 08:08:08
function getTimer() {
    var time = new Date();
    var h = time.getHours();
    h = h < 10 ? '0' + h : h;
    var m = time.getMinutes();
    m = m < 10 ? '0' + m : m;
    var s = time.getSeconds();
    s = s < 10 ? '0' + s : s;
    return h + ':' + m + ':' + s;
}
console.log(getTimer());

```



## 2.3 获取日期的总的毫秒形式
date.valueOf() ：得到现在时间距离1970.1.1总的毫秒数
date.getTime() ：得到现在时间距离1970.1.1总的毫秒数

```js
// 获取Date总的毫秒数 不是当前时间的毫秒数 而是距离1970年1月1号过了多少毫秒数

// 实例化Date对象
var date = new Date();

// 1 .通过 valueOf()  getTime() 用于获取对象的原始值
console.log(date.valueOf());  //得到现在时间距离1970.1.1总的毫秒数
console.log(date.getTime());

// 2.简单的写法
var date1 = +new Date();  // +new Date()返回的就是总的毫秒数，
console.log(date1);

// 3. HTML5中提供的方法 获得总的毫秒数 有兼容性问题
console.log(Date.now());
```


🔥倒计时效果
```js
function countDown(time) {
    var nowTime = +new Date(); //没有参数，返回的是当前时间总的毫秒数
    var inputTime = +new Date(time); // 有参数，返回的是用户输入时间的总毫秒数
    var times = (inputTime - nowTime) / 1000; //times就是剩余时间的总的秒数

    var d = parseInt(times / 60 / 60 / 24); //天数
    d < 10 ? '0' + d : d;
    var h = parseInt(times / 60 / 60 % 24); //小时
    h < 10 ? '0' + h : h;
    var m = parseInt(times / 60 % 60); //分
    m < 10 ? '0' + m : m;
    var s = parseInt(times % 60); //秒
    s < 10 ? '0' + s : s;
    return d + '天' + h + '时' + m + '分' + s + '秒';
}
console.log(countDown('2020-11-09 18:29:00'));
var date = new Date;
console.log(date); //现在时间
```
