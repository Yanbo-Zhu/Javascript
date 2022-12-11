# 1 引子

JavaScript 代码是由浏览器中的 JavaScript 解析器来执行的。JavaScript 解析器在运行 JavaScript 代码的时候分为两步：预解析和代码执行。
- <mark> 预解析：js引擎会把js里面所有的 var 还有 function 提升到当前作用域的最前面</mark> 
- 代码执行：从上到下执行JS语句

预解析只会发生在
- 通过 var 定义的变量
    - 通过 b = 1 定义的 b, 不会被预解析, 因为前面没有 var 
- 用 命名函数的方式 声明 的 function 上
    - 用匿名函数 声明的 function 不会被预解析 
- 
学习预解析能够让我们知道为什么在变量声明之前访问变量的值是 undefined，为什么在函数声明之前就可以调用函数。

首先来看几段代码和结果：

```js
1
console.log(num);  // 结果是多少？
//会报错 num is undefined

2
console.log(num);  // 结果是多少？
var num = 10;   
// 不报错, 得到 undefined


//相当于执行了以下代码
var num 
console.log(num);  // 不报错, 得到 undefined
num = 10 

3 
// 命名函数(自定义函数方式):若我们把函数调用放在函数声明上面
fn();				//得到 11
function fn() {
    console.log('11');
}

4 
// 匿名函数(函数表达式方式):若我们把函数调用放在函数声明上面
fn(); // 报错
var  fn = function() {
    console.log('22'); 
}

//相当于执行了以下代码
var fn;
fn();      //fn没赋值，没这个，报错
var  fn = function() {
    console.log('22'); //报错
}
```


# 2 英语对应
变量提升
keine hoisting的意思是 : 不用先定义后使用, funtion 可以, 先 ausfuhre, 然后在下一行 进行 这个 funtion 的 decalre 
Funktion ist hoisted 的意思是: funktion 已经在前面先被定义了, 然后再 之后的行中被使用了 

# 3 变量预解析(变量提升 )
变量预解析也叫做变量提升


变量提升: 变量的声明会被提升到当前作用域的最上面，
只是变量的声明 会被提升. 变量的赋值不会提升

```js
console.log(num);  // 结果是多少？
var num = 10;   
// 结果是 undefined


//相当于执行了以下代码
var num;		// 变量声明提升到当前作用域最上面
console.log(num);
num = 10;		// 变量的赋值不会提升
```


# 4 函数预解析(函数提升,gehoisted, hositing)
函数提升： 函数的声明会被提升到当前作用域的最上面，但是不会调用函数。

Funktionsdeklarationen werden gehoisted (an den Anfang des Skripts geschoben)

```js
fn();				//11
function fn() {
    console.log('11');
}

// 相当于
function fn() {  // 这个被提到了前面 
    console.log('11');
}
fn();
```


# 5 解决 用匿名声明 出来的函数的 调用问题
对于函数表达式声明调用需要记住：函数表达式调用必须写在函数声明的下面

必须写成
```js
// 匿名函数(函数表达式方式)
var  fn = function() {
    console.log('22'); // 报错
}
fn();

```

不然就会出现问题: 
```js
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
```


# 6 预解析练习
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
    var num;  // 因为 每一个 函数块内都是scope,  内部和外部的 参数 不一样.  因为 有 var num = 20; num 在这个作用域块内 会被预解析.   所以这里会生成一个定义的 num, 但是没有值 
    console.log(num); 
    num = 20;
    console.log(num);
}
num = 10;
fn(); // num = 10;并没有传到 fu() 中. num 也不是 fn() 的 参数
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
    var b;   // 因为 每一个 函数块内都是scope,  内部和外部的 参数 不一样. 因为有 var b = 9 , b 在这个作用域块内 会被预解析 ,  所以这里会生成一个定义的 b, 但是没有值 
    var a  //  // 因为 每一个 函数块内都是scope,  内部和外部的 参数 不一样. 因为有  var a = '123' , b 在这个作用域块内 会被预解析 ,  所以这里会生成一个定义的 b, 但是没有值 
    b = 9;
    console.log(a);	//undefined
    console.log(b);	//9
    a = '123';
}
a = 18;
f1();  // a = 18;并没有传到 fu() 中. a 也不是 fn() 的 参数
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
    var a;  // 只有 a 被预解析.   b c 使用的是 b = 9;c = 9; b和c的前面没有var声明,所以不会被预解析 
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

