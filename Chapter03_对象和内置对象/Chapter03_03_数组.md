
# 1 数组的原理

- Array 为 一个 classe 的 name. 所有的数组对象 都是 Array 这个 class 的 子元素
- 数组的 index 从 0 开始 
- typeof of a array 为 object
```js
let listOfNames = ["Hans", "Peter", "Susanne"];
console.log(listOfNames, typeof listOfNames); // typeof listOfNames 得到的值 为 object 这几个字母 
```


## 1.1 dense array 和 sparse array 的区别
Ein Array, in dem alle Plätze besetzt sind, nennt sich dense array. Ein Array, in dem sich leere Plätze befinden ist ein sparse array.
dense array: 所有位置都有值 ` let listOfNames = ["Hans", "Peter", "Susanne"];` 
sparse array:  有 leere Plätze, 比如 `let listOfStuff = [1,2,3,,true,"Hallo Welt",false,null];`  null 不算做  leere Plätze

Im Rahmen von HTML-Dokumenten ist nicht zu vergessen, daß die HTML-Elemente keine vollwertigen Arrays sind, sondern Listen.

## 1.2 sparse array

```js
let listOfStuff = [1,2,3,,true,"Hallo Welt",false,null];
console.log(listOfStuff); // 显示为 [1, 2, 3, empty, true, 'Hallo Welt', false, null], 这里 3 后面那个 空白位 被显示 为 empty
console.log(listOfStuff.length); // 显示为 8,  说明 3 后面那个 空白位  也被计入 总长度了

listOfStuff[10] = 100;  listOfStuff 原先只有8 8 个, 直接在第10位 插入 100
```

# 2 数组的创建和方法
## 2.1 数组对象的创建
创建数组对象的两种方式

字面量方式: new Array()

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


## 2.3 添加删除数组元素
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



👉筛选数组
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



## 2.4 数组排序
|方法名	|说明	|是否修改原数组|
|---|---|---|
|reverse()	|颠倒数组中元素的顺序，无参数	|该方法会改变原来的数组，返回新数组|
|sort()|	对数组的元素进行排序	|该方法会改变原来的数组，返回新数组|
```js
// 1.翻转数组
var arr = ['pink','red','blue'];
arr.reverse();
console.log(arr);

// 2.数组排序(冒泡排序)
var arr1 = [3,4,7,1];
arr1.sort();
console.log(arr1);

// 对于双位数
var arr = [1,64,9,61];
arr.sort(function(a,b) {
     return b - a;  //降序的排列
     return a - b; //升序
 	}
 )
```


## 2.5 数组索引
|方法名	|说明|	返回值|
|---|---|---|
|indexOf()	|数组中查找给定元素的第一个索引	|如果存在返回索引号，如果不存在，则返回-1|
|lastIndexOf()	|在数组的最后一个索引，从后向前索引	|如果存在返回索引号，如果不存在，则返回-1|

```js
//返回数组元素索引号方法 indexOf(数组元素)  作用就是返回该数组元素的索引号
//它只发返回第一个满足条件的索引号
//如果找不到元素，则返回-1
var arr = ['red','green','blue','pink','blue'];
console.log(arr.indexOf('blue'));  // 2

console.log(arr.lastIndexOf('blue')); // 4
```


### 2.5.1 数组去重

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



## 2.6 数组转化为字符串
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
1
```


## 2.7 其他方法
|方法名	|说明	|返回值|
|---|---|---|
|concat()	|连接两个或多个数组 不影响原数组	|返回一个新的数组|
|slice()|	数组截取slice(begin,end)	|返回被截取项目的新数组|
|splice()	|数组删除splice(第几个开始要删除的个数)|返回被删除项目的新数组，这个会影响原数组|



