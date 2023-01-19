
# 1 前言

在编程中使用最多的就是函数，在 ES5 中是用 `function` 关键字来定义函数的，由于历史原因 `function` 定义的函数存在一些问题，如 `this` 的指向、函数参数 `arguments` 等。

ES6 规定了可以使用 “箭头” `=>` 来定义一个函数，语法更加简洁。它没有自己的 `this`、`arguments`、`super` 或 `new.target`，箭头函数表达式更适用于那些本来需要匿名函数的地方，但它不能用作构造函数。





# 2 认识箭头函数

普通函数：

- `function 函数名() {}`
- `const 变量名 = function () {};`

箭头函数：

- `参数 => 函数体`

- `() => {}`

> 由于箭头函数是匿名函数，所以我们通常把它赋给一个变量

```javascript
const add = (x, y) => {
    return x + y;
};

console.log(add(1, 1));        // 2
```

```js
() => {}    
const fn = () => {}


var f = v => v;
上面的箭头函数等同于：
var f = function(v) {
  return v;
};
```

# 3 写法

## 3.1 行参个数和省略写法

如果箭头函数不需要参数或多个参数：
```js
var f = () => 5;
//等同于
var f = function(){return 5};

var sum = (num1,num2) => num1 + num2;
//等同于
var sum = function(num1,num2){return num1 + num2}


```

如果形参只有一个，可以省略小括号
```js
function fn(v){
    retuen v;
} 
const fn = v => v;
```


```javascript
const add = (x) => {
    return x + 1;
};

// 单个参数可以省略 ()
const add = x => {
    return x + 1;
};

// 无参数
const test = () => {
    return 1;
};
//或者
const test = _ => {
    return 1;
};


//多个参数, 不能去省略 ()
var sum = (num1,num2) => num1 + num2;
//等同于
var sum = function(num1,num2){return num1 + num2}
```

## 3.2 代码数量
函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号
```js
function sum(num1, num2) {
    return num1 + num2;
}    
const sum = (num1, num2) => num1 + num2;
```

如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
```js
var sum = (num1, num2) => { return num1 + num2; }
1
由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

var getTempItem = id => ({ id: id, name: "Temp" });
```


由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

```javascript
va#r getTempItem = id => ({ id: id, name: "Temp" });
```

## 3.3 单行函数体
函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号
```javascript
const add = (x, y) => {
    return x + y;
};

const add = (x, y) => {
    return {
        value: x + y
    };
};

// 单行函数体可以省略 return 和 {}，且一但省略就 return 和 {} 都要一起省略
const add = (x, y) => x + y; 
```

### 3.3.1 单行函数体, 函数带返回对象 


由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。
```javascript
var sum = (num1, num2) => ({ return num1 + num2; }
                       // 数组就没有以上问题
const add = (x, y) => [x, y];

```


 推荐：一般情况最好不要简写！
```js
// 报错！因为 {} 会产生歧义！
const add = (x, y) => {value: x + y};  

// () 可以将语句变为表达式，从而 {} 就可以被顺理成章解释为对象. 由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。
const add = (x, y) => ({value: x + y});

```

### 3.3.2 多行函数体
如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
```js
var getTempItem = id => ({ id: id, name: "Temp" });

```


## 3.4 简化回调函数
```js
//ES5写法
[1,2,3].map(function(x)){
    return x * x;
}

//ES6写法
[1,2,3].map(x => x * x);
```



# 4 语法注意点
## 4.1 箭头函数可以与变量解构结合使用
```js
const full = ({first,last}) => first + ' ' + last;

//等同于
function full(person){
   return person.first + ' ' + person.last;
}
```


## 4.2 函数传递参数设置默认值
语法:function 函数名(形参1=默认值1,形参2=默认值2){ }
```js
       function fn(a){
            // 如果没传参，直接输出10，如果传参了，直接输出传入的值
            a = a||10;
            console.log(a)
        }
        fn(20)

        //可以使用函数参数的默认值简写
        function fn(a=10){
            console.log(a)
        }
        fn(100)
// 当箭头函数的形参只有一个，但是有默认值的情况下，不能省略()
        var fn = (a=10)=>console.log(a)
```


# 5 特点

- 箭头函数是匿名函数
- 更短的函数，优雅简洁； 不需要写 argments
- arrow function hat keine hoisting的意思是 : 不用先定义后使用. funtionk 可以, 先 ausfuhre, 然后在下一行 进行 这个 funtion 的 decalre 
- 箭头函数不使用 this, 不会创建自己的 this，它只会从自己的作用域链的上一层继承 this；
    - 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
- 不能绑定 arguments， 该对象在函数体内不存在。只能使用 `...args` 展开运算来获取当前参数的数组。
    - 不可以使用arguments对象，因为箭头函数不会创建自己的 this, 该对象在函数体内不存在。
    - 如果要用，可以用Rest参数代替。
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
- 不可以使用yield命令，因此箭头函数不能用作Generator函数。

（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。


## 5.1 箭头函数不使用 this, 不会创建自己的 this，
```js
    let objFunc = {};
    objFunc.show = function(par){
        return console.log(`Parameter: ${par}`, this);  // this 处 打印为 show f(par)
    };
    objFunc.show(true);
    
    // kein this für Arrow Functions
    let objArrow = {};
    objArrow.show = par => console.log(`Parameter: ${par}`, this);   // this 处 打印为 undefinied 
    objArrow.show(true);
    
```

## 5.2 不能用作构造器

箭头函数不能用作构造器，和 new 一起用会抛出错误。

```js
var Foo = () => {};
var foo = new Foo(); // TypeError: Foo is not a constructor
```

## 5.3 没有 prototype 属性

箭头函数没有 prototype 属性。

```js
var Foo = () => {};
console.log(Foo.prototype); // undefined
```

## 5.4 不能使用 yield 命令

yield 关键字通常不能在箭头函数中使用，因此箭头函数不能用作 Generator 函数。



# 6 箭头函数和匿名函数的转换
e= > {}  
等效于 function() = {}

# 7 箭头函数里面的this

箭头函数里面的this，绑定定义时所在的作用域，而不是指向运行时所在的作用域。
this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数。

(箭头函数导致this总是指向函数定义生效时所在的对象)

```js
const obj = { name: '张三'}
function fn () {
    console.log(this); // obj 
    return () => {
        console.log(this) // obj 
    }
}
const resFn = fn.call(obj);
resFn();
```

## 7.1 全局作用域中的 this 指向

```javascript
console.log(this);
// window
```


## 7.2 一般函数（非箭头函数）中的 this 指向

> 只有在函数调用的时候 this 指向才能确定，不调用的时候，不知道指向谁。
> 
> this 指向和函数在哪儿没有关系，只和谁在调用有关。

```javascript
function add() {
    console.log(this);
}

add();    // window
// 在非严格模式下，this 其实是先指向 undefined，然后被自动转为了 window
```

```javascript
'use strict'    // 严格模式

function add() {
    console.log(this);
}

add();    // undefined
// 在严格模式下，this 为 undefined
```

```javascript
'use strict'    // 严格模式

function add() {
    console.log(this);
}

const calc = {
    add: add
};

calc.add();        // 上下文 this 为 calc

const adder = calc.add;
adder();        // 指向 undefined（非严格模式下指向 window）
```

## 7.3 箭头函数没有 this
箭头函数里面的this，绑定定义时所在的作用域，而不是指向运行时所在的作用域。
this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数。

(箭头函数导致this总是指向函数定义生效时所在的对象)

### 7.3.1 例子
在 JavaScript 中，要说让人最头疼的知识点中，this 绑定绝对算一个，这是因为 this 的绑定 ‘难以捉摸’，出错的时候还往往不知道为什么，相当反逻辑。下面我们来看一个示例：

```js
var title = "全局标题";
var imooc = {
    title: "慕课网 ES6 Wiki",
    getTitle : function(){
        console.log(this.title);
    }
};
imooc.getTitle();        // 慕课网 ES6 Wiki
var bar = imooc.getTitle;
bar();        // 全局标题
```

通过上面的小例子的打印结果可以看出 `this` 的问题，说明 `this` 的指向是不固定的。

这里简单说明一下 `this` 的指向，**`this` 指向的是调用它的对象**。例子中的 `this` 是在 getTitle 的函数中的，执行 `imooc.getTitle()` 这个方法时，调用它的对象是 `imooc`，所以 this 的指向是 `imooc`。

之后把 `imooc.getTitle` 方法赋给 `bar`，这里要注意的是，只是把地址赋值给了 `bar` ，并没有调用。 而 `bar` 是全局对象 `window` 下的方法，所以在执行 `bar` 方法时，调用它的是 Window 对象，所以这里打印的结果是 window 下的 title——“全局标题”。

> TIPS: 上面的示例只是简单的 `this` 指向问题，还有很多更加复杂的，在面试中经常会被问到，所以还不清楚的同学可以去研究一下 `this` 的问题。

ES6 为了规避这样的问题，提出了箭头函数的解决方案，在箭头函数中没有自己的 `this` 指向，所有的 this 指向都指向它的上一层 `this` ，这样规定就比较容易理解了。下面看使用箭头函数下的 `this` 指向：

```js
var title = "全局标题";
var imooc = {
    title: "慕课网 ES6 Wiki",
    getTitle : () => {
        console.log(this.title);
    }
};
imooc.getTitle();        // 全局标题
var bar = imooc.getTitle;
bar();        // 全局标题
```

上面的打印结果可以看出来，所有的 `this` 指向都指向了 window 对象下的 title，本身的 imooc 对象下没有了 `this` ，它的上一层就是 window。

# 8 不适用箭头函数的场景

## 8.1 作为构造函数

因为箭头函数没有 this，而构造函数的核心就是 this。

## 8.2 需要 this 指向调用对象的时候

因为箭头函数没有 this，所以如果箭头函数中出现了 this，那么这个 this 就是外层的！

## 8.3 需要使用 arguments 的时候

箭头函数没有 arguments。

（这个问题有替代解决方案：剩余参数）

```js
var fun = function() {
  console.log(arguments)
};
fun(1,2,3);  // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]

var fun = () => {
  console.log(arguments)
};
fun(1,2,3);  // Uncaught ReferenceError: arguments is not defined
```

上面的示例中，对比两种定义函数的方法可以明显的看出，在箭头函数中去取 `arguments` 时会报引用错误，没有定义的 `arguments`。

`arguments` 的主要作用是获取所有调用函数时所需要传入的参数，在箭头函数中使用剩余参数 `...args`，在函数内可以直接使用。

```js
function foo(...args) { 
  console.log(args)
}
foo(1);         // [1]
foo(1, 2, 3);   // [1, 2, 3]
```



