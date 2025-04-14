

# 1 其他数据类型与数组之间的转化 


## 1.1 Array.from(): 其他数据类型转化为数组

本节讲解了字符串的 `Array.from()` 方法的使用，用于将类数组对象和可迭代的对象转化真正的数组，在编程中主要用于更加方便的初始化一个有默认值的数组，还可以用于将获取的 html 的 DOM 对象转化为数组，可以使用数组方法进行操作。


在前端开发中经常会遇到类数组，但是我们不能直接使用数组的方法，需要先把类数组转化为数组。本节介绍 ES6 数组的新增方法 `Array.from()`，该方法用于将类数组对象（array-like）和可遍历的对象（iterable）转换为真正的数组进行使用。

Array.from() 只是没有永久改变这个变量的数据类型:  die Umwandlung der Collection in ein Array ist nur temporär,Die Variable allP verweist immer noch auf eine Collection
DOM Elementen 储存进array 
```js
// Listen aus DOM Elementen sind Collections
let allP = document.getElementsByTagName("p");
console.log(allP,typeof allP);  // 显示为 HTMLCollection(4) [p, p, p, p] 'object'
console.log(Array.from(allP), typeof Array.from(allP));

// folgendes ist nicht möglich, weil allP kein Array ist.
// allP 是一个 HTMLCollection 的数据类型
// ForEach 是一个 array method , forEach 不能 对非array数据类型 的 变量 进行使用 
// 所以这里会报错: Uncaught TypeError: allP.forEach is not a function 
allP.forEach(element => {
    console.log(element);
});

// Um Array Methoden auf sie anzuwenden, müssen sie in ein Array umgewandelt werden. 使用 Array.from 函数 , 将其转换为 array 类型 
Array.from(allP).forEach(element => {
    console.log(element);
});

```


### 1.1.1 基本语法

`Array.from()` 方法会接收一个类数组对象然后返回一个真正的数组实例，返回的数组可以调用数组的所有方法。

**语法使用：**

```js
Array.from(arrayLike[, mapFn[, thisArg]])
```



**参数解释：**

| 参数        | 描述                          |
|:--------- |:--------------------------- |
| arrayLike | 想要转换成数组的类数组对象或可迭代对象         |
| mapFn     | 如果指定了该参数，新数组中的每个元素会执行该回调函数  |
| thisArg   | 可选参数，执行回调函数 mapFn 时 this 对象 |

1 将类(伪)数组或可遍历对象转换为正真的数组
```js
let arrayLike = {
     '0': 'a',
     '1': 'b',
     '2': 'c',
     length: 3
 };
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']    
```
 
2 方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。
```js
let arrayLike = {
    "0": 1,
    "1": 2,
    "length": 2
}
let newAry = Array.from(aryLike, item => item * 2)
```



### 1.1.2 类数组转化

所谓类数组对象，就是指可以通过索引属性访问元素，并且对象拥有 length 属性，类数组对象一般是以下这样的结构：

```js
var arrLike = {
  '0': 'apple',
  '1': 'banana',
  '2': 'orange',
  length: 3
};
```

在 ES5 中没有对应的方法将类数组转化为数组，但是可以借助 call 和 apply 来实现：

```js
var arr = [].slice.call(arrLike);
// 或
var arr = [].slice.apply(arrLike);
```

有了 ES6 的 `Array.from()` 就更简单了，对类数组对象直接操作，即可得到数组。

```js
var arr = Array.from(arrLike);
console.log(arr)  // ['apple', 'banana', 'orange']
```

#### 1.1.2.1 第二个参数 —— 回调函数

在 `Array.from` 中第二个参数是一个类似 map 函数的回调函数，该回调函数会依次接收数组中的每一项作为传入的参数，然后对传入值进行处理，最得到一个新的数组。
`Array.from(obj, mapFn, thisArg)` 也可以用 map 改写成这样 `Array.from(obj).map(mapFn, thisArg)`。

```js
var arr = Array.from([1, 2, 3], function (x) {
  return 2 * x;
});
var arr = Array.from([1, 2, 3]).map(function (x) {
  return 2 * x;
});
//arr: [2, 4, 6]



let arrayLike = {
    "0": 1,
    "1": 2,
    "length": 2
}
let newAry = Array.from(aryLike, item => item * 2)
```

上面的例子展示了，`Array.from` 的参数可以使用 `map` 方法来进行替换，它们是等价的操作。

#### 1.1.2.2 第三个参数 ——this

`Array.from` 中第三个参数可以对回调函数中 this 的指向进行绑定，该参数是非常有用的，我们可以将被处理的数据和处理对象分离，将各种不同的处理数据的方法封装到不同的的对象中去，处理方法采用相同的名字。

在调用 Array.from 对数据对象进行转换时，可以将不同的处理对象按实际情况进行注入，以得到不同的结果，适合解耦。

```js
let obj = {
  handle: function(n){
    return n + 2
  }
}

Array.from([1, 2, 3, 4, 5], function (x){
  return this.handle(x)
}, obj)
// [3, 4, 5, 6, 7]
```

定义一个 `obj` 对象可以认作是，`Array.from` 回调函数中处理数据的方法集合，`handle` 是其中的一个方法，把 `obj` 作为第三个参数传给 `Array.from` 这样在回调函数中可以通过 `this` 来拿到 `obj` 对象。

#### 1.1.2.3 从字符串里生成数组

`Array.from()` 在传入字符串时，会把字符串的每一项都拆成单个的字符串作为数组中的一项。

```js
Array.from('imooc'); 
// [ "i", "m", "o", "o", "c" ]
```

#### 1.1.2.4 从 Set 中生成数组

用 `Set` 定义的数组对象，可以使用 `Array.from()` 得到一个正常的数组。

```js
const set = new Set(['a', 'b', 'c', 'd']);
Array.from(set);
// [ "a", "b", "c", "d" ]
```

上面的代码中创建了一个 Set 数据结构，把实例传入 `Array.from()` 可以得到一个真正的数组。

#### 1.1.2.5 从 Map 中生成数组

`Map` 对象保存的是一个个键值对，`Map` 中的参数是一个数组或是一个可迭代的对象。 `Array.from()` 可以把 Map 实例转换为一个二维数组。

```js
const map = new Map([[1, 2], [2, 4], [4, 8]]);

Array.from(map);  // [[1, 2], [2, 4], [4, 8]]
```

### 1.1.3 使用案例




#### 1.1.3.1 创建一个包含从 0 到 99 (n) 的连续整数的数组

1. 一般情况下我们可以使用 for 循环来实现。

```js
var arr = [];
for(var i = 0; i <= 99; i++) {
  arr.push(i);
}
```

这种方法的主要优点是最直观了，性能也最好的，但是很多时候我们不想使用 for 循环来进行操作。

1. 使用 Array 配合 map 来实现。

```js
var arr = Array(100).join(' ').split('').map(function(item,index){return index});
```

Array (100) 创建了一个包含 100 个空位的数组，但是这样创建出来的数组是没法进行迭代的。所以要通过字符串转换，覆盖 undefined，最后调用 map 修改元素值。

1. 使用 es6 的 `Array.from` 实现。

```js
var arr = Array.from({length:100}).map(function(item,index){return index});
```

`Array.from({length:100})` 可以定义一个可迭代的数组，数组的每一项都是 undefined，这样就非常方便的定义出所需要的数组了，但是这样定义的数组性能最差，具体可以参考 [constArray](https://jsperf.com/constarray/4) 的测试结果。

#### 1.1.3.2 数组去重合并

```js
function combine(){ 
  let arr = [].concat.apply([], arguments);  //没有去重复的新数组 
  return Array.from(new Set(arr));
} 

var m = [1, 2, 2], n = [2,3,3]; 
console.log(combine(m,n));                     // [1, 2, 3]
```

首先定义一个去重数组函数，通过 concat 把传入的数组进行合并到一个新的数组中去，通过 new Set () 可以对 arr 进行去重操作，再使用 `Array.from()` 返回一个拷贝后的数组。


## 1.2 Array.of(): 将一组值转换为数组 

`Array.of()`方法用于将一组值，转换为数组。

```js
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```

这个方法的主要目的，是弥补数组构造函数`Array()`的不足。因为参数个数的不同，会导致`Array()`的行为有差异。

```js
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
```

上面代码中，`Array()`方法没有参数、一个参数、三个参数时，返回的结果都不一样。只有当参数个数不少于 2 个时，`Array()`才会返回由参数组成的新数组。参数只有一个正整数时，实际上是指定数组的长度。

`Array.of()`基本上可以用来替代`Array()`或`new Array()`，并且不存在由于参数不同而导致的重载。它的行为非常统一。

```js
Array.of() // []
Array.of(undefined) // [undefined]
Array.of(1) // [1]
Array.of(1, 2) // [1, 2]
```

`Array.of()`总是返回参数值组成的数组。如果没有参数，就返回一个空数组。

`Array.of()`方法可以用下面的代码模拟实现。

```js
function ArrayOf(){
  return [].slice.call(arguments);
}
```

## 1.3 数组和字符串之间的转变 toString()	join()

### 1.3.1 数组转成字符串 
|方法名	|说明	|返回值|
|---|---|---|
|toString()	|把数组转换成字符串，逗号分隔每一项	|返回一个字符串|
|join(‘分隔符’)	|方法用于把数组中的所有元素转换为一个字符串	|返回一个字符串|

```js
// 1.toString() 将我们的数组转换为字符串
var arr = [1, 2, 3];
console.log(arr.toString()); // 1,2,3

// 2.join('分隔符')
var arr1 = ['green', 'blue', 'red'];
console.log(arr1.join()); // 不写默认用逗号分割
console.log(arr1.join('-')); //  green-blue-red
console.log(arr1.join('&')); // green&blue&red

console.log(listOfStuff);
let listAsString = "";
listAsString = listOfStuff.join();
console.log(listAsString, typeof listAsString);
// das Komma ist der default Seperator 

let letters = ["H","a","l","l","o"];
listAsString = letters.join("");
console.log(listAsString);

```

### 1.3.2 字符串转为数组  split ()
```js
//ist die Umkehrung von join() 

let alleNames = "Max, Klaus, Susi";
let eachName = alleNames.split(",");
console.log(eachName); // ['Max', ' Klaus', ' Susi']


// string内不含comma  但是 delimiter 设置成 comma
// 结果是 整个String 会变成 唯一一个 element in a array 
let alleNames = "Max Klaus Susi";
let eachName = alleNames.split(",");
console.log(eachName); // [Max Klaus Susi]

```

# 2 isArray()


本节介绍了判断一个值是数组类型的方法 `Array.isArray()` 此方法可以很准确地判断数组，学习了在 ES5 中判断数组类型的几个方法的缺陷。在不支持 ES6 的情况下也可以通过 `Object.prototype.toString` 自定义 `Array.isArray()` 方法。



在程序中判断数组是很常见的应用，但在 ES5 中没有能严格判断 JS 对象是否为数组，都会存在一定的问题，比较受广大认可的是借助 toString 来进行判断，很显然这样不是很简洁。ES6 提供了 `Array.isArray()` 方法更加简洁地判断 JS 对象是否为数组。

### 2.1.1 方法详情

判断 JS 对象，如果值是 `Array`，则为 true; 否则为 false。

**语法使用：**

```js
Array.isArray(obj)
```

**参数解释：**

| 参数  | 描述          |
|:--- |:----------- |
| obj | 需要检测的 JS 对象 |

### 2.1.2 ES5 中判断数组的方法

通常使用 `typeof` 来判断变量的数据类型，但是对数组得到不一样的结果

```js
// 基本类型
typeof 123;  //number
typeof "123"; //string
typeof true; //boolean

// 引用类型
typeof [1,2,3]; //object
```

上面的代码中，对于基本类型的判断没有问题，但是判断数组时，返回了 object 显然不能使用 `typeof` 来作为判断数组的方法。

#### 2.1.2.1 通过 instanceof 判断

`instanceof` 运算符用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链。

`instanceof` 可以用来判断数组是否存在，判断方式如下：

```js
var arr = ['a', 'b', 'c'];
console.log(arr instanceof Array);            // true 
console.log(arr.constructor === Array;); // true
```

在解释上面的代码时，先看下数组的原型链指向示意图：

![image-20220826200454480](https://i0.hdslb.com/bfs/album/a5e71101dce3f5bf36c1e004cba8b699f804fcb7.png)

数组实例的原型链指向的是 `Array.prototype` 属性，`instanceof` 运算符就是用来检测 `Array.prototype` 属性是否存在于数组的原型链上，上面代码中的 arr 变量就是一个数组，所有拥有 `Array.prototype` 属性，返回值 `true`，这样就很好的判断数组类型了。

但是，需要注意的是，`prototype` 属性是可以修改的，所以并不是最初判断为 `true` 就一定永远为真。

#### 2.1.2.2 通过 constructor 判断

我们知道，Array 是 JavaScript 内置的构造函数，构造函数属性（prototype）的 `constructor` 指向构造函数（见下图），那么通过 `constructor` 属性也可以判断是否为一个数组。

```js
var arr = new Array('a', 'b', 'c');
arr.constructor === Array;    //true
```

下面我们通过构造函数的示意图来进行分析：

![image-20220826200839160](https://i0.hdslb.com/bfs/album/679d04cac62904c293f0e7db186700ab8d6390a8.png)

由上面的示意图可以知道，我们 new 出来的实例对象上的原型对象有 `constructor` 属性指向构造函数 Array，由此我们可以判断一个数组类型。

但是 `constructor` 是可以被重写，所以不能确保一定是数组，如下示例：

```js
var str = 'abc';
str.constructor = Array;
str.constructor === Array // true
```

上面的代码中，str 显然不是数组，但是可以把 `constructor` 指向 Array 构造函数，这样再去进行判断就是有问题的了。

`constructor` 和 `instanceof` 也存在同样问题，不同执行环境下，`constructor` 的判断也有可能不正确。

### 2.1.3 Array.isArray () 的使用

下面我们通过示例来看下 `Array.isArray()` 是怎样判断数组的。

```js
// 下面的函数调用都返回 true
Array.isArray([]);
Array.isArray([10]);
Array.isArray(new Array());
Array.isArray(new Array('a', 'b', 'c'))
// 鲜为人知的事实：其实 Array.prototype 也是一个数组。
Array.isArray(Array.prototype); 

// 下面的函数调用都返回 false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray(new Uint8Array(32))
Array.isArray({ __proto__: Array.prototype });
```

上面的代码中对 JavaScript 中的数据类型做验证，可以很好地区分数组类型。

### 2.1.4 自定义 isArray

在 ES5 中比较通用的方法是使用 `Object.prototype.toString` 去判断一个值的类型，也是各大主流库的标准。在不支持 ES6 语法的环境下可以使用下面的方法给 `Array` 上添加 `isArray` 方法

```js
if (!Array.isArray){
  Array.isArray = function(arg){
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

