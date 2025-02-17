
# 1 数组的原理

数组(Array)是指一组数据的集合，其中的每个数据被称作元素，在数组中可以存放任意类型的元素。数组是一种将一组数据存储在单个变量名下的优雅方式。

//普通变量一次只能存储一个值
var num = 10;
//数组一次可以存储多个值
var arr =[1,2,3,4,5];

- Array 为 一个 classe 的 name. 所有的数组对象 都是 Array 这个 class 的 子元素
- 数组的 index 从 0 开始 
- typeof of a array 为 object
```js
let listOfNames = ["Hans", "Peter", "Susanne"];
console.log(listOfNames, typeof listOfNames); // typeof listOfNames 得到的值 为 object 这几个字母 
```

## 1.1 empty array
```js
/*empty array*/
let listOfSomething=[];
```


## 1.2 dense array 和 sparse array 的区别

Ein Array, in dem alle Plätze besetzt sind, nennt sich dense array. Ein Array, in dem sich leere Plätze befinden ist ein sparse array.
dense array: 所有位置都有值 ` let listOfNames = ["Hans", "Peter", "Susanne"];` 
sparse array:  有 leere Plätze, 比如 `let listOfStuff = [1,2,3,,true,"Hallo Welt",false,null];`  null 不算做  leere Plätze

Im Rahmen von HTML-Dokumenten ist nicht zu vergessen, daß die HTML-Elemente keine vollwertigen Arrays sind, sondern Listen.

### 1.2.1 sparse array

```js
let listOfStuff = [1,2,3,,true,"Hallo Welt",false,null];
console.log(listOfStuff); // 显示为 [1, 2, 3, empty, true, 'Hallo Welt', false, null], 这里 3 后面那个 空白位 被显示 为 empty
console.log(listOfStuff.length); // 显示为 8,  说明 3 后面那个 空白位  也被计入 总长度了

listOfStuff[10] = 100;  listOfStuff 原先只有8 8 个, 直接在第10位 插入 100
console.log(listOfStuff); //  显示为 [1, 2, 3, empty, true, 'Hallo Welt', false, null, empty × 2, 100]
console.log(listOfStuff.length); // 显示为 11 
```

# 2 数组常识 

## 2.1 数组对象的创建

JavaScript 中创建数组有两种方式：
利用 new 创建数组
利用数组字面量创建数组 字面量方式: new Array()

①利用 new 创建数组
```js
var 数组名 = new Array();
var arr = new Array(); //创建一个新的空数组
注意 Array()，A要大写


// Über den Konstruktor deklarieren
let arrKonstr = new Array();
console.log(arrKonstr);
for(let i=0; i<10; i++){
    arrKonstr[i] = ("a" + i);
}
console.log(arrKonstr);
```


②利用数组字面量创建数组
```js
// 1.利用数组字面量方式创建空的数组
var 数组名 =[];
// 2.使用数组字面量方式创建带初始值的数组
var 数组名 =['小白','小黑','小黄','瑞奇'];
// 3.数组中可以存放任意类型的数据，例如字符串，数字，布尔值等
var arrStus =['小白'，12,true,28.9];

```

数组的字面量是方括号
声明数组并赋值称为数组的初始化
这种字面量方式也是我们以后最多使用的方式

## 2.2 检测是否为数组
instanceof 运算符，可以判断一个对象是否属于某种类型
Array.isArray(对象的名字 ) 用于判断一个对象是否为数组，isArray() 是 HTML5 中提供的方法

```js
var arr = [1, 23];
var obj = {};
console.log(arr instanceof Array); // true
console.log(obj instanceof Array); // false
console.log(Array.isArray(arr));   // true
console.log(Array.isArray(obj));   // false
```

## 2.3 数组的索引（下标）
索引 (下标) ：用来访问数组元素的序号（数组下标从 0 开始）

```
//定义数组
var arrStus = [1,2,3];
//获取数组中的第2个元素
alert(arrStus[1]);
//
listOfNames[3]="Susanne";

```

## 2.4 数组的长度

使用“数组名.length”可以访问数组元素的数量（数组长度）

```
var arrStus = [1,2,3];
alert(arrStus.length);  // 3
```


注意：
此处数组的长度是数组元素的个数 ，不要和数组的索引号混淆
当我们数组里面的元素个数发生了变化，这个 length 属性跟着一起变化




# 3 扩展运算符 ES6 spreads arguments into a real Array
https://www.mediaevent.de/javascript/spread-operator.html

## 3.1 含义

扩展运算符（spread）是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

```js
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```

1扩展运算符可以将数组或者对象转为用逗号分隔的参数序列。
```js
let aty = [1, 2, 3];
// ...ary  // 1, 2, 3
console.log(...ary);  // 1 2 3 
```

2可以把对象里面的内容展开,合并到一个新的对象里面
```js
        let obj = {
            name:"zhangsan",
            age:12
        }
        let obj2 = {
            gender:'男',
            love:"meat",
            ...obj
        }
        console.log(...obj);
```



2扩展运算符可以应用于合并数组。
```js
//方法一 
let ary1 = [1, 2, 3];
let ary2 = [3, 4, 5];
let ary3 = [...ary1, ...ary2];  
// 方法二
ary1.push(...ary2);
```


3 将类(伪)数组或可遍历对象转换为正真的数组
```js
let oDivs = document.getElemenetsByTagName('div');
oDivs = [...oDivs];
```

4 可以把展开结果作为函数的实参

```javascript
let arr1 = [12,34,56]
let fn = (a,b,c)=>{
    console.log(a+b+c)
}
fn(...arr1)
```


1 该运算符主要用于函数调用。

```js
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers) // 42
```

上面代码中，`array.push(...items)`和`add(...numbers)`这两行，都是函数的调用，它们都使用了扩展运算符。该运算符将一个数组，变为参数序列。

2 扩展运算符与正常的函数参数可以结合使用，非常灵活。

```js
function f(v, w, x, y, z) { }
const args = [0, 1];
f(-1, ...args, 2, ...[3]);
```

3 扩展运算符后面还可以放置表达式。

```js
const arr = [
  ...(x > 0 ? ['a'] : []),
  'b',
];
```

4 如果扩展运算符后面是一个空数组，则不产生任何效果。

```js
[...[], 1]
// [1]
```

注意，只有函数调用时，扩展运算符才可以放在圆括号中，否则会报错。

```js
(...[1, 2])
// Uncaught SyntaxError: Unexpected number

console.log((...[1, 2]))
// Uncaught SyntaxError: Unexpected number

console.log(...[1, 2])
// 1 2
```

上面三种情况，扩展运算符都放在圆括号里面，但是前两种情况会报错，因为扩展运算符所在的括号不是函数调用。

## 3.2 替代函数的 apply() 方法

由于扩展运算符可以展开数组，所以不再需要`apply()`方法将数组转为函数的参数了。

```js
// ES5 的写法
function f(x, y, z) {
  // ...
}
var args = [0, 1, 2];
f.apply(null, args);

// ES6 的写法
function f(x, y, z) {
  // ...
}
let args = [0, 1, 2];
f(...args);
```

下面是扩展运算符取代`apply()`方法的一个实际的例子，应用`Math.max()`方法，简化求出一个数组最大元素的写法。

```js
// ES5 的写法
Math.max.apply(null, [14, 3, 77])

// ES6 的写法
Math.max(...[14, 3, 77])

// 等同于
Math.max(14, 3, 77);
```

上面代码中，由于 JavaScript 不提供求数组最大元素的函数，所以只能套用`Math.max()`函数，将数组转为一个参数序列，然后求最大值。有了扩展运算符以后，就可以直接用`Math.max()`了。

另一个例子是通过`push()`函数，将一个数组添加到另一个数组的尾部。

```js
// ES5 的写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);

// ES6 的写法
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
arr1.push(...arr2);
```

上面代码的 ES5 写法中，`push()`方法的参数不能是数组，所以只好通过`apply()`方法变通使用`push()`方法。有了扩展运算符，就可以直接将数组传入`push()`方法。

下面是另外一个例子。

```js
// ES5
new (Date.bind.apply(Date, [null, 2015, 1, 1]))

// ES6
new Date(...[2015, 1, 1]);
```

## 3.3 扩展运算符的应用


(0)扩展运算符可以将数组或者对象转为用逗号分隔的参数序列。
```js
let aty = [1, 2, 3];
// ...ary  // 1, 2, 3
console.log(...ary);  // 1 2 3 
```

**（1）复制数组**

数组是复合的数据类型，直接复制的话，只是复制了指向底层数据结构的指针，而不是克隆一个全新的数组。

```js
const a1 = [1, 2];
const a2 = a1;

a2[0] = 2;
a1 // [2, 2]
```

上面代码中，`a2`并不是`a1`的克隆，而是指向同一份数据的另一个指针。修改`a2`，会直接导致`a1`的变化。

ES5 只能用变通方法来复制数组。

```js
const a1 = [1, 2];
const a2 = a1.concat();

a2[0] = 2;
a1 // [1, 2]
```

上面代码中，`a1`会返回原数组的克隆，再修改`a2`就不会对`a1`产生影响。

扩展运算符提供了复制数组的简便写法。

```js
const a1 = [1, 2];
// 写法
const a2 = [...a1];
```

上面的两种写法，`a2`都是`a1`的克隆。

**（2）合并数组**

扩展运算符提供了数组合并的新写法。

```js
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];

// ES5 的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6 的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
```

不过，这两种方法都是浅拷贝，使用的时候需要注意。

```js
const a1 = [{ foo: 1 }];
const a2 = [{ bar: 2 }];

const a3 = a1.concat(a2);
const a4 = [...a1, ...a2];

a3[0] === a1[0] // true
a4[0] === a1[0] // true
```

上面代码中，`a3`和`a4`是用两种不同方法合并而成的新数组，但是它们的成员都是对原数组成员的引用，这就是浅拷贝。如果修改了引用指向的值，会同步反映到新数组。

**(4）字符串转为数组**

扩展运算符还可以将字符串转为真正的数组。

```js
console.log(...'alex');                // a l e x
console.log('a', 'l', 'e', 'x');    // a l e x

console.log([...'alex']);            // [ 'a', 'l', 'e', 'x' ]
// ES6 之前字符串转数组是通过：'alex'.split('');
```

**（5）类数组转为数组**

```js
// arguments
function func() {
    console.log(arguments);            // [Arguments] { '0': 1, '1': 2 }
    console.log([...arguments]);    // [ 1, 2 ]
}
func(1, 2);

// NodeList
console.log([...document.querySelectorAll('p')].push);
```


**（6）可以把展开结果作为函数的实参 **

```javascript
let arr1 = [12,34,56]
let fn = (a,b,c)=>{
    console.log(a+b+c)
}
fn(...arr1)
```


