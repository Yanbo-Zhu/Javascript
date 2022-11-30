# 1 引子
首先来看几段代码和结果：

1
console.log(num);  // 结果是多少？
//会报错 num is undefined

2
console.log(num);  // 结果是多少？
var num = 10;   
// undefined

3 
// 命名函数(自定义函数方式):若我们把函数调用放在函数声明上面
fn();				//11
function fn() {
    console.log('11');
}

4 
// 匿名函数(函数表达式方式):若我们把函数调用放在函数声明上面
fn();
var  fn = function() {
    console.log('22'); // 报错
}


//相当于执行了以下代码
var fn;
fn();      //fn没赋值，没这个，报错
var  fn = function() {
    console.log('22'); //报错
}


JavaScript 代码是由浏览器中的 JavaScript 解析器来执行的。JavaScript 解析器在运行 JavaScript 代码的时候分为两步：预解析和代码执行。
- <mark> 预解析：js引擎会把js里面所有的 var 还有 function 提升到当前作用域的最前面</mark> 
- 代码执行：从上到下执行JS语句

预解析只会发生在通过 var 定义的变量和 function 上。学习预解析能够让我们知道为什么在变量声明之前访问变量的值是 undefined，为什么在函数声明之前就可以调用函数。

# 2 变量预解析(变量提升)
变量预解析也叫做变量提升、

变量提升: 变量的声明会被提升到当前作用域的最上面，变量的赋值不会提升
```js
console.log(num);  // 结果是多少？
var num = 10;   
// 结果是 undefined



//相当于执行了以下代码
var num;		// 变量声明提升到当前作用域最上面
console.log(num);
num = 10;		// 变量的赋值不会提升
```


# 3 函数预解析(函数提升)
函数提升： 函数的声明会被提升到当前作用域的最上面，但是不会调用函数。

```js
fn();				//11
function fn() {
    console.log('11');
}
```



# 4 解决函数表达式声明调用问题
对于函数表达式声明调用需要记住：函数表达式调用必须写在函数声明的下面

// 匿名函数(函数表达式方式):若我们把函数调用放在函数声明上面
fn();
var  fn = function() {
    console.log('22'); // 报错
}


//相当于执行了以下代码
var fn;
fn();      //fn没赋值，没这个，报错
var  fn = function() {
    console.log('22'); //报错
}


# 5 预解析练习
预解析部分十分重要，可以通过下面4个练习来理解。
Pink老师的视频讲解预解析：https://www.bilibili.com/video/BV1Sy4y1C7ha?p=143

练习1: 
```js
var num = 10;
fun();
function fun() {
    console.log(num);	//undefined
    var num = 20;
}
// 最终结果是 undefined


// 上述代码相当于执行了以下操作

var num;
function fun() {
    var num;
    console.log(num);
    num = 20;
}
num = 10;
fun();

```



练习2
```js
var num = 10;
function fn(){
    console.log(num);		//undefined
    var num = 20;
    console.log(num);		//20
}
fn();
// 最终结果是 undefined 20

// 上述代码相当于执行了以下操作

var num;
function fn(){
    var num;
    console.log(num);
    num = 20;
    console.log(num);
}
num = 10;
fn();
```


// 练习3
```js
var a = 18;
f1();

function f1() {
    var b = 9;
    console.log(a);
    console.log(b);
    var a = '123';
}

//上述代码相当于执行了以下操作
var a;
function f1() {
    var b;
    var a
    b = 9;
    console.log(a);	//undefined
    console.log(b);	//9
    a = '123';
}
a = 18;
f1();
```


练习4
```js
f1();
console.log(c);
console.log(b);
console.log(a);
function f1() {
    var a = b = c = 9;
    // 相当于 var a = 9; b = 9;c = 9;  b和c的前面没有var声明,当全局变量看
    // 集体声明 var a = 9,b = 9,c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}

//上述代码相当于执行了以下操作

function f1() {
    var a;
    a = b = c = 9;
    console.log(a);	//9
    console.log(b);	//9
    console.log(c);	//9
}
f1();
console.log(c);	//9
console.log(b);	//9
console.log(a);	//报错 a是局部变量
```

