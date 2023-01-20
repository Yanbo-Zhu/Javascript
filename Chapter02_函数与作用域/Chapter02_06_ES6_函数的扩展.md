

# 1 函数的扩展
## 1.1 函数参数的默认值

### 1.1.1 认识函数参数的默认值

调用函数的时候传参了，就用传递的参数；如果没传参，就用默认值

### 1.1.2 函数参数默认值的基本用法

```javascript
// 之前的默认值实现方式
const multiply = (x, y) => {
    if (typeof y === 'undefined') {
        y = 3;
    }
    return x * y;
};
console.log(multiply(2, 2));    // 4
console.log(multiply(2));        // 6
```

```javascript
// ES6 默认值实现方式
const multiply = (x, y = 3) => {
    return x * y;
};
console.log(multiply(2, 2));    // 4
console.log(multiply(2));        // 6
```

### 1.1.3 默认值的生效条件

不传参数，或者明确的传递 undefined 作为参数，只有这两种情况下，默认值才会生效。

注意：null 就是 null，不会使用默认值。

### 1.1.4 与解构赋值默认值结合使用

参数默认值可以与解构赋值的默认值，结合起来使用。

```js
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined 5
foo({x: 1}) // 1 5
foo({x: 1, y: 2}) // 1 2
foo() // TypeError: Cannot read property 'x' of undefined
```

上面代码只使用了对象的解构赋值默认值，没有使用函数参数的默认值。只有当函数`foo()`的参数是一个对象时，变量`x`和`y`才会通过解构赋值生成。如果函数`foo()`调用时没提供参数，变量`x`和`y`就不会生成，从而报错。通过提供函数参数的默认值，就可以避免这种情况。

```js
function foo({x, y = 5} = {}) {
  console.log(x, y);
}

foo() // undefined 5
```

上面代码指定，如果没有提供参数，函数`foo`的参数默认为一个空对象。

下面是另一个解构赋值默认值的例子。

```js
function fetch(url, { body = '', method = 'GET', headers = {} }) {
  console.log(method);
}

fetch('http://example.com', {})
// "GET"

fetch('http://example.com')
// 报错
```

上面代码中，如果函数`fetch()`的第二个参数是一个对象，就可以为它的三个属性设置默认值。这种写法不能省略第二个参数，如果结合函数参数的默认值，就可以省略第二个参数。这时，就出现了双重默认值。

```js
function fetch(url, { body = '', method = 'GET', headers = {} } = {}) {
  console.log(method);
}

fetch('http://example.com')
// "GET"
```

上面代码中，函数`fetch`没有第二个参数时，函数参数的默认值就会生效，然后才是解构赋值的默认值生效，变量`method`才会取到默认值`GET`。

注意，函数参数的默认值生效以后，参数解构赋值依然会进行。

```js
function f({ a, b = 'world' } = { a: 'hello' }) {
  console.log(b);
}

f() // world
```

上面示例中，函数`f()`调用时没有参数，所以参数默认值`{ a: 'hello' }`生效，然后再对这个默认值进行解构赋值，从而触发参数变量`b`的默认值生效。

### 1.1.5 参数默认值的位置

通常情况下，定义了默认值的参数，应该是函数的尾参数。因为这样比较容易看出来，到底省略了哪些参数。如果非尾部的参数设置默认值，实际上这个参数是没法省略的。


1
上面代码中，有默认值的参数都不是尾参数。这时，无法只省略该参数，而不省略它后面的参数，除非显式输入`undefined`。

```js
// 例一
function f(x = 1, y) {
  return [x, y];
}

f() // [1, undefined]
f(2) // [2, undefined]
f(, 1) // 报错
f(undefined, 1) // [1, 1]

// 例二
function f(x, y = 5, z) {
  return [x, y, z];
}

f() // [undefined, 5, undefined]
f(1) // [1, 5, undefined]
f(1, ,2) // 报错
f(1, undefined, 2) // [1, 5, 2]
```

2
如果传入`undefined`，将触发该参数等于默认值，
传入 `null`, 不会触发 默认值。

```js
function foo(x = 5, y = 6) {
  console.log(x, y);
}

foo(undefined, null)
// 5 null
```

上面代码中，`x`参数对应`undefined`，结果触发了默认值，`y`参数等于`null`，就没有触发默认值。

### 1.1.6 函数参数默认值的应用

#### 1.1.6.1 通过一个例子了解全部

```js
const power = (base,exponent=2) => {
    let result = 1;
    for(let i=0; i<exponent; i++){
        result *= base;
    }
    console.log(base, exponent, typeof exponent);
  return result;  
}

console.log(power(2,3)); // 结果为 (2 3 'number', 8)  替代掉 默认值
console.log(power(2)); //  结果为 (2 2 'number', 4)    使用了默认值
console.log(power()); //  结果为 (undefined 2 'number', NaN)    使用了默认值
console.log(power(2,2,2)); // 结果为 (2 2 'number', 4)    超出的那个 根本就没使用 
console.log(power(null,5)); // 结果为 (null 5 'number', 0)  null 被转变为0
console.log(power(true,2)); // 结果为 (true 2 'number', 1 )  true 被转变为 1 , false 会被 转化为 数值 0  
console.log(power(2,"Hurra")); //结果为 (2 'Hurra' 'string', 1 )   string 无法转为任何数值 , string 为 NaN : not a number 
console.log(power("bla",5));  // 结果为 (bla 5 number, NaN )  string 无法转为任何数值 , string 为 NaN : not a number 
}
```

#### 1.1.6.2 其他
**接收很多参数的时候**

```javascript
// 普通时候
const logUser = (username = 'zjr', age = 18, sex = 'male') => {
    console.log(username, age, sex);
};
// 需要能够记住参数的顺序，如果参数较多那么需要配合文档，使用不方便
logUser('jerry', 18, 'male');

// ------------------------------------------------------------

// 接收一个对象作为参数
// 不需要记住参数的顺序
const logUser = options => {
    console.log(options.username, options.age, options.sex);
};
logUser({
    username: 'jerry',
    age: 18,
    sex: 'male'
});

// ------------------------------------------------------------

// 再优化
const logUser = ({username, age, sex}) => {
    console.log(username, age, sex);
};

logUser({
    username: 'jerry',
    age: 18,
    sex: 'male'
});

// ------------------------------------------------------------

// 引入默认值
const logUser = ({
    username = 'zjr',
    age = 18,
    sex = 'male'
}) => {
    console.log(username, age, sex);
};

// 其实是解构赋值原理
logUser({username: 'jerry'});    // jerry 18 male

logUser({});    // zjr 18 male

logUser();        // 报错，因为这样相当于传了一个 undefined，不符合解构赋值

// ------------------------------------------------------------

// 再优化（函数默认值 + 解构赋值 + 解构赋值默认值）
const logUser = ({
    username = 'zjr',
    age = 18,
    sex = 'male'
} = {}) => {
    console.log(username, age, sex);
};
logUser();    // zjr 18 male

/* 
解释：
1、options 与 {username = 'zjr', age = 18, sex = 'male'} 互等
2、{username = 'zjr', age = 18, sex = 'male'} = {} 其实就是 options = {}
3、由于 logUser() 的实参为 undefined，所以默认值为 {}
4、再因为 {username = 'zjr', age = 18, sex = 'male'} = {} 是解构赋值
5、由于 {} 内为 undefined，所以解构赋值启用默认值
5、所以真正的形参为 {username = 'zjr', age = 18, sex = 'male'}
注明：这样做的好处是增加函数的健壮性！
*/
```

**某一个参数不得省略，如果省略就抛出一个错误**

```js
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
// Error: Missing parameter
```

上面代码的`foo`函数，如果调用的时候没有参数，就会调用默认值`throwIfMissing`函数，从而抛出一个错误。

从上面代码还可以看到，参数`mustBeProvided`的默认值等于`throwIfMissing`函数的运行结果（注意函数名`throwIfMissing`之后有一对圆括号），这表明参数的默认值不是在定义时执行，而是在运行时执行。如果参数已经赋值，默认值中的函数就不会运行。

另外，可以将参数默认值设为`undefined`，表明这个参数是可以省略的。

```js
function foo(optional = undefined) { ··· }
```

## 1.2 rest 参数/剩余参数

剩余参数语法允许我们将一个不定数量的参数表示为一个数组。
```js
function sum (first, ...args) {
    console.log(first); // 10 
    console.log(args); // [20, 30]
}
sun(10, 20, 30);
```


剩余参数和解构配合使用
```js
let students = ['wangwu', 'zhangsan', 'lisi'];
let [s1, ...s2] = students;
console.log(s1); // wangwu
console.log(s2); // ['zhangsan', 'lisi']
```


### 1.2.1 前言

剩余语法（Rest syntax 也可以叫剩余参数）看起来和展开语法完全相同都是使用 `...` 的语法糖，不同之处在于剩余参数用于解构数组和对象。从某种意义上说，剩余语法与展开语法是相反的：展开语法将数组展开为其中的各个元素，而剩余语法则是将多个元素收集起来成为一个整体。

### 1.2.2 函数参数

在讲解剩余参数前，我们先来看看，剩余参数在函数参数中都解决了哪些问题？为什么会引入剩余参数的概念？

在 ES5 中，函数经常会传入不定参数，在传入不定参数时，ES5 的给出的解决方案是通过 `arguments` 对象来获取函数调用时传递的参数。 `arguments` 对象不是一个数组，它是一个类数组对象，所谓类数组对象，就是指可以**通过索引属性访问元素**并且**拥有 length** 属性的对象。

一个简单的类数组对象是长这样的:

```js
var arrLike = {
  0: 'name',
  1: 'age',
  2: 'job',
  length: 3
}
```

而它所对应的数组应该是这样子的：

```js
var arr = ['name', 'age', 'job'];
```

这里我们说类数组对象与数组的性质相似，是因为类数组对象在**访问**、**赋值**、**获取长度**上的操作与数组是一致的，具体内容可查阅相关的类数组使用。

在函数体中定义了 Arguments 对象，其包含函数的参数和其它属性，以 `arguments` 变量来指代。下面我们看个实例：

```js
function fn() {
    console.log(arguments);
}
fn('imooc', 7, 'ES6')
```

在控制台中打印出上面的代码结果，如下图所示：在定义函数的时候没有给定参数，但是通过 `arguments` 对象可以拿到传入的参数。可以看到 `arguments` 中包含了函数传递的参数、length 等属性，length 属性表示的是实参的长度，即调用函数的时候传入的参数个数。这样我们就对 `arguments` 对象有了一定的了解。

![image-20220826180356855](https://i0.hdslb.com/bfs/album/116b8f3318b159435aaeca5914bc5cf3dd424fdf.png)

在 ES5 的开发模式下，想要使用传递的参数，则需要按位置把对应的参数取出来。尽管 `arguments` 是一个类数组且可遍历的变量，但它终究不是数组，它不支持数组方法，因此我们不能调用 `arguments.forEeach (…)` 等数组的方法。需要使用一些特殊的方法转换成数组使用，如：

```js
function fn() {
  var arr = [].slice.call(arguments);
  console.log(arr)
}
fn('ES6');
//  ["ES6"]
fn('imooc', 7, 'ES6');
//  ["imooc", 7, "ES6"]
```

终于借助 `call` 方法把 `arguments` 转化成一个真正的数组了。但是这样无疑是一个繁琐的过程，而且不容易理解。这时 ES6 给出了它的完美解决方案 —— 剩余参数，那剩余参数是如何在函数传参中使用的呢？下面我们来看看实例：

语法：`const add = (x, y, z, ...args) => {};`

```js
function fn(...args) {
  console.log(args)
}
fn('ES6');
//  ["ES6"]
fn('imooc', 7, 'ES6');
//  ["imooc", 7, "ES6"]
```

使用方式很简单在函数定义时使用 `...` 紧接着跟一个收集的参数，这个收集的参数就是我们所传入不定参数的集合 —— 也就是数组。这样就很简单地摆脱了 arguments 的束缚。另外，还可以指定一个默认的参数，如下示例：

```js
function fn(name, ...args) {
  console.log(name);  // 基础参数
  console.log(args);  // 剩下的参数组成的数组
}
fn('ES6');
//    'ES6'
//    []
fn('imooc', 7, 'ES6');
//  "imooc"
//    [7, "ES6"]
```

上面的代码中给函数第一个参数，声明一个变量 name，剩余的参数会被 `...` 收集成一个数组，这就是剩余参数。引入剩余参数就是为了能替代函数内部的 `arguments`，由于 `arguments` 对象不具备数组的方法，所以很多时候在使用之前要先转换成一个数组。而剩余参数本来就是一个数组，避免了这多余的一步，使用起来既优雅又自然。

### 1.2.3 注意事项

**箭头函数的剩余参数**

箭头函数的参数部分即使只有一个剩余参数，也不能省略圆括号。

`const add = (...args) => {};`

 **使用剩余参数替代 arguments 获取实际参数**

- 剩余参数是一个 “真数组”，arguments 是一个 “伪数组”
- 剩余参数的名字可以自定义

**剩余参数的位置**

剩余参数只能是最后一个参数，之后不能再有其他参数，否则会报错。

### 1.2.4 剩余参数的应用

作为数组的应用：

```javascript
const add = (...args) => {
    let sum = 0;

    for (let i = 0; i < args.length; i++) {
        sum += args[i];
    } // 当然此处，arguments 也可以

    return sum;
};

console.log(add());            // 0
console.log(add(1, 1));        // 2
console.log(add(1, 2, 3));    // 6
```

与解构赋值结合使用：

（剩余参数不一定非要作为函数参数使用）

- 与数组解构赋值结合

```javascript
let array = [1, 2, 3, 4, 5];
let [a, b, ...others] = array;
console.log(a);                     // 1
console.log(b);                     // 2
console.log(others);         // [3,4,5]
```

- 与对象解构赋值结合

```javascript
const {x, y, ...z} = {a: 3, x: 1, y: 2, b: 4};
console.log(x, y, z);
// 1 2 { a: 3, b: 4 }
// 这里的剩余参数是个对象（准确的应该叫：剩余元素）
```

```javascript
const func = ({x, y, ...z}) => {
    console.log(x, y, z);    // 1 2 { a: 3, b: 4 }
};
func({a: 3, x: 1, y: 2, b: 4});
```

- 在函数传参的时候也可以是和解构一起使用

```js
function fun(...[a, b, c]) {
  return a + b + c;
}
fun('1')          // NaN (b 和 c 都是 undefined)
fun(1, 2, 3)      // 6
fun(1, 2, 3, 4)   // 6 多余的参数不会被获取到
```

上面的代码中，a、b、c 会去解构传入参数，加上有剩余语法的作用，对应的值从数组中的项解构出来，在函数内部直接使用解构出来的参数即可。剩余语法看起来和展开语法完全相同，不同点在于，剩余参数用于解构数组和对象。

### 1.2.5 小结

本节结合了 ES5 函数中的 `arguments` 对象引入了为什么 ES6 会引入剩余参数的概念，可以看到剩余参数所带来的好处。本节内容可以总结以下几点：

1. 剩余参数是为了能替代函数内部的 arguments 而引入的；
2. 和展开语法相反，剩余参数是将多个单个元素聚集起来形成一个单独的个体的过程。


## 1.3 函数参数的尾逗号

ES2017 允许函数的最后一个参数有尾逗号（trailing comma）。

此前，函数定义和调用时，都不允许最后一个参数后面出现逗号。

```js
function clownsEverywhere(
  param1,
  param2
) { /* ... */ }

clownsEverywhere(
  'foo',
  'bar'
);
```

上面代码中，如果在`param2`或`bar`后面加一个逗号，就会报错。

如果像上面这样，将参数写成多行（即每个参数占据一行），以后修改代码的时候，想为函数`clownsEverywhere`添加第三个参数，或者调整参数的次序，就势必要在原来最后一个参数后面添加一个逗号。这对于版本管理系统来说，就会显示添加逗号的那一行也发生了变动。这看上去有点冗余，因此新的语法允许定义和调用时，尾部直接有一个逗号。

```js
function clownsEverywhere(
  param1,
  param2,
) { /* ... */ }

clownsEverywhere(
  'foo',
  'bar',
);
```

这样的规定也使得，函数参数与数组和对象的尾逗号规则，保持一致了。

## 1.4 catch 命令的参数省略

JavaScript 语言的`try...catch`结构，以前明确要求`catch`命令后面必须跟参数，接受`try`代码块抛出的错误对象。

```js
try {
  // ...
} catch (err) {
  // 处理错误
}
```

上面代码中，`catch`命令后面带有参数`err`。

很多时候，`catch`代码块可能用不到这个参数。但是，为了保证语法正确，还是必须写。ES2019做出了改变，允许`catch`语句省略参数。

```js
try {
  // ...
} catch {
  // ...
}
```
