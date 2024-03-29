

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


# 3 数组的其他方法


## 3.1 find()，findIndex(), findLast()，findLastIndex()

1
数组实例的`find()`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

```js
[1, 4, -5, 10].find((n) => n < 0)
// -5
```

上面代码找出数组中第一个小于 0 的成员。

```js
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

上面代码中，`find()`方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

2 
数组实例的`findIndex()`方法的用法与`find()`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

```js
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```

这两个方法都可以接受第二个参数，用来绑定回调函数的`this`对象。

```js
function f(v){
  return v > this.age;
}
let person = {name: 'John', age: 20};
[10, 12, 26, 15].find(f, person);    // 26
```

上面的代码中，`find()`函数接收了第二个参数`person`对象，回调函数中的`this`对象指向`person`对象。

另外，这两个方法都可以发现`NaN`，弥补了数组的`indexOf()`方法的不足。

```js
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

上面代码中，`indexOf()`方法无法识别数组的`NaN`成员，但是`findIndex()`方法可以借助`Object.is()`方法做到。

`find()`和`findIndex()`都是从数组的0号位，依次向后检查。

3 
[ES2022](https://github.com/tc39/proposal-array-find-from-last) 新增了两个方法`findLast()`和`findLastIndex()`，从数组的最后一个成员开始，依次向前检查，其他都保持不变。

```js
const array = [
  { value: 1 },
  { value: 2 },
  { value: 3 },
  { value: 4 }
];

array.findLast(n => n.value % 2 === 1); // { value: 3 }
array.findLastIndex(n => n.value % 2 === 1); // 2
```

上面示例中，`findLast()`和`findLastIndex()`从数组结尾开始，寻找第一个`value`属性为奇数的成员。结果，该成员是`{ value: 3 }`，位置是2号位。

## 3.2 flat()

Dimension des Arrays auf 1 herabsetzen, alle Werte
```js
let a = [0, 1, 2, 3, 4, [5, 6, null]];
a.flat(Infinity);  // 0,1,2,3,4,5,6,

```
  
## 3.3 filter()

array.filter(function(currentValue,index,arr))
filter()方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组
注意它直接返回一个新数组
-   currentValue : 数组当前项的值
-   index ：数组当前项的索引
-   arr : 数组对象本身

```js
let a = [0, 1, 2, 3, 4, [5, 6, null]];

// Das Filtern auf genau jene Elemente, für die die Bedingung WAHR lautet (hier: ungerade Zahlen)
a.filter((i) => {return i % 2 == 1 ? true : false;});  // 1,3

```

```html
<body>
    <script>
        // filter 筛选数组
        var arr = [12, 66, 4, 88, 3, 7];
        var newArr = arr.filter(function(value, index) {
            // return value >= 20;
            return value % 2 === 0;
        });
        console.log(newArr);
    </script>
</body>

```



`filter()`方法用于过滤数组成员，满足条件的成员组成一个新数组返回。

它的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。该方法不会改变原数组。

```js
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})
// [4, 5]
```

上面代码将大于`3`的数组成员，作为一个新数组返回。

```js
var arr = [0, 1, 'a', false];

arr.filter(Boolean)
// [1, "a"]
```

上面代码中，`filter()`方法返回数组`arr`里面所有布尔值为`true`的成员。

`filter()`方法的参数函数可以接受三个参数：当前成员，当前位置和整个数组。

```js
[1, 2, 3, 4, 5].filter(function (elem, index, arr) {
  return index % 2 === 0;
});
// [1, 3, 5]
```

上面代码返回偶数位置的成员组成的新数组。

`filter()`方法还可以接受第二个参数，用来绑定参数函数内部的`this`变量。

```js
var obj = { MAX: 3 };
var myFilter = function (item) {
  if (item > this.MAX) return true;
};

var arr = [2, 8, 3, 4, 1, 3, 2, 9];
arr.filter(myFilter, obj) // [8, 4, 9]
```

上面代码中，过滤器`myFilter()`内部有`this`变量，它可以被`filter()`方法的第二个参数`obj`绑定，返回大于`3`的成员。

## 3.4 map()

`map()`方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。

```js
    let a = [0, 1, 2, 3, 4, [5, 6, null]];

 // Die Abbildung jeden Wertes auf je ein Funktionsergebnis (hier: gerade Zahlen)
    a.map((i) => {return i * 2;});  // 0,2,4,6,8,NaN

    
```

```js
var numbers = [1, 2, 3];

numbers.map(function (n) {
  return n + 1;
});
// [2, 3, 4]

numbers
// [1, 2, 3]
```

上面代码中，`numbers`数组的所有成员依次执行参数函数，运行结果组成一个新数组返回，原数组没有变化。

`map()`方法接受一个函数作为参数。该函数调用时，`map()`方法向它传入三个参数：当前成员、当前位置和数组本身。

```js
[1, 2, 3].map(function(elem, index, arr) {
  return elem * index;
});
// [0, 2, 6]
```

上面代码中，`map()`方法的回调函数有三个参数，`elem`为当前成员的值，`index`为当前成员的位置，`arr`为原数组（`[1, 2, 3]`）。

`map()`方法还可以接受第二个参数，用来绑定回调函数内部的`this`变量（详见《this 变量》一章）。

```js
var arr = ['a', 'b', 'c'];

[1, 2].map(function (e) {
  return this[e];
}, arr)
// ['b', 'c']
```

上面代码通过`map()`方法的第二个参数，将回调函数内部的`this`对象，指向`arr`数组。

如果数组有空位，`map()`方法的回调函数在这个位置不会执行，会跳过数组的空位。

```js
var f = function (n) { return 'a' };

[1, undefined, 2].map(f) // ["a", "a", "a"]
[1, null, 2].map(f) // ["a", "a", "a"]
[1, , 2].map(f) // ["a", , "a"]
```

上面代码中，`map()`方法不会跳过`undefined`和`null`，但是会跳过空位。

## 3.5 reduce()

`reduce()`方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，`reduce()`是从左到右处理（从第一个成员到最后一个成员）。

语法:`arr.reduce(function(累计值, 当前元素){}, 起始值)`

```js
[1, 2, 3, 4, 5].reduce(function (a, b) {
  console.log(a, b);
  return a + b;
})
// 1 2
// 3 3
// 6 4
// 10 5
//最后结果：15


   // Die Reduktion des Array-Inhalts (hier: 10 und das einzelne Array [5,6,null] !)
       let a = [0, 1, 2, 3, 4, [5, 6, null]];
    a.reduce((p, n) => {return p + n;});  // 105,6,

    
```

上面代码中，`reduce()`方法用来求出数组所有成员的和。`reduce()`的参数是一个函数，数组每个成员都会依次执行这个函数。如果数组有 n 个成员，这个参数函数就会执行 n - 1 次。

- 第一次执行：`a`是数组的第一个成员`1`，`b`是数组的第二个成员`2`。
- 第二次执行：`a`为上一轮的返回值`3`，`b`为第三个成员`3`。
- 第三次执行：`a`为上一轮的返回值`6`，`b`为第四个成员`4`。
- 第四次执行：`a`为上一轮返回值`10`，`b`为第五个成员`5`。至此所有成员遍历完成，整个方法的返回值就是最后一轮的返回值`15`。

`reduce()`方法的第一个参数都是一个函数。该函数接受以下四个参数。

1. 累积变量。第一次执行时，默认为数组的第一个成员；以后每次执行时，都是上一轮的返回值。
2. 当前变量。第一次执行时，默认为数组的第二个成员；以后每次执行时，都是下一个成员。
3. 当前位置。一个整数，表示第二个参数（当前变量）的位置，默认为`1`。
4. 原数组。

这四个参数之中，只有前两个是必须的，后两个则是可选的。

```js
[1, 2, 3, 4, 5].reduce(function (
  a,   // 累积变量，必须
  b,   // 当前变量，必须
  i,   // 当前位置，可选
  arr  // 原数组，可选
) {
  // ... ...
```

如果要对累积变量指定初值，可以把它放在`reduce()`方法的第二个参数。

```js
[1, 2, 3, 4, 5].reduce(function (a, b) {
  return a + b;
}, 10);
// 25
```

上面代码指定参数`a`的初值为10，所以数组从10开始累加，最终结果为25。注意，这时`b`是从数组的第一个成员开始遍历，参数函数会执行5次。

建议总是加上第二个参数，这样比较符合直觉，每个数组成员都会依次执行`reduce()`方法的参数函数。另外，第二个参数可以防止空数组报错。

```js
function add(prev, cur) {
  return prev + cur;
}

[].reduce(add)
// TypeError: Reduce of empty array with no initial value
[].reduce(add, 1)
// 1
```

上面代码中，由于空数组取不到累积变量的初始值，`reduce()`方法会报错。这时，加上第二个参数，就能保证总是会返回一个值。

**总结**

```js
//reduce 返回函数累计处理的结果，经常用于求和等
/*
计值参数：
1. 如果有起始值，则以起始值为准开始累计， 累计值 = 起始值
2. 如果没有起始值， 则累计值以数组的第一个数组元素作为起始值开始累计
3. 后面每次遍历就会用后面的数组元素 累计到 累计值 里面（类似求和里面的 sum ）
*/
```

## 3.6 some()，every()


这两个方法类似“断言”（assert），返回一个布尔值，表示判断数组成员是否符合某种条件。

它们接受一个函数作为参数，所有数组成员依次执行该函数。该函数接受三个参数：当前成员、当前位置和整个数组，然后返回一个布尔值。

注意，对于空数组，`some`方法返回`false`，`every`方法返回`true`，回调函数都不会执行。

```js
function isEven(x) { return x % 2 === 0 }

[].some(isEven) // false
[].every(isEven) // true
```

`some`和`every`方法还可以接受第二个参数，用来绑定参数函数内部的`this`变量。

### 3.6.1 some()
some()方法用于检测数组中的元素是否满足指定条件（查找数组中是否有满足条件的元素）
注意它返回的是布尔值，如果查找到这个元素，就返回true，如果查找不到就返回false
如果找到第一个满足条件的元素，则终止循环，不再继续查找
-   currentValue : 数组当前项的值
-   index ：数组当前项的索引
-   arr : 数组对象本身


```html
<body>
    <script>
        // some 查找数组中是否有满足条件的元素 
        var arr1 = ['red', 'pink', 'blue'];
        var flag1 = arr1.some(function(value) {
            return value == 'pink';
        });
        console.log(flag1);
        // 1. filter 也是查找满足条件的元素 返回的是一个数组 而且是把所有满足条件的元素返回回来
        // 2. some 也是查找满足条件的元素是否存在  返回的是一个布尔值 如果查找到第一个满足条件的元素就终止循环
    </script>
</body>
```


`some`方法是只要一个成员的返回值是`true`，则整个`some`方法的返回值就是`true`，否则返回`false`。

```js
var arr = [1, 2, 3, 4, 5];
arr.some(function (elem, index, arr) {
  return elem >= 3;
});
// true
```

上面代码中，如果数组`arr`有一个成员大于等于3，`some`方法就返回`true`。

### 3.6.2 every()


`every`方法是所有成员的返回值都是`true`，整个`every`方法才返回`true`，否则返回`false`。

```js
var arr = [1, 2, 3, 4, 5];
arr.every(function (elem, index, arr) {
  return elem >= 3;
});
// false
```

上面代码中，数组`arr`并非所有成员大于等于`3`，所以返回`false`。



## 3.7 fill()

`arr.fill(value[, start[, end]])`方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
起始索引，默认值为 0。
终止索引，默认值为 this.length。

```js
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

上面代码表明，`fill`方法用于空数组的初始化非常方便。数组中已有的元素，会被全部抹去。

`fill`方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。

```js
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

上面代码表示，`fill`方法从 1 号位开始，向原数组填充 7，到 2 号位之前结束。

注意，如果填充的类型为对象，那么被赋值的是同一个内存地址的对象，而不是深拷贝对象。

```js
let arr = new Array(3).fill({name: "Mike"});
arr[0].name = "Ben";
arr
// [{name: "Ben"}, {name: "Ben"}, {name: "Ben"}]

let arr = new Array(3).fill([]);
arr[0].push(5);
arr
// [[5], [5], [5]]
```

## 3.8 at()

长久以来，JavaScript 不支持数组的负索引，如果要引用数组的最后一个成员，不能写成`arr[-1]`，只能使用`arr[arr.length - 1]`。

这是因为方括号运算符`[]`在 JavaScript 语言里面，不仅用于数组，还用于对象。对于对象来说，方括号里面就是键名，比如`obj[1]`引用的是键名为字符串`1`的键，同理`obj[-1]`引用的是键名为字符串`-1`的键。由于 JavaScript 的数组是特殊的对象，所以方括号里面的负数无法再有其他语义了，也就是说，不可能添加新语法来支持负索引。

为了解决这个问题，ES2022为数组实例增加了`at()`方法，接受一个整数作为参数，返回对应位置的成员，并支持负索引。这个方法不仅可用于数组，也可用于字符串和类型数组（TypedArray）。

```js
const arr = [5, 12, 8, 130, 44];
arr.at(2) // 8
arr.at(-2) // 130
```

如果参数位置超出了数组范围，`at()`返回`undefined`。

```js
const sentence = 'This is a sample sentence';

sentence.at(0); // 'T'
sentence.at(-1); // 'e'

sentence.at(-100) // undefined
sentence.at(100) // undefined
```

## 3.9 entries()，keys() 和 values()

ES6 提供三个新的方法——`entries()`，`keys()`和`values()`——用于遍历数组。它们都返回一个遍历器对象，可以用`for...of`循环进行遍历，唯一的区别是`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。

```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

## 3.10 includes()
表示某个数组是否包含给定的值，返回布尔值
`Array.prototype.includes`方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的`includes`方法类似。ES2016 引入了该方法。

```js
[1, 2, 3].includes(2)     // true
[1, 2, 3].includes(4)     // false
[1, 2, NaN].includes(NaN) // true
```

该方法的第二个参数表示搜索的起始位置，默认为`0`。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为`-4`，但数组长度为`3`），则会重置为从`0`开始。

```js
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```

没有该方法之前，我们通常使用数组的`indexOf`方法，检查是否包含某个值。

```js
if (arr.indexOf(el) !== -1) {
  // ...
}
```

`indexOf`方法有两个缺点，一是不够语义化，它的含义是找到参数值的第一个出现位置，所以要去比较是否不等于`-1`，表达起来不够直观。二是，它内部使用严格相等运算符（`===`）进行判断，这会导致对`NaN`的误判。

```js
[NaN].indexOf(NaN)
// -1
```

`includes`使用的是不一样的判断算法，就没有这个问题。

```js
[NaN].includes(NaN)
// true
```

另外，Map 和 Set 数据结构有一个`has`方法，需要注意与`includes`区分。

- Map 结构的`has`方法，是用来查找键名的，比如`Map.prototype.has(key)`、`WeakMap.prototype.has(key)`、`Reflect.has(target, propertyKey)`。
- Set 结构的`has`方法，是用来查找值的，比如`Set.prototype.has(value)`、`WeakSet.prototype.has(value)`。

## 3.11 toReversed()，toSorted()，toSpliced()，with()

很多数组的传统方法会改变原数组，比如`push()`、`pop()`、`shift()`、`unshift()`等等。数组只要调用了这些方法，它的值就变了。现在有一个提案，允许对数组进行操作时，不改变原数组，而返回一个原数组的拷贝。

这样的方法一共有四个。

- `Array.prototype.toReversed() -> Array`
- `Array.prototype.toSorted(compareFn) -> Array`
- `Array.prototype.toSpliced(start, deleteCount, ...items) -> Array`
- `Array.prototype.with(index, value) -> Array`

它们分别对应数组的原有方法。

- `toReversed()`对应`reverse()`，用来颠倒数组成员的位置。
- `toSorted()`对应`sort()`，用来对数组成员排序。
- `toSpliced()`对应`splice()`，用来在指定位置，删除指定数量的成员，并插入新成员。
- `with(index, value)`对应`splice(index, 1, value)`，用来将指定位置的成员替换为新的值。

上面是这四个新方法对应的原有方法，含义和用法完全一样，唯一不同的是不会改变原数组，而是返回原数组操作后的拷贝。

下面是示例。

```js
const sequence = [1, 2, 3];
sequence.toReversed() // [3, 2, 1]
sequence // [1, 2, 3]

const outOfOrder = [3, 1, 2];
outOfOrder.toSorted() // [1, 2, 3]
outOfOrder // [3, 1, 2]

const array = [1, 2, 3, 4];
array.toSpliced(1, 2, 5, 6, 7) // [1, 5, 6, 7, 4]
array // [1, 2, 3, 4]

const correctionNeeded = [1, 1, 3];
correctionNeeded.with(1, 2) // [1, 2, 3]
correctionNeeded // [1, 1, 3]
```

