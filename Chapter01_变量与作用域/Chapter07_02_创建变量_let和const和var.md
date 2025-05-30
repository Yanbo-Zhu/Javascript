
https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/

# 1 总览


## 1.1 let,const, var的德语解析 

- Seit Version 6 von ECMAScript können Variablen mit den Schlüsselwörtern `**let**` und `**const**` deklariert werden
- `**let**` deklariert Variablen auf Blockebene werden, d.h. der Scope der Variablen wird durch den umgebenden Block gebildet
- Außerhalb des umgebenden Blockes ist eine mit `**let**` deklarierte Variable nicht zugreifbar
- Traditionelle Deklaration von Variablen (vor Version 6) mit `**var**`
- `**var**` hat keinen Block-Scope
- Mit `**const**` können nicht veränderbare Variablen (_Konstanten_) deklariert werden, deren Scope durch den umgebenden Block gegeben ist


In JavaScript, im Gegensatz zu z.B. Java oder C, müssen wir uns keine Gedanken darüber machen, welchen Typ unsere Variable hat. Wir müssen keine int oder long vor Zahlen, double oder float vor Gleitkommazahlen setzen.

In JavaScript gibt es drei Arten von Variablen: `var`, `let` und `const`. Sie können alle Datentypen speichern. Wir können schreiben zum Beispiel: `const x = 1`, `const haha = 'haha'`, `const arr = [true, true, 'Pferd']`, usw. Es gibt jedoch einen wesentlichen Unterschied zwischen diesen Variablentypen:

1 let
let weist einer Variable einen Wert zu, der geändert werden kann. Wir können sie zunächst deklarieren und später initialisieren.

let 的variable , 
同一个variable name 不能被 多次 deklaiert werden 

```js
let number = 1;
let string = "IntroProg";
let bool;

number = 99;
string = "Webtechnologien";
bool = 1 > 3;

console.log(number); // 99
console.log(string); // Webtechlogien
console.log(bool); // false
```


2 const
const weist einer Variable einen Wert zu, der nicht geändert werden kann (ähnlich wie eine final-Variable in Java). Die Deklaration muss sofort zusammen mit der Initialisierung erfolgen.
```js
const num = 12;
const str = "hello world";
const arr = [true, false, true, false];

const num2; // 'const' declarations must be initialized.ts(1155)
num2 = 41;  // 'const' declarations must be initialized.ts(1155)

const age = 25;
age = 26;   // Cannot redeclare block-scoped variable 'age'.ts(2451)
```


3 var
var ist “problematisch“. Es kann zunächst deklariert und später wie let initialisiert werden. Der Wert kann ebenfalls geändert werden. ==Was es jedoch von let unterscheidet, ist, dass es mehrmals deklariert werden kann.==
每次被deklarieren, 之前的vararibale 地址都丢失了, 
新的地址被分配给他 

```js
var myVar = 3;
console.log(myVar); // 3

myVar = "haha";
console.log(myVar); // haha

var myVar = true;
console.log(myVar); // true

```


## 1.2 let、const、var 的总览


| ?                    | var    | let     | const   |
| -------------------- | ------ | ------- | ------- |
| scope                | 函数级作用域 | 块级作用域   | 块级作用域   |
| 预解析 gehoisten, Hoist | 变量提升   | 不存在变量提升 | 不存在变量提升 |
| 值的变化                 | 值可更改   | 值可更改    | 值不可更改   |

1. 使用var声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象。  die Variable ist gültig in der Funktion, in der sie deklariert wird
2. 使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升。 die Variable ist gültig in dem Anweisungsblock, in dem sie deklariert wird
3. 使用 const 声明的常量，在后面出现的代码中不能修改该常量的值。  die Variable hat einen festen unveränderlichen Wert


- `var` declarations are globally scoped or function scoped while `let` and `const` are block scoped.
- `var` variables can be updated and re-declared within its scope; `let` variables can be updated but not re-declared; `const` variables can neither be updated nor re-declared.
- They are all hoisted to the top of their scope. But while `var` variables are initialized with `undefined`, `let` and `const` variables are not initialized.
- While `var` and `let` can be declared without being initialized, `const` must be initialized during declaration.


### 1.2.1 let、const与var的区别
1. let和const不能重复声明变量
```js
         var num = 100;
         var num = 100;

         let num = 100;
         let num = 100;//会报错

         const num = 100;
         const num = 100;//会报错

```
2. let和const定义的变量是块级作用域，会被{}限制作用范围
```js
0 
function guess(event) {
    let counter = 0;
        if (life > 0) {
            for (var j = 0; j < answer.length; j++) {
                if (guessWord === answerArray[j]) {
                    counter += 1;   // 此处 counter 不会报错, 会继续用 let counter = 0 处 对 counter 的定义
                }
            }
}


1 
 {
     let num = 100
     console.log(num)
 }
 console.log(num)//会报错

    function outside(){
        // statement
        function inside(){
            let n = 0;
        }
        n = 5; // 此处会报错, 因为  let n = 0; n的效力 值存在于 {} 之内. 所以  n = 5 这里, n 等于之前根本就没有被定义 
    }

2 
 {
     const num = 100
     console.log(num);
 }
 console.log(num);//会报错

```
3. let和const没有预解析
        console.log(num)
        var num = 100;
        let num = 100;//会报错
        const num = 100;//会报错


## 1.3 let和const总结

1. let 声明的变量会产生块作用域，var 不会产生块作用域
2. const 声明的常量也会产生块作用域
3. 不同代码块之间的变量无法互相访问
4. 注意: 对象属性修改和数组元素变化不会出发 const 错误 （数组和对象存的是引用地址）
5. 应用场景：声明对象类型使用 const，非对象类型声明选择 let
6. cosnt声明必须赋初始值，标识符一般为大写，值不允许修改。

### 1.3.1 什么时候用 let，什么使用用 const

原则：如果不知道用什么的时候，就用 const

原因：如果应该是常量，那么刚好符合需求。如果应该是变量，那么后来报错时，再来改为变量也为时不晚。同时，一开始就设置为常量还会避免真的需要为常量时，该值在后来被意外修改的情况。

### 1.3.2 let与const的区别
1.let可以重复赋值，const不可以重复赋值
        let num = 100;
        num = 200;

        const num = 100;
        num = 200;//会报错

2.let定义的时候可以不赋值，const定义的时候就要赋值
       let num;
       const num;//会报错


## 1.4 var


### 1.4.1 scope of var 


The scope is global when a `var` variable is declared outside a function. This means that any variable that is declared with `var` outside a function block is available for use in the whole window.

`var` is function scoped when it is declared within a function. This means that it is available and can be accessed only within that function.


```javascript


var tester = "hey hi";

function newFunction() {
    var hello = "hello";
}
console.log(hello); // error: hello is not defined

```


### 1.4.2 var variables can be re-declared and updated

This means that we can do this within the same scope and won't get an error.

```js

var greeter = "hey hi";
var greeter = "say Hello instead";


var greeter = "hey hi";
greeter = "say Hello instead";


```



### 1.4.3 Hoisting of var 变量提升 


Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. This means that if we do this:

```js
console.log (greeter);
var greeter = "say hello"

//it is interpreted as this:
//So var variables are hoisted to the top of their scope and initialized with a value of undefined.
var greeter;
console.log(greeter); // greeter is undefined
greeter = "say hello"

```


### 1.4.4 Problem with var

There's a weakness that comes with var. I'll use the example below to explain:

```
    var greeter = "hey hi";
    var times = 4;

    if (times > 3) {
        var greeter = "say Hello instead"; 
    }

    console.log(greeter) // "say Hello instead"
```


So, since `times > 3` returns true, `greeter` is redefined to `"say Hello instead"`. While this is not a problem if you knowingly want `greeter` to be redefined, it becomes a problem when you do not realize that a variable `greeter` has already been defined before.

If you have used `greeter` in other parts of your code, you might be surprised at the output you might get. This will likely cause a lot of bugs in your code. This is why `let` and `const` are necessary.


## 1.5 let 命令

`let` is now preferred for variable declaration. It's no surprise as it comes as an improvement to `var` declarations. 
It also solves the problem with `var` that we just covered. Let's consider why this is so.



1、变量声明
let a;
let b,c,d;
let e=100;
let f=342,g='fgsddgf',h=[];

### 1.5.1 特点
1. 变量不能重复声明，下面代码就会报错
    1. let star='df'; let star='ff';
2. let 声明的变量只在所处于的块级有效: 块级作用域（只在{}里面有效）、全局、函数、evel
    1. 注意：使用let 关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性
3. 不存在变量提升
```js
1
//下面就不会报错
console.log(song);
var song='wer';
//下面就会报错
console.log(song);
let song='wer';

2
console.log(a);  // a is not defined
let a = 20;   
```

4. 暂时性死区

```js
var tmp = 123;
if (true) {
    tmp = 'abc';
    let tmp;
}
```


### 1.5.2 为块级作用域

ES6 新增了`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效。
使用let 关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性

```js
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

上面代码在代码块之中，分别用`let`和`var`声明了两个变量。然后在代码块之外调用这两个变量，结果`let`声明的变量报错，`var`声明的变量返回了正确的值。这表明，`let`声明的变量只在它所在的代码块有效。

`for`循环的计数器，就很合适使用`let`命令。

```js
for (let i = 0; i < 10; i++) {
  // ...
}

console.log(i);
// ReferenceError: i is not defined
```

上面代码中，计数器`i`只在`for`循环体内有效，在循环体外引用就会报错。

下面的代码如果使用`var`，最后输出的是`10`。

```js
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```

上面代码中，变量`i`是`var`命令声明的，在全局范围内都有效，所以全局只有一个变量`i`。每一次循环，变量`i`的值都会发生改变，而循环内被赋给数组`a`的函数内部的`console.log(i)`，里面的`i`指向的就是全局的`i`。也就是说，所有数组`a`的成员里面的`i`，指向的都是同一个`i`，导致运行时输出的是最后一轮的`i`的值，也就是 10。

如果使用`let`，声明的变量仅在块级作用域内有效，最后输出的是 6。

```js
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```

上面代码中，变量`i`是`let`声明的，当前的`i`只在本轮循环有效，所以每一次循环的`i`其实都是一个新的变量，所以最后输出的是`6`。你可能会问，如果每一轮循环的变量`i`都是重新声明的，那它怎么知道上一轮循环的值，从而计算出本轮循环的值？这是因为 JavaScript 引擎内部会记住上一轮循环的值，初始化本轮的变量`i`时，就在上一轮循环的基础上进行计算。

另外，`for`循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

```js
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```

上面代码正确运行，输出了 3 次`abc`。这表明函数内部的变量`i`与循环变量`i`不在同一个作用域，有各自单独的作用域（同一个作用域不可使用 `let` 重复声明同一个变量）。

---

So a variable declared in a block with `let` is only available for use within that block. Let me explain this with an example:

```javascript
   let greeting = "say Hi";
   let times = 4;

   if (times > 3) {
        let hello = "say Hello instead";
        console.log(hello);// "say Hello instead"
    }
   console.log(hello) // hello is not defined
```






### 1.5.3 不存在变量提升

> Just like `var`, `let` declarations are hoisted to the top. Unlike `var` which is initialized as `undefined`, the `let` keyword is not initialized. So if you try to use a `let` variable before declaration, you'll get a `Reference Error`.

`var`命令会发生“变量提升”现象，即变量可以在声明之前使用，值为`undefined`。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。

为了纠正这种现象，`let`命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

```js
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

上面代码中，变量`foo`用`var`命令声明，会发生变量提升，即脚本开始运行时，变量`foo`已经存在了，但是没有值，所以会输出`undefined`。变量`bar`用`let`命令声明，不会发生变量提升。这表示在声明它之前，变量`bar`是不存在的，这时如果用到它，就会抛出一个错误。

### 1.5.4 暂时性死区

只要作用域内存在 let、const，它们所声明的变量或常量就自动 “绑定” 这个区域，不再受到外部作用域的影响。

```javascript
let a = 2;
function func() {
    console.log(a);        // 报错
    let a = 1;
}
func();
```

```javascript
let a = 2;
function func() {
    console.log(a);        // 2
}
func();
```

**即：只要作用域内出现了同名的 let 或 const，那么就会去找这个量（向前找），如果找不到也不会跳去外部找，只会直接报错！**

> 只要我们遵守 “**先声明后使用**”，那么其实就基本不会遇到变量提升及暂时性死区问题。

### 1.5.5 不允许重复声明 (let can be updated but not re-declared.)

Just like `var`, a variable declared with `let` can be updated within its scope. Unlike `var`, a `let` variable cannot be re-declared within its scope. So while this will work:


```js
let greeting = "say Hi";
greeting = "say Hello instead";  // 不报错 

//this will return an error:
let greeting = "say Hi";
let greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared

```


However, if the same variable is defined in different scopes, there will be no error:
```javascript
    let greeting = "say Hi";
    if (true) {
        let greeting = "say Hello instead";
        console.log(greeting); // "say Hello instead"
    }
    console.log(greeting); // "say Hi"
```

Why is there no error? This is because both instances are treated as different variables since they have different scopes.

This fact makes `let` a better choice than `var`. When using `let`, you don't have to bother if you have used a name for a variable before as a variable exists only within its scope.

Also, since a variable cannot be declared more than once within a scope, then the problem discussed earlier that occurs with `var` does not happen.



-----

`let`不允许在相同作用域内，重复声明同一个变量。

```js
// 报错
function func() {
  let a = 10;
  var a = 1;
}

// 报错
function func() {
  let a = 10;
  let a = 1;
}
```

因此，不能在函数内部重新声明参数。

```js
function func(arg) {
  let arg;
}
func() // 报错

function func(arg) {
  {
    let arg;
  }
}
func() // 不报错
```


## 1.6 const 命令

声明常量，常量就是值(内存地址) 不能变化的量

1、声明常量
const SCHOOL='sgg';

### 1.6.1 特点

- 一定要赋初值 : const PI; // Missing initializer in const declaration
- 一般常量使用大写命名（潜规则）
- 常量的值不能修改
```js
const = PI;
PI = 100; // assignment to constant variable.   

const ary = [100, 200];
ary[0] = 'a';
ary[1] = 'b';
console.log(ary); // ['a', 'b'];
ary = ['a','b']; // assignment to constant variable.   
```
- 块级作用域，块级外无效
```js
if (true) {
	const a = 10;
}
console.log(a); // a is not defined
```
- 对于数组和对象的元素修改，不算做对常量的修改，不会报错

```js
const T=['UE','TX','NG'];
T.push('DF');
 //只要T所指的地址没有改变，就不会报错
```



### 1.6.2 const cannot be updated or re-declared

This means that the value of a variable declared with `const` remains the same within its scope. It cannot be updated or re-declared. So if we declare a variable with `const`, we can neither do this:

```javascript

const greeting = "say Hi";
greeting = "say Hello instead"; //  会报错 error: Assignment to constant variable.

const greeting = "say Hi";
const greeting = "say Hello instead";// 会报错 error: Identifier 'greeting' has already been declared

```

Every `const` declaration, therefore, must be initialized at the time of declaration.


> This behavior is somehow different when it comes to objects declared with `const`. While a `const` object cannot be updated, the properties of this objects can be updated. Therefore, if we declare a `const` object as this:

```javascript

const greeting = {
    message: "say Hi",
    times: 4
}

// while we cannot do this:
greeting = {
    words: "Hello",
    number: "five"
} // error:  Assignment to constant variable.

/// we can do this:
    greeting.message = "say Hello instead";


```

---


`const`声明一个只读的常量。一旦声明，常量的值就不能改变。

```js
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

上面代码表明改变常量的值会报错。

`const`声明的变量不得改变值，这意味着，`const`一旦声明变量，就必须立即初始化，不能留到以后赋值。

```js
const foo;
// SyntaxError: Missing initializer in const declaration
```

上面代码表示，对于`const`来说，只声明不赋值，就会报错。

---


 `const`声明的常量，也与`let`一样不可重复声明。

```js
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```


### 1.6.3 const declarations are block scoped

Like `let` declarations, `const` declarations can only be accessed within the block they were declared.
`const`的作用域与`let`命令相同：只在声明所在的块级作用域内有效。

```js
if (true) {
  const MAX = 5;
}

MAX // Uncaught ReferenceError: MAX is not defined
```


### 1.6.4 Hoisting of const

`const`命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。
Just like `let`, `const` declarations are hoisted to the top but are not initialized.

```js
if (true) {
  console.log(MAX); // ReferenceError
  const MAX = 5;
}
```

上面代码在常量`MAX`声明之前就调用，结果报错。

### 1.6.5 本质

`const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。

```js
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```

上面代码中，常量`foo`储存的是一个地址，这个地址指向一个对象。不可变的只是这个地址，即不能把`foo`指向另一个地址，但对象本身是可变的，所以依然可以为其添加新属性。

下面是另一个例子。

```js
const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
a = ['Dave'];    // 报错
```

上面代码中，常量`a`是一个数组，这个数组本身是可写的，但是如果将另一个数组赋值给`a`，就会报错。

## 1.7 window 对象的属性和方法（全局作用域中）

全局作用域中，`var` 声明的变量，`function` 声明的函数，会自动变成 window 对象的属性或方法。

```javascript
var age = 18;
function add() {}
console.log(window.age);            // 18
console.log(window.add === add);     // true
```

```javascript
let age = 18;
const add = function() {}
console.log(window.age);            // undefined
console.log(window.add === add);     // false
```



## 1.8 块级作用域

### 1.8.1 为什么需要块级作用域？

ES5 只有全局作用域和函数作用域，没有块级作用域，这带来很多不合理的场景。

第一种场景，内层变量可能会覆盖外层变量。

```js
var tmp = new Date();

function f() {
  console.log(tmp);
  if (false) {
    var tmp = 'hello world';
  }
}

f(); // undefined
```

上面代码的原意是，`if`代码块的外部使用外层的`tmp`变量，内部使用内层的`tmp`变量。但是，函数`f`执行后，输出结果为`undefined`，原因在于变量提升，导致内层的`tmp`变量覆盖了外层的`tmp`变量。

第二种场景，用来计数的循环变量泄露为全局变量。

```
var s = 'hello';

for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}

console.log(i); // 5
```

上面代码中，变量`i`只用来控制循环，但是循环结束后，它并没有消失，泄露成了全局变量。

### 1.8.2 ES6 的块级作用域

`let`实际上为 JavaScript 新增了块级作用域。

- 作用域链：内层作用域 ——> 外层作用域 ——> 全局作用域

- 块级作用域：除了对象 `{}`，函数 `{}`（函数作用域）之外的一切 `{}` 都属于块级作用域。

```js
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

上面的函数有两个代码块，都声明了变量`n`，运行后输出 5。这表示外层代码块不受内层代码块的影响。如果两次都使用`var`定义变量`n`，最后输出的值才是 10。

ES6 允许块级作用域的任意嵌套。

```js
{{{{
  {let insane = 'Hello World'}
  console.log(insane); // 报错
}}}};
```

上面代码使用了一个五层的块级作用域，每一层都是一个单独的作用域。第四层作用域无法读取第五层作用域的内部变量。

内层作用域可以定义外层作用域的同名变量。

```js
{{{{
  let insane = 'Hello World';
  {let insane = 'Hello World'}
}}}};
```

块级作用域的出现，实际上使得获得广泛应用的匿名立即执行函数表达式（匿名 IIFE）不再必要了。

```js
// IIFE 写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```

### 1.8.3 块级作用域与函数声明

函数能不能在块级作用域之中声明？这是一个相当令人混淆的问题。

ES5 规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。

```js
// 情况一
if (true) {
  function f() {}
}

// 情况二
try {
  function f() {}
} catch(e) {
  // ...
}
```

上面两种函数声明，根据 ES5 的规定都是非法的。

但是，浏览器没有遵守这个规定，为了兼容以前的旧代码，还是支持在块级作用域之中声明函数，因此上面两种情况实际都能运行，不会报错。

ES6 引入了块级作用域，明确允许在块级作用域之中声明函数。ES6 规定，块级作用域之中，函数声明语句的行为类似于`let`，在块级作用域之外不可引用。

```js
function f() { console.log('I am outside!'); }

(function () {
  if (false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }

  f();
}());
```

上面代码在 ES5 中运行，会得到“I am inside!”，因为在`if`内声明的函数`f`会被提升到函数头部，实际运行的代码如下。

```js
// ES5 环境
function f() { console.log('I am outside!'); }

(function () {
  function f() { console.log('I am inside!'); }
  if (false) {
  }
  f();
}());
```

ES6 就完全不一样了，理论上会得到“I am outside!”。因为块级作用域内声明的函数类似于`let`，对作用域之外没有影响。但是，如果你真的在 ES6 浏览器中运行一下上面的代码，是会报错的，这是为什么呢？

```js
// 浏览器的 ES6 环境
function f() { console.log('I am outside!'); }

(function () {
  if (false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }

  f();
}());
// Uncaught TypeError: f is not a function
```

上面的代码在 ES6 浏览器中，都会报错。

原来，如果改变了块级作用域内声明的函数的处理规则，显然会对老代码产生很大影响。

- 允许在块级作用域内声明函数。
- 函数声明类似于`var`，即会提升到全局作用域或函数作用域的头部。
- 同时，函数声明还会提升到所在的块级作用域的头部。

注意，上面三条规则只对 ES6 的浏览器实现有效，其他环境的实现不用遵守，还是将块级作用域的函数声明当作`let`处理。

根据这三条规则，浏览器的 ES6 环境中，块级作用域内声明的函数，行为类似于`var`声明的变量。上面的例子实际运行的代码如下。

```js
// 浏览器的 ES6 环境
function f() { console.log('I am outside!'); }
(function () {
  var f = undefined;
  if (false) {
    function f() { console.log('I am inside!'); }
  }

  f();
}());
// Uncaught TypeError: f is not a function
```

考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。

```js
// 块级作用域内部的函数声明语句，建议不要使用
{
  let a = 'secret';
  function f() {
    return a;
  }
}

// 块级作用域内部，优先使用函数表达式
{
  let a = 'secret';
  let f = function () {
    return a;
  };
}
```

另外，还有一个需要注意的地方。ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。

```js
// 第一种写法，报错
if (true) let x = 1;

// 第二种写法，不报错
if (true) {
  let x = 1;
}
```

上面代码中，第一种写法没有大括号，所以不存在块级作用域，而`let`只能出现在当前作用域的顶层，所以报错。第二种写法有大括号，所以块级作用域成立。

函数声明也是如此，严格模式下，函数只能声明在当前作用域的顶层。

```js
// 不报错
'use strict';
if (true) {
  function f() {}
}

// 报错
'use strict';
if (true)
  function f() {}
```


## 1.9 5.顶层对象的属性

顶层对象，在浏览器环境指的是`window`对象，在 Node 指的是`global`对象。ES5 之中，顶层对象的属性与全局变量是等价的。

```js
window.a = 1;
a // 1

a = 2;
window.a // 2
```

上面代码中，顶层对象的属性赋值与全局变量的赋值，是同一件事。

顶层对象的属性与全局变量挂钩，被认为是 JavaScript 语言最大的设计败笔之一。这样的设计带来了几个很大的问题，首先是没法在编译时就报出变量未声明的错误，只有运行时才能知道（因为全局变量可能是顶层对象的属性创造的，而属性的创造是动态的）；其次，程序员很容易不知不觉地就创建了全局变量（比如打字出错）；最后，顶层对象的属性是到处可以读写的，这非常不利于模块化编程。另一方面，`window`对象有实体含义，指的是浏览器的窗口对象，顶层对象是一个有实体含义的对象，也是不合适的。

ES6 为了改变这一点，一方面规定，为了保持兼容性，`var`命令和`function`命令声明的全局变量，依旧是顶层对象的属性；另一方面规定，`let`命令、`const`命令、`class`命令声明的全局变量，不属于顶层对象的属性。也就是说，从 ES6 开始，全局变量将逐步与顶层对象的属性脱钩。

```js
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```

上面代码中，全局变量`a`由`var`命令声明，所以它是顶层对象的属性；全局变量`b`由`let`命令声明，所以它不是顶层对象的属性，返回`undefined`。
