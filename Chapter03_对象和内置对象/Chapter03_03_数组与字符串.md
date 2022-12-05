
# 1 数组对象
## 1.1 数组对象的创建
创建数组对象的两种方式

字面量方式
new Array()

## 1.2 检测是否为数组
instanceof 运算符，可以判断一个对象是否属于某种类型
Array.isArray() 用于判断一个对象是否为数组，isArray() 是 HTML5 中提供的方法

```js
var arr = [1, 23];
var obj = {};
console.log(arr instanceof Array); // true
console.log(obj instanceof Array); // false
console.log(Array.isArray(arr));   // true
console.log(Array.isArray(obj));   // false
```


## 1.3 添加删除数组元素
|方法名	|说明|	返回值|
|--|--|--|
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



## 1.4 数组排序
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


## 1.5 数组索引
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


### 1.5.1 数组去重

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



## 1.6 数组转化为字符串
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


## 1.7 其他方法
|方法名	|说明	|返回值|
|---|---|---|
|concat()	|连接两个或多个数组 不影响原数组	|返回一个新的数组|
|slice()|	数组截取slice(begin,end)	|返回被截取项目的新数组|
|splice()	|数组删除splice(第几个开始要删除的个数)|返回被删除项目的新数组，这个会影响原数组|



# 2 字符串对象
## 2.1 基本包装类型
为了方便操作基本数据类型，JavaScript 还提供了三个特殊的引用类型：String、Number和 Boolean。
基本包装类型就是把简单数据类型包装成为复杂数据类型，这样基本数据类型就有了属性和方法。

我们看看下面代码有什么问题吗？

var str = 'andy';
console.log(str.length);


按道理基本数据类型是没有属性和方法的，而对象才有属性和方法，但上面代码却可以执行，这是因为 js 会把基本数据类型包装为复杂数据类型，
其执行过程如下 ：
// 1.生成临时变量,把简单类型包装为复杂数据类型
var temp = new String('andy');
// 2.赋值给我们声明的字符变量
str = temp;
// 3.销毁临时变量
temp = null;


## 2.2 字符串的不可变
指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。

```js
var str = 'abc';
str = 'hello';
// 当重新给 str 赋值的时候，常量'abc'不会被修改，依然在内存中
// 重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
// 由于字符串的不可变，在大量拼接字符串的时候会有效率问题
var str = '';
for(var i = 0; i < 10000;  i++){
    str += i;
}
console.log(str);
// 这个结果需要花费大量时间来显示，因为需要不断的开辟新的空间
```



## 2.3 根据字符返回位置
字符串所有的方法，都不会修改字符串本身(字符串是不可变的)，操作完成会返回一个新的字符串

方法名	说明
indexOf(‘要查找的字符’，开始的位置): 	返回指定内容在元字符串中的位置，如果找不到就返回-1，开始的位置是index索引号
lastIndexOf():	从后往前找，只找第一个匹配的

```js

 // 字符串对象  根据字符返回位置  str.indexOf('要查找的字符', [起始的位置])
        var str = '改革春风吹满地，春天来了';
        console.log(str.indexOf('春')); //默认从0开始查找 ，结果为2
        console.log(str.indexOf('春', 3)); // 从索引号是 3的位置开始往后查找，结果是8
        
```



### 2.3.1 返回字符位置
查找字符串 “abcoefoxyozzopp” 中所有o出现的位置以及次数

核心算法：先查找第一个o出现的位置
然后 只要 indexOf返回的结果不是 -1 就继续往后查找
因为 indexOf 只能查找到第一个，所以后面的查找，一定是当前索引加1，从而继续查找

```js
var str = "oabcoefoxyozzopp";
var index = str.indexOf('o');
var num = 0;
// console.log(index);
while (index !== -1) {
    console.log(index);
    num++;
    index = str.indexOf('o', index + 1);
}
console.log('o出现的次数是: ' + num);
```


## 2.4 根据位置返回字符
|方法名	|说明|	使用|
|---|---|---|
|charAt(index)|	返回指定位置的字符(index字符串的索引号)	|str.charAt(0)|
|charCodeAt(index)	获取指定位置处字符的ASCII码(index索引号)|	str.charCodeAt(0)|
|str[index]|	获取指定位置处字符|	HTML,IE8+支持和charAt()等效|

返回字符位置: 
判断一个字符串 “abcoefoxyozzopp” 中出现次数最多的字符，并统计其次数
核心算法：利用 charAt() 遍历这个字符串
把每个字符都存储给对象， 如果对象没有该属性，就为1，如果存在了就 +1
遍历对象，得到最大值和该字符

```html
<script>
    // 有一个对象 来判断是否有该属性 对象['属性名']
    var o = {
        age: 18
    }
    if (o['sex']) {
        console.log('里面有该属性');

    } else {
        console.log('没有该属性');

    }

    //  判断一个字符串 'abcoefoxyozzopp' 中出现次数最多的字符，并统计其次数。
    // o.a = 1
    // o.b = 1
    // o.c = 1
    // o.o = 4
    // 核心算法：利用 charAt() 遍历这个字符串
    // 把每个字符都存储给对象， 如果对象没有该属性，就为1，如果存在了就 +1
    // 遍历对象，得到最大值和该字符
    var str = 'abcoefoxyozzopp';
    var o = {};
    for (var i = 0; i < str.length; i++) {
        var chars = str.charAt(i); // chars 是 字符串的每一个字符
        if (o[chars]) { // o[chars] 得到的是属性值
            o[chars]++;
        } else {
            o[chars] = 1;
        }
    }
    console.log(o);
    // 2. 遍历对象
    var max = 0;
    var ch = '';
    for (var k in o) {
        // k 得到是 属性名
        // o[k] 得到的是属性值
        if (o[k] > max) {
            max = o[k];
            ch = k;
        }
    }
    console.log(max);
    console.log('最多的字符是' + ch);
</script>

```

## 2.5 字符串操作方法
方法名	说明
concat(str1,str2,str3…): 	concat() 方法用于连接两个或对各字符串。拼接字符串🔥
substr(start,length): 	从 start 位置开始(索引号), length 取的个数。🔥
slice(start,end): 	从 start 位置开始，截取到 end 位置 ，end 取不到 (两个都是索引号)
substring(start,end): 	从 start 位置开始，截取到 end 位置 ，end 取不到 (基本和 slice 相同，但是不接受负)

```html
<script>
    // 1. concat('字符串1','字符串2'....)
    var str = 'andy';
    console.log(str.concat('red'));

    // 2. substr('截取的起始位置', '截取几个字符');
    var str1 = '改革春风吹满地';
    console.log(str1.substr(2, 2)); // 第一个2 是索引号的2   第二个2 是取几个字符
</script>
```


## 2.6 replace()方法
replace() 方法用于在字符串中用一些字符替换另一些字符

其使用格式：replace(被替换的字符,要替换为的字符串)

```html
<script>
    // 1. 替换字符 replace('被替换的字符', '替换为的字符')  它只会替换第一个字符
    var str = 'andyandy';
    console.log(str.replace('a', 'b'));
    // 有一个字符串 'abcoefoxyozzopp'  要求把里面所有的 o 替换为 *
    var str1 = 'abcoefoxyozzopp';
    while (str1.indexOf('o') !== -1) {
        str1 = str1.replace('o', '*');
    }
    console.log(str1);
</script>
```



## 2.7 split()方法
split() 方法用于切分字符串，它可以将字符串切分为数组。在切分完毕之后，返回的是一个新数组。

例如下面代码：
```js
var str = 'a,b,c,d';
console.log(str.split(','));
// 返回的是一个数组 ['a', 'b', 'c', 'd']


```

```html
<script>
// 2. 字符转换为数组 split('分隔符')    前面我们学过 join 把数组转换为字符串
    var str2 = 'red, pink, blue';
    console.log(str2.split(','));
    var str3 = 'red&pink&blue';
    console.log(str3.split('&'));
</script>
```

## 2.8 大小写转换
toUpperCase() 转换大写
toLowerCase() 转换小写
