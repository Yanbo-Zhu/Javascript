函数：就是封装了一段可被重复调用执行的代码块。通过此代码块可以实现大量代码的重复使用。


# 1 Funktion 和 method 的区别
Function:
Function muss nicht  an einem Objekt gebunden sind 
Function kann ohne Klass, ohne Objekt  aufrufen kann  

可以直接使用 fn1(), 来 调用 fn()

Method:  
1 ein Method muss an einem Objekt gebunden sind. 
比如 要使用 objekt1.method1 (1,2)
不能 method1(1,2) ,不加 objekt1 , 是无法使用 method1 的


# 2 把整个函数打印出来 

```js
console.log(moodCheck()); // 把整个函数快都打印出来 
```

# 3 函数的使用
函数在使用时分为两步：声明函数和调用函数

## 3.1 声明函数
function 是声明函数的关键字,必须小写
由于函数一般是为了实现某个功能才定义的， 所以通常我们将函数名命名为动词，比如 getSum
```css
function fn() {...}
```


### 3.1.1 四种声明方式
1. 函数声明方式 function 关键字(命名函数)
    1. function fn() {...}
2. 函数表达式(匿名函数)
    2. var fn = function(){...};
3.  const num3 = () => {....}
4. new Function()
    1. var fn = new Function('参数1','参数2',.....,'函数体');
    2. Function 里面参数都必须是字符串格式
    3. 这种方式执行效率低，也不方便书写，因此较少使用

- 函数也属于对象
- 所有函数都是 Function 的实例(对象)
    - ![在这里插入图片描述](https://img-blog.csdnimg.cn/51f9b4f2353649d485ab68a68e2dfae7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5ZCE56eNX0RlbW8=,size_20,color_FFFFFF,t_70,g_se,x_16)


```js
   // function expression
    const squareNum2 = function(){
        let square = 2 * 2;
        return square;
    };

    // arrow functions
    const squareNum3 = () => {
        let square = 2 * 2;
        return square;
    }
```

```html
<body>
    <script>
        //  函数的定义方式

        // 1. 自定义函数(命名函数) 

        function fn() {};

        // 2. 函数表达式 (匿名函数)

        var fun = function() {};


        // 3. 利用 new Function('参数1','参数2', '函数体');
		//             Function 里面参数都必须是字符串格式，执行效率低，较少写

        var f = new Function('a', 'b', 'console.log(a + b)');
        f(1, 2);
        // 4. 所有函数都是 Function 的实例(对象)
        console.dir(f);
        // 5. 函数也属于对象
        console.log(f instanceof Object);
    </script>
</body>

```



### 3.1.2 声明方式: 自定义函数方式(命名函数)

利用函数关键字 function 自定义函数方式。
因为有名字，所以也被称为命名函数
调用函数的代码既可以放到声明函数的前面，也可以放在声明函数的后面

```js
//声明函数
function 函数名(){
     //函数体代码
}

function myFunc(par1, par2){

  //Programmblock, Anweisungen
  return Wert;
}
myFunc(42,"Hallo Welt"); //par1=42, par2="Hallo Welt"
```

```js
// 声明定义方式
function fn() {...}

// 调用  
fn();  


```


### 3.1.3 声明方式:  函数表达式方式(匿名函数)
利用函数表达式方式的写法如下：

因为函数没有名字，所以也称为匿名函数
这个fn 里面存储的是一个函数
函数调用的代码必须写到函数体后面

```js
// 这是函数表达式写法，匿名函数后面跟分号结束
var fn = function(){...};

let func = functions(par1){
 //Do something with par1
}

// 调用的方式，函数调用必须写到函数体下面
fn();
```

## 3.2 Immediately Invoked Function Expression
Funktionen können auch in einem Arbeitsgang deklariert und ausgeführt werden. Auch die IIFE gelten als Ausdruck.

```js
(function(e){
    return e;
})();

```



## 3.3 调用函数/Funktionsaufruf

函数名(); //通过调用函数名来执行函数体代码

调用的时候千万不要忘记添加小括号
口诀：函数不调用，自己不执行
注意：声明函数本身并不会执行代码，只有调用函数时才会执行函数体代码。


### 3.3.1 函数的调用方式
1. 普通函数
2. 对象的方法
3. 构造函数
4. 绑定事件函数
5. 定时器函数
6. 立即执行函数/Immediately invoked function expression/ LIFE

```html
<body>
    <script>
        // 函数的调用方式

        // 1. 普通函数
        function fn() {
            console.log('人生的巅峰');

        }
        // fn();   fn.call()
        
        // 2. 对象的方法
        var o = {
            sayHi: function() {
                console.log('人生的巅峰');

            }
        }
        o.sayHi();
        
        // 3. 构造函数
        function Star() {};
        new Star();
        
        // 4. 绑定事件函数
         btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
        
        // 5. 定时器函数
         setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
        
        // 6. 立即执行函数
        (function() {
            console.log('人生的巅峰');
        })();
        // 立即执行函数是自动调用, 这样的话就不用 后面的下一行, 再加一句 fn() 了
    </script>
</body>

```


## 3.4 引用函数/Funktionsreferenz
不加 () 使用函数

```js
// Funktionsdeklarationen werden gehoisted (an den Anfang des Skripts geschoben)
function squareTwo(){
    let square = 2;
    return square;
    // Funktionen ohne Rückgabewert liefern undefined
}

// Funktionsaufruf
console.log(squareTwo());

// Funktionsreferenz
squareTwo;
    
// Referenz in einer anderen Variablen speichern
    let takeSquareTwo = squareTwo;
    console.log(takeSquareTwo);
```

## 3.5 引用函数与调用函数的区别
https://blog.csdn.net/miao_9/article/details/76418984

引用函数与调用函数的差别与函数名称后是否附有括号()有关。函数引用只会单独出现，但函数调用则必定后随括号，很多时候还附有自变量。

- 函数与一般变量的差异，在于如何使用数据。与函数相关的数据（或代码）可被执行。
- 想执行函数时，就在函数名称后加上括号()，如果函数需要自变量，也要记得附加上。
- <mark>函数变量的值 ( var A = fn (a=1, b=2 )  ) 不是代码本身，而是指向存储代码的存储器位置的引用 </mark>

1
如下的代码：代码一和代码二分部是函数引用和函数调用的列子，返回都为true，代码三也是函数调用的列子，返回且为false

我们现在来理解下函数引用和函数调用的本质区别：
- 当引用函数时候，多个变量内存存储的是函数的相同的入口指针，因此对于同一个函数来讲，无论多少个变量引用，他们都是相等的，因为对于引用类型(对象，数组，函数等)都是比较的是内存地址，如果他们内存地址一样的话，说明是相同的；
- 但是对于函数调用来讲，
    - 比如代码三;每次调用的时候，都被分配一个新的内存地址，所以他们的内存地址不相同，因此他们会返回false，
    - 但是对于代码二来讲，我们看到他们没有返回函数，只是返回数值，他们比较的不是内存地址，而是比较值，所以他们的值相等，因此他们也返回true，

```js
// 函数引用 代码一
function f(){
    var x = 5;
    return x;
}
var a = f;
var b = f;

console.log(a===b); // true
// 函数调用 代码二
function f2() {
    var x = 5;
    return x;
}
var a2 = f2();
var b2 = f2();
console.log(a2 === b2);

// 函数调用 代码三
function f3(){
    var x = 5;
    return function(){
        return x;
    }
}
var a3 = f3();
var b3 = f3();
console.log(a3 === b3); // false
```

2 
我们也可以看看如下实列化一个对象的列子，他们也被分配到不同的内存地址，因此他们也是返回false的；如下代码测试：

```js
function F(){
    this.x = 5;
}
var a = new F();
var b = new F();
console.log(a === b); // false
```




# 4 函数的封装
函数的封装是把一个或者多个功能通过函数的方式封装起来，对外只提供一个简单的函数接口

# 5 函数的参数

## 5.1 形参和实参
行参 parameter: 
- 在声明函数时，可以在函数名称后面的小括号中添加一些参数，这些参数被称为形参，
- 形式上的参数 函数定义的时候 传递的参数 当前并不知道是什么
- 声明函数的时候，函数名括号里面的是形参，形参的默认值为 undefined
实参 argument: 
- 而在调用该函数时，同样也需要传递相应的参数，这些参数被称为实参。
- 调用函数的时候，函数名括号里面的是实参
- 实际上的参数 函数调用的时候 传递的参数 实参是传递给形参的

参数的作用 : 在函数内部某些值不能固定，我们可以通过参数在调用函数时传递不同的值进去
- 函数调用的时候实参值是传递给形参的
- 形参简单理解为:不用声明的变量
- 实参和形参的多个参数之间用逗号(,)分隔，

```js
// 带参数的函数声明
function 函数名(形参1, 形参2 , 形参3...) { // 可以定义任意多的参数，用逗号分隔
  // 函数体
}

// 带参数的函数调用
函数名(实参1, 实参2, 实参3...); 


例如：利用函数求任意两个数的和
// 声明函数
function getSum(num1,num2){
    console.log(num1+num2)
}

// 调用函数
getSum(1,3) //4
getSum(6，5) //11

```


## 5.2 形参和实参个数不匹配

|参数个数| 说明|
|--|--|
|实参个数等于形参个数|	输出正确结果|
|实参个数多于形参个数|	只取到形参的个数|
|实参个数小于形参个数|	多的形参定义为undefined，结果为NaN|

注意：在JavaScript中，形参的默认值是undefined

例子: 
```js
function sum(num1, num2) {
    console.log(num1 + num2);
}
sum(100, 200);             // 300，形参和实参个数相等，输出正确结果

sum(100, 400, 500, 700);   // 500，实参个数多于形参，只取到形参的个数

sum(200);                  // 实参个数少于形参，多的形参定义为undefined，结果为NaN
```


## 5.3 小结
- 函数可以带参数也可以不带参数
- 声明函数的时候，函数名括号里面的是形参，形参的默认值为 undefined
- 调用函数的时候，函数名括号里面的是实参
- 多个参数中间用逗号分隔
- 形参的个数可以和实参个数不匹配，但是结果不可预计，我们尽量要匹配




# 6 带 return 的函数

## 6.1 return语句
有的时候，我们会希望函数将值返回给调用者，此时通过使用 return 语句就可以实现。

- 在使用 return 语句时，函数会停止执行，并返回指定的值
- <mark>如果函数没有 return ，返回的值是 undefined</mark>

return 语句的语法格式如下：
```js

// 声明函数
function 函数名（）{
    ...
    return  需要返回的值;
}
// 调用函数
函数名();    // 此时调用函数就可以得到函数体内return 后面的值
```

```js
// 声明函数
function sum(){
    ...
    return  666;
}
// 调用函数
sum();      // 此时 sum 的值就等于666，因为 return 语句会把自身后面的值返回给调用者 
```


## 6.2 return 终止函数
return 语句之后的代码不被执行
```js
function add(num1，num2){
    //函数体
    return num1 + num2; // 注意：return 后的代码不执行
    alert('我不会被执行，因为前面有 return');
}
var resNum = add(21,6); // 调用函数，传入两个实参，并通过 resNum 接收函数返回值
alert(resNum);          // 27

```


## 6.3 return 的返回值

### 6.3.1 返回一个值
return 返回一个值。如果用逗号隔开多个值，以最后一个为准
```js
function add(num1，num2){
    //函数体
    return num1,num2;
}
var resNum = add(21,6); // 调用函数，传入两个实参，并通过 resNum 接收函数返回值
alert(resNum);          // 6
```

### 6.3.2 返回多个值

1. 使用数组的方式
```js
function getData()
{
  var names=new Array("oec2003","oec2004");
  return names;
}
function getNames()
{
  var names=getData();
  alert(getData()[0]); //返回oec2003
}
```


2.将数据封装在Json中返回
```js
function getData()
{
  var info={"name":"oec2003","age":"25"};
  return info;
}
function getInfo()
{
  var info=getData();
  var name=info["name"];
  var age=info["age"];
  alert("姓名："+name+" 年龄："+age);
}
```


3.通过对象的属性访问方法
```js
function add(a,b){
    var sum;
    var sub
    return{
      sum:a+b,
      sub:a-b
    }
  }
  var obj = add(5,2);
  console.log(obj.sum);
  console.log(obj.sub);


=========
在这种情况下， `const { age, name } = getDetails()`中的`age`和`name`的顺序不再重要，因为它们是命名参数。

const getDetails = () => {
  return { 
    age : 37 , 
    name : 'Flavio'
  }
}
 
const { age , name } = getDetails ()
```




## 6.4 小结
函数都是有返回值的

如果有 return ，则返回 return 后面的值
如果没有 return，则返回 undefined

## 6.5 break、continue、return 的区别

break ： 结束当前循环体(如 for、while)
continue ：跳出本次循环，继续执行下次循环(如for、while)
return ：不仅可以退出循环，还能够返回 return 语句中的值，同时还可以结束当前的函数体内的代码

## 6.6 回调函数例子
1.利用函数求任意两个数的最大值
```js
function getMax(num1, num2) {
    return num1 > num2 ? num1 : num2;
}
console.log(getMax(1, 2));
console.log(getMax(11, 2));
```


2.求数组 [5,2,99,101,67,77] 中的最大数值
```js
//定义一个获取数组中最大数的函数
function getMaxFromArr(numArray){
    var maxNum = numArray[0];
    for(var i = 0; i < numArray.length;i++){
        if(numArray[i]>maxNum){
            maxNum = numArray[i];
        }
    }
    return maxNum;
}
var arrNum = [5,2,99,101,67,77];
var maxN = getMaxFromArr(arrNum);  //这个实参是个数组
alert('最大值为' + maxN);
```


3.创建一个函数，实现两个数之间的加减乘除运算，并将结果返回
```js
var a = parseFloat(prompt('请输入第一个数'));
var b = parseFloat(prompt('请输入第二个数'));

function count(a,b){
    var arr = [a + b, a - b, a * b, a / b];
    return arr;
}
var result = count(a,b);
console.log(result)
```

1.利用函数封装方式，翻转任意一个数组
```js
function reverse(arr) {
    var newArr = [];
    for (var i = arr.length - 1; i >= 0; i--) {
        newArr[newArr.length] = arr[i];
    }
    return newArr;
}
var arr1 = reverse([1, 3, 4, 6, 9]);
console.log(arr1);

```


2.利用函数封装方式，对数组排序 – 冒泡排序
```js
function sort(arr) {
    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j+1]) { 
	            var temp = arr[j];
	            arr[j] = arr[j + 1]; 
	            arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
```




# 7 arguments对象的使用
当我们不确定有多少个参数传递的时候，可以用 arguments 来获取。在 JavaScript 中，arguments 实际上它是当前函数的一个内置对象。所有函数都内置了一个 arguments 对象，arguments 对象中存储了传递的所有实参。

arguments存放的是传递过来的实参
arguments展示形式是一个伪数组，因此可以进行遍历。伪数组具有以下特点

1. 具有 length 属性
2. 按索引方式储存数据
3. 不具有数组的 push , pop 等方法

```js
// 函数声明
function fn() {
    console.log(arguments);  //里面存储了所有传递过来的实参
    console.log(arrguments.length); // 3
    console.log(arrguments[2]); // 3
}

// 函数调用
fn(1,2,3);
```


例如：利用函数求任意个数的最大值
```js
function maxValue() {
    var max = arguments[0];
    for (var i = 0; i < arguments.length; i++) {
        if (max < arguments[i]) {
            max = arguments[i];
        }
    }
    return max;
}
console.log(maxValue(2, 4, 5, 9)); // 9
console.log(maxValue(12, 4, 9)); // 12
```


打印参数
```js
function funcArgs(x,y,z){
    let args = "";
    // console.log(arguments);
    for(let i=0; i<arguments.length; i++){
        args += arguments[i];
    }
    console.log(args);
    // Versuchen Sie sich den Typ der Parameter ausgeben zu lassen mit typeof
}
```

## 7.1 



# 8 函数块内 调用另外一个函数
因为每个函数都是独立的代码块，用于完成特殊任务，因此经常会用到函数相互调用的情况。具体演示在下面的函数练习中会有。

3.输入一个年份，判断是否是闰年（闰年：能被4整除并且不能被100整数，或者能被400整除）
```js
function isRun(year) {
     var flag = false;
     if (year % 4 === 0 && year % 100 !== 0 || year % 400 === 0) {
        flag = true;
     }
    return flag;
}
console.log(isRun(2010));
console.log(isRun(2012));
```


4.用户输入年份，输出当前年份2月份的天数，如果是闰年，则2月份是 29天， 如果是平年，则2月份是 28天
```js
function backDay() {
    var year = prompt('请您输入年份:');
    if (isRun(year)) { //调用函数需要加小括号
        alert('你输入的' + year + '是闰年，2月份有29天');
    } else {
        alert('您输入的' + year + '不是闰年，2月份有28天');
    }
}
backDay();
//判断是否是闰年的函数
function isRun(year) {
    var flag = false;
    if (year % 4 === 0 && year % 100 !== 0 || year % 400 === 0) {
        flag = true;
    }
    return flag;
}
```

