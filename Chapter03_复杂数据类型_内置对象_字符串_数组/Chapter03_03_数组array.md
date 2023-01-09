
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

//定义数组
var arrStus = [1,2,3];
//获取数组中的第2个元素
alert(arrStus[1]);

## 2.4 数组的长度
使用“数组名.length”可以访问数组元素的数量（数组长度）

var arrStus = [1,2,3];
alert(arrStus.length);  // 3


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




# 4 数组的方法


## 4.1 遍历数组 (for, forEach(), for in )

用 listOfStuff[i].value 是无效的, 是会报错的 

```js
// 数组索引访问数组中的元素
var arr = ['red','green', 'blue'];
console.log(arr[0]) // red
console.log(arr[1]) // green
console.log(arr[2]) // blue

// for zeigt auch leere Elemente als undefined;   does show empty slots as undefined
// empty 处 显示 为 undefined in Console 
// booleanische Value (值 为 true 或者 false) . 值 为 null, 值为字符串类型的  处的 元素 都能正常显示. 
for(let i=0; i<listOfStuff.length; i++){
    console.log(listOfStuff[i]);  
}


// for循环遍历数组
var arr = ['red','green', 'blue'];
for (var i = 0; i < arr.length; i++){
    console.log(arrStus[i]);
}

// for...in zeigt nicht die leeren Elemente
// empty 处 显示 不会显示为 undefined in Console, 根本就不显示在 console 中. do not show undefineds,
// booleanische Value (值 为 true 或者 false) . 值 为 null, 值为字符串类型的  处的 元素 都能正常显示. 
for(let item in listOfStuff){
    console.log(listOfStuff[item]);
}

// forEach() zeigt nicht die leeren Elemente
// empty 处 显示 不会显示为 undefined in Console, 根本就不显示在 console 中 
// booleanische Value (值 为 true 或者 false) . 值 为 null, 值为字符串类型的  处的 元素 都能正常显示. 
 
listOfStuff.forEach(element => {
    console.log(element);
});
```


```js
 /*write a function that takes any array or list and some text 
 and iterates over the array with for*/
 
 function denseArray(arr,text){
  let showArr="";	
  let i=0;
  let len=arr.length;
  for(i;i<len;i++){
   showArr+=" "+arr[i];
  }
  console.log("for: " + text + showArr);
 }

 denseArray(listOfStuff, "listOfStuff");
 
 console.log("--------------1");




 /*write a function that takes any array or list and some text 
 and iterates of the array with for-in*/
 function sparseArray(arr,text){
  let showArr="";
  for(let item in arr){
   showArr+=" "+arr[item];
  }
  console.log("for in: "+ text + showArr);
 }

 sparseArray(listOfStuff,"listOfStuff");




 /*Write it again as Arrow-Function*/
 const denseArr = (arr, text) => {
    let showArr = "";
    for (let item in arr) {
      showArr += " " + arr[item];
    }
    let result = "for: " + text + showArr;
    return result;
  };
 console.log(denseArr(listOfStuff, "listOfStuff"));





 /* Write it again with forEach() */
  const denseForEach = (arr, text) => {
    let showArr = "";
    arr.forEach(element => {
      showArr += " " + element;
    });
    let result = "forEach(): " + text + showArr;
    return result;
  };

  console.log(denseForEach(listOfStuff, "listOfStuff: "));
```

## 1.1 forEach()
array.forEach(function(currentValue,index,arr))

currentValue : 数组当前项的值
index: 数组当前项的索引
arr: 数组对象本身

```html
<body>
    <script>
        // forEach 迭代(遍历) 数组
        var arr = [1, 2, 3];
        var sum = 0;
        arr.forEach(function(value, index, array) {
            console.log('每个数组元素' + value);
            console.log('每个数组元素的索引号' + index);
            console.log('数组本身' + array);
            sum += value;
        })
        console.log(sum);
    </script>
</body>
```



## 4.2 数组中新增元素
①通过修改 length 长度新增数组元素
可以通过修改 length 长度来实现数组扩容的目的

length 属性是可读写的

var arr = ['red', 'green', 'blue', 'pink'];
arr.length = 7;
console.log(arr);
console.log(arr[4]);
console.log(arr[5]);
console.log(arr[6]);

其中索引号是 4，5，6 的空间没有给值，就是声明变量未给值，默认值就是 undefined

②通过修改数组索引新增数组元素
可以通过修改数组索引的方式追加数组元素

不能直接给数组名赋值，否则会覆盖掉以前的数据

这种方式也是我们最常用的一种方式

var arr = ['red', 'green', 'blue', 'pink'];
arr[4] = 'hotpink';
console.log(arr);


### 4.2.1 例子

1.新建一个数组，里面存放10个整数（ 1~10）， 要求使用循环追加的方式输出： [1,2,3,4,5,6,7,8,9,10]

①使用循环来追加数组。
②声明一个空数组 arr。
③循环中的计数器 i 可以作为数组元素存入。
由于数组的索引号是从0开始的， 因此计数器从 0 开始更合适，存入的数组元素要+1。

```js
var arr = [];
for (var i = 0; i < 10; i++){
    arr[i] = i + 1;
}
console.log(arr);
```


2.将数组 [2, 0, 6, 1, 77, 0, 52, 0, 25, 7] 中大于等于 10 的元素选出来，放入新数组

①声明一个新的数组用于存放新数据。
②遍历原来的数组，找出大于等于 10 的元素。
③依次追加给新数组 newArr。


实现代码1：
```js
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
// 定义一个变量 用来计算 新数组的索引号
var j = 0;
for (var i = 0; i < arr.length; i++) {
    if (arr[i] >= 10) {
        // 给新数组
        newArr[j] = arr[i];
        // 索引号 不断自加
        j++;
    }
}
console.log(newArr);
```

实现代码2：
```js
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
for (var i = 0; i < arr.length; i++) {
    if (arr[i] >= 10) {
        // 给新数组
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```


## 4.3 删除指定数组元素


将数组[2, 0, 6, 1, 77, 0, 52, 0, 25, 7]中的 0 去掉后，形成一个不包含 0 的新数组。

1
```js
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
for(var i = 0; i <arr.length; i++){
    if(arr[i] != 0){
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```


2 
//老师代码
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];   // 空数组的默认的长度为 0 
// 定义一个变量 i 用来计算新数组的索引号

```js
for (var i = 0; i < arr.length; i++) {
    // 找出大于 10 的数
    if (arr[i] != 0) {
        // 给新数组
        // 每次存入一个值，newArr长度都会 +1  
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```




## 4.4 修改数组元素的方法 push() pop() unshift() shift()
|方法名	|说明|	返回值|
|--|--|--|
|listOfStuff[8] = 100; | listOfStuff 原先只有 4 位, 直接在第八位 插入 100 ||
|push(参数1…)	|末尾添加一个或多个元素，注意修改原数组	|并返回新的长度|
|pop()	|删除数组最后一个元素	|返回它删除的元素的值|
|unshift(参数1…)	|向数组的开头添加一个或更多元素，注意修改原数组	|并返回新的长度|
|shift()	|删除数组的第一个元素，数组长度减1，无参数，修改原数组	|并返回第一个元素|



```js
// 1.push() 在我们数组的末尾，添加一个或者多个数组元素 push 推
var arr = [1, 2, 3];
arr.push(4, '秦晓');
console.log(arr);
console.log(arr.push(4, '秦晓'));
console.log(arr);
// push 完毕之后，返回结果是新数组的长度


// 2. unshift 在我们数组的开头 添加一个或者多个数组元素
arr.unshift('red');
console.log(arr);

// pop() 它可以删除数组的最后一个元素，一次只能删除一个元素
arr.pop(); //不加参数
// shift() 它剋删除数组的第一个元素,一次只能删除一个元素
arr.shift(); //不加参数
```



例子: 筛选数组
有一个包含工资的数组[1500,1200,2000,2100,1800],要求把数组中工资超过2000的删除，剩余的放到新数组里面
```js
var arr = [1500, 1200, 2000, 2100, 1800];
var newArr = [];
for (var i = 0; i < arr.length; i++) {
    if (arr[i] < 2000) {
        newArr.push(arr[i]);
    }
}
console.log(newArr);
```



## 4.5 翻转数组 reverse()	
|方法名	|说明	|是否修改原数组|
|---|---|---|
|reverse()	|颠倒数组中元素的顺序，无参数	|该方法会改变原来的数组，返回新数组|
|sort()|	对数组的元素进行排序	|该方法会改变原来的数组，返回新数组|

1

```js
// 1.翻转数组
var arr = ['pink','red','blue'];
arr.reverse();
console.log(arr);  

反转前: ['H', 'a', 'l', 'l', 'o', '!']
反转后: ['!', 'o', 'l', 'l', 'a', 'H']

```

2 
将数组 [‘red’, ‘green’, ‘blue’, ‘pink’, ‘purple’] 的内容反过来存放

// 把旧数组索引号的第4个取过来(arr.length - 1),给新数组索引号第0个元素(newArr.length)

```js
var arr = ['red','green','blue','pink','purple'];
var newArr = [];
for (var i = arr.length -1; i>=0; i--){
    newArr[newArr.length] = arr[i];
}
console.log(newArr);
```



## 4.6 数组排序 sort()

|方法名	|说明	|是否修改原数组|
|---|---|---|
|reverse()	|颠倒数组中元素的顺序，无参数	|该方法会改变原来的数组，返回新数组|
|sort()|	对数组的元素进行排序	|该方法会改变原来的数组，返回新数组|

### 4.6.1 不给入自定义的 vergleichsfunktion
按照  alphabetisch 排序
Wird kein Argument übergeben, dann wird das array alphabetisch sortiert.

sort 的排序规则 很奇怪 

Sort 的结果
1. Nummer 在前: 1, 100, 2, 3
2. 然后是 string
3. 然后是 boolean value 混杂着 null, 按照  alphabetisch 排序
4. 然后是 empty, undefined Elemente werden an das Ende des arrays gesetzt.

```js
var arr1 = [3,4,7,1];
arr1.sort();
console.log(arr1);


 let numbers = [7,1,102,40,10];
  console.log(numbers);  // [7, 1, 102, 40, 10]
 console.log(numbers.sort()); // [1, 10, 102, 40, 7]


let listOfAllTypes = [true,5,null,1,100,,undefined,"a","A","b","B","z",false,"f","F","g","m","s",null];
console.log(listOfAllTypes);
listOfAllTypes.sort();
console.log(listOfAllTypes); // [1, 100, 5, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty]



console.log(listOfStuff);  // [1, 2, 3, empty, true, 'Hallo Welt', false, null, empty × 2, 100]
console.log(listOfStuff.sort()); // [1, 100, 2, 3, 'Hallo Welt', false, null, true, empty × 3]    
```

### 4.6.2 自定义的 Vergleichsfunktion 
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

A 为当前元素, b 为下一个元素 
如果 compareFn(a, b) 大于 0，b 会被排列到 a 之前。
如果 compareFn(a, b) 小于 0，那么 a 会被排列到 b 之前；
如果 compareFn(a, b) 等于 0，a 和 b 的相对位置不变。备注：ECMAScript 标准并不保证这一行为，而且也不是所有浏览器都会遵守（例如 Mozilla 在 2003 年之前的版本）；
compareFn(a, b) 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。

function(a,b){return a-b;} : Wenn a<b,  a-b 小于零, 则a 这个元素就往link移动 ,  a 会被排列到 b 之前
function(a,b){return b-a;} : Wenn a<b,  a-b 大于零, 则b 这个元素就往link移动 ,  b 会被排列到 a 之前

```js
// 对于双位数
var arr = [1,64,9,61];
arr.sort(function(a,b) {
     return b - a;  //降序的排列
     return a - b; //升序
 	}
 )


// 可以变为 arrow function
listOfStuff.sort(function(a,b){return a-b;});
listOfNumbers.sort((a,b) => a-b);
```

```js
 listOfAllTypes = [1, 100, 5, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty];
 console.log(listOfAllTypes);  // [1, 100, 5, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty]
 
 listOfAllTypes.sort((a,b) => a-b);
 console.log(listOfAllTypes); // [1, 5, 100, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty]
 
 listOfAllTypes.sort((a,b) => b-a);
 console.log(listOfAllTypes); // [100, 5, 1, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', true, null, null, 's', 'z', undefined, empty]


 listOfAllTypes = [true,5,null,1,100,,undefined,"a","A","b","B","z",false,"f","F","g","m","s",null];
 console.log(listOfAllTypes);
 listOfAllTypes.sort((a,b) => a-b);
 console.log(listOfAllTypes); // [null, true, 1, 5, 100, 'a', 'A', 'b', 'B', 'z', false, 'f', 'F', 'g', 'm', 's', null, undefined, empty]
 listOfAllTypes.sort((a,b) => b-a);
 console.log(listOfAllTypes); //  [100, 5, true, 1, null, 'a', 'A', 'b', 'B', 'z', false, 'f', 'F', 'g', 'm', 's', null, undefined, empty]


```

### 4.6.3 冒泡排序
将数组 [5, 4, 3, 2, 1]中的元素按照从小到大的顺序排序，输出： 1，2，3，4，5

```js
var arr = [5,4,3,2,1];
for (var i = 0; i < arr.length-1; i++){ //外层循环管趟数，5个数共交换4躺
    for (var j = 0; j <= arr.length - i - 1; j++){
        //里层循环管每一趟交换的次数
        //前一个和后面一个数组元素相比较
        if(arr[j] > arr[j+1]){
            var temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }  
    }
}
console.log(arr);
```



## 4.7 数组索引 indexOf() lastIndexOf()
|方法名	|说明|	返回值|
|---|---|---|
|indexOf(true, 4)或者 indexOf("Z") 	|数组中查找给定元素的第一个索引	|如果存在返回索引号，如果不存在，则返回-1, gibt den index eines gesuchten Wertes zurück, Wird ein Wert nicht gefunden, liefert sie -1 zurück|
|lastIndexOf()	|在数组的最后一个索引，从后向前索引, den ersten Index von hinten 	|如果存在返回索引号，如果不存在，则返回-1|

 gibt den index eines gesuchten Wertes aus einem array zurück. 
 Wenn ein Wert nicht gefunden wird, dann gibt die Methode -1 zurück.
 Dabei wird das array mit indexOf() von vorn beginnend durchlaufen 
 und mit lastIndexOf() von hinten.
 Optional kann als zweites Argument der index übergeben werden, 
 ab dem gesucht werden soll.

```js
var arr = ['red','green','blue','pink','blue'];

console.log(arr.indexOf('blue'));  // 2
console.log(listOfStuff.indexOf(red,4));   // erst ab index=4 suchen:


console.log(arr.lastIndexOf('blue')); // 4

// 如果是查找字符串的话, 是 case -sensitive 的
listOfStuff.push("z");
console.log(listOfStuff.indexOf("Z")); // 结果是 找不到 显示  -1 

``` 


### 4.7.1 数组去重

分析：把旧数组里面不重复的元素选取出来放到新数组中，重复的元素只保留一个，放到新数组中去重。

核心算法：我们遍历旧数组，然后拿着旧数组元素去查询新数组，如果该元素在新数组里面没有出现过，我们就添加，否则不添加。

我们怎么知道该元素没有存在？ 利用 新数组.indexOf(数组元素) 如果返回是 -1 就说明 新数组里面没有改元素

```js
// 封装一个去重的函数 unique 独一无二的
function unique(arr) {
    var newArr = [];
    for (var i = 0; i < arr.length; i++) {
        if (newArr.indexOf(arr[i]) === -1) {
            newArr.push(arr[i]);
        }
    }
    return newArr;
}
var demo = unique(['c', 'a', 'z', 'a', 'x', 'a', 'x', 'c', 'b']);
console.log(demo);
```




## 4.8 数组的连接截取 
|方法名	|说明	|返回值|
|---|---|---|
|concat()	|连接两个或多个数组 不影响原数组	|返回一个新的数组, 原来的数组不受影响|
|slice()|	数组截取slice(begin,end)	|返回被截取项目的新数组,  原来的数组不受影响|
|splice()	|数组删除splice(第几个开始要删除的个数), 从某个位置移除数组的几个元素 ，并在这个位置上添加新元素|原数组被改为被删除项目后的数组，会return一个数组, 这个额数据包含了 那些元素被删除了|

### 4.8.1 concat()
```js
 console.log(numbers); // [1, 7, 10, 40, 102]
 let newList=numbers.concat(4,5);  
 console.log(newList); // [1, 7, 10, 40, 102, 4, 5]
 console.log(numbers); // [1, 7, 10, 40, 102]
 
 newList=numbers.concat(newList,['aha'],[true,false,[0]],5678);
 console.log(newList); // [1, 7, 10, 40, 102, 1, 7, 10, 40, 102, 4, 5, 'aha', true, false, Array(1), 5678]

```


### 4.8.2 slice()
给入两个值 
 Die Methode gibt einen beliebigen Teilbereich aus einem array zurück.   Mit zwei Argumenten werden Anfang und Ende des Teilbereiches spezifiziert. 
 Dabei wird der Wert des ersten Argumentes mit ausgegeben, aber nicht der des zweiten. Das ursprüngliche array wird nicht verändert.
```js
 console.log(numbers); //[ 1, 7, 10, 40, 102]
 let partNumbers = numbers.slice(1,3); //   从 index =1 的地方开始取值, 到 index=3 , index=3 的值不被取
 console.log(partNumbers); // [7, 10]
```

给入一个值 
Wird nur ein Argument übergeben, dann spezifiziert dieses den Anfang des Teilbereiches und das Ende wird durch das Ende des array spezifiziert.
从 index =3 的地方开始取值, 
取到最后 最后一个值要被取进去 
```js
 console.log(numbers.slice(3)); // [40, 102]
 
```

Negative Argumente beginnen mit dem Teilbereich am Ende des arrays, zählen aber nach rechts.
从 index 为倒数第三的地方开始取,  包括 index=-3 的这个位置  的地方开始取值,  取到最后, 最后一个值要被取进去 
```js
 console.log(numbers.slice(-3));
```

### 4.8.3 splice()
entfernen und hinzufügen

 Mit dieser Methode können Elemente sowohl eingefügt als auch entfernt werden.  Dabei wird das ursprüngliche array verändert.
  Die Methode gibt ein array zurück, welches die entfernten Elemente enthält.  
 - Das erste Argument spezifiziert die Position des Einfügens oder Entfernens.
 - Das zweite Argument spezifiziert die Anzahl der Elemente,  die entfernt werden sollen.
 - Wird das zweite Argument nicht übergeben, wird das Ende des Arrays angenommen.
 - Ab dem 3. Argument kann hinzugefügt werden.

 
```js
console.log(numbers); //  [1, 7, 10, 40, 102]
let spliceNumber = numbers.splice(1,0,5,true);
console.log(spliceNumber); // []
console.log(numbers); // [1, 5, true, 7, 10, 40, 102]


console.log(numbers); //  [1, 7, 10, 40, 102]
let spliceNumber = numbers.splice(1,1,5,true);
console.log(spliceNumber); // [7]
console.log(numbers); // [1, 5, true,10, 40, 102]


// Übung: finde alle true und entferne sie
function findTrue(arr){
    let i=0;
    while(i !== -1){
        i = arr.indexOf(true);
        console.log(i);
        arr.splice(i,1);
    }
}

findTrue(listOfStuff);
console.log(listOfStuff);

```

# 5 案例

1.请将 [“关羽”,“张飞”,“马超”,“赵云”,“黄忠”,“刘备”,“姜维”]; 数组里的元素依次打印到控制台

var arr = ["关羽","张飞","马超","赵云","黄忠","刘备","姜维"]; 
// 遍历  从第一个到最后一个
for(var i = 0; i < arr.length; i++ )  { 
   console.log( arr[i] );
} 


2.求数组 [2,6,1,7, 4] 里面所有元素的和以及平均值

①声明一个求和变量 sum。
①遍历这个数组，把里面每个数组元素加到 sum 里面。
①用求和变量 sum 除以数组的长度就可以得到数组的平均值。
```js
var arr = [2, 6, 1, 7, 4];
var sum = 0;
var average = 0;
for (var i = 0; i < arr.length; i++) {
    sum += arr[i];
}
average = sum / i; //此时i为5
//      average = sum / arr.length;
console.log('和为' + sum);
console.log('平均值为' + average);
```


3.求数组[2,6,1,77,52,25,7]中的最大值

①声明一个保存最大元素的变量 max。
②默认最大值可以取数组中的第一个元素。
③遍历这个数组，把里面每个数组元素和 max 相比较。
④如果这个数组元素大于max 就把这个数组元素存到 max 里面，否则继续下一轮比较。
⑤最后输出这个 max。

方法1
```js
 var arr = [2, 6, 1, 77, 52, 25, 7];
        var max = arr[0];
        var temp;
        for (var i = 0; i < arr.length; i++) {
            if (max < arr[i]) {
                temp = max;
                max = arr[i];
                arr[i] = temp;
            }
        }
        console.log('最大值为' + max);

```


方法二：
```js
var arrNum = [2,6,1,77,52,25,7];
var maxNum = arrNum[0]; // 用来保存最大元素,默认最大值是数组中的第一个元素
// 从0 开始循环数组里的每个元素
for(var i = 0;i< arrNum.length; i++){
    // 如果数组里当前循环的元素大于 maxNum，则保存这个元素和下标
    if(arrNum[i] > maxNum){
        maxNum = arrNum[i]; // 保存数值到变量 maxNum
    }
}
```


4.将数组 [‘red’, ‘green’, ‘blue’, ‘pink’] 里面的元素转换为字符串

思路：就是把里面的元素相加就好了，但是注意保证是字符相加

①需要一个新变量 str 用于存放转换完的字符串。
②遍历原来的数组，分别把里面数据取出来，加到字符串变量 str 里面。
```js
var arr = ['red','green','blue','pink'];
var str ='';
for(var i = 0; i < arr.length; i++){
    str += arr[i];
}
console.log(str);
// redgreenbluepink

```


5.将数组 [‘red’, ‘green’, ‘blue’, ‘pink’] 转换为字符串，并且用 | 或其他符号分割

①需要一个新变量用于存放转换完的字符串 str。
①遍历原来的数组，分别把里面数据取出来，加到字符串里面。
①同时在后面多加一个分隔符。

```js
var arr = ['red', 'green', 'blue', 'pink'];
var str = '';
var separator = '|';
for (var i = 0; i < arr.length; i++) {
   str += arr[i] + separator;
}
console.log(str);
// red|green|blue|pink

```

## 5.1 案例: hangman

https://codepen.io/cathydutton/pen/JjpxMm
https://codesandbox.io/s/z9fhk?file=/src/index.js:3525-3536
https://itsourcecode.com/free-projects/jsprojects/hangman-game-javascript-from-scratch-with-source-code/