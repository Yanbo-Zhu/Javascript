# 1 ES6

什么是 ES6？
ES 的全称是 ECMAScript, 他是由 ESMA 国际标准化组织，制定的一项脚本语言的标准化规范。

年份	版本
2015年6月	ES2015
2016年6月	ES2016
2017年6月	ES2017
2018年6月	ES2018
ES6 实际上是一个泛指，泛指 ES2015 及后续的版本。

为什么使用 ES6？
每一次标准的诞生都意味着语言的完善，功能的加强。JavaScript语言本身也有一些令人不满意的地方。
变量提升特性增加了程序运行时的不可预测性
语法过于松散，实现相同的功能，不同的人可能会写出不同的代码

# 2 ES6的新增语法

## 2.1 定义变量
### 2.1.1 let、const、var 的区别


|var	|let	|const|
|---|---|---|
|函数级作用域|	块级作用域|	块级作用域|
|变量提升	|不存在变量提升|	不存在变量提升|
|值可更改|	值可更改	|值不可更改|

1. 使用var声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象。
2. 使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升。
3. 使用 const 声明的常量，在后面出现的代码中不能修改该常量的值。

### 2.1.2 let、const与var的区别
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
       
         {
             let num = 100
             console.log(num)
         }
         console.log(num)//会报错
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


### 2.1.3 let与const的区别
1.let可以重复赋值，const不可以重复赋值
        let num = 100;
        num = 200;

        const num = 100;
        num = 200;//会报错

2.let定义的时候可以不赋值，const定义的时候就要赋值
       let num;
       const num;//会报错



### 2.1.4 let变量声明及声明特性
1、变量声明
let a;
let b,c,d;
let e=100;
let f=342,g='fgsddgf',h=[];

2、声明特性
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

### 2.1.5 const常量
声明常量，常量就是值(内存地址) 不能变化的量

1、声明常量
const SCHOOL='sgg';

2、特点
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




## 2.2 数组解构对象解构
es6允许按照一定模式从数组和对象中提取值，对变量进行赋值，这被称为解构赋值
1、数组的解构
```js
const F4=['xsy','ln','zs','sxb'];
let [x,l,z,s]=F4;
 //这样就相当于x='xsy',l='ln',z='zs',s='sxb'

 let [a, b, c] = [1, 2, 3];
console.log(a);
console.log(b);
console.log(c);    


// 如果解构不成功，变量的值为undefined 
let [foo] = [];
let [bar, foo] = [1];   


按照之前的写法，获取数组元素的方法就是：
       let a = arr[0];
       let b = arr[1];
       let c = arr[2];
```

2、对象的解构
```js
let person = { name: 'zhangsan', age: 20 }; 
let { name, age } = person;
console.log(name); // 'zhangsan'
console.log(age); // 20    
          
let {name: myName, age: myAge} = person; // myName myAge 属性别名
console.log(myName); // 'zhangsan' 
console.log(myAge); // 20 


按照之前的写法，获取对象值的方法就是：

       let username = obj.username;
       let age = obj.age;
       let password = obj.password;

现在用解构赋值就可以简写成：

        let {age,username,password} = obj;
        console.log(username,age,password)

```


## 2.3 箭头函数 
1 ES6中新增的定义函数的方法。
```js
() => {}    
const fn = () => {}


var f = v => v;
上面的箭头函数等同于：
var f = function(v) {
  return v;
};
```

2  形参个数
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

3 代码数量
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
var getTempItem = id => ({ id: id, name: "Temp" });
```


4 其他
箭头函数可以与变量解构结合使用。
```js
const full = ({first,last}) => first + ' ' + last;

//等同于
function full(person){
   return person.first + ' ' + person.last;
}
```


箭头函数的一个用处是简化回调函数。
```js
//ES5写法
[1,2,3].map(function(x)){
    return x * x;
}

//ES6写法
[1,2,3].map(x => x * x);
```

### 2.3.1 使用注意点
1 箭头函数有几个使用注意点。

（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。

2 箭头函数this指向问题
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

3 函数传递参数设置默认值
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



## 2.4 剩余参数

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

# 3 ES6的内置对象扩展
## 3.1 模板字符串
1、声明（反引号）
let str = `我也是字符串`;

### 3.1.1 特点
特点1: 模板字符串中可以解析变量。
```js
let name = '张三';
let sayHello = `hello,my name is ${name}`; // hello,my name is zhangsan 

```


特点2: 内容中可以直接出现换行符
```js
let str =`<ul>
			<li>sdgsdg</li>
			<li>sdgsdg</li>
			<li>sdgsdg</li>
			<li>sdgsdg</li>
		  </ul>`

let resilt = {
    name: 'zhangsan',
    age: 20,
    sex：'男'
}
let html = ` <div>
    <span>${result.name}</span>
    <span>${result.name}</span>
    <span>${result.name}</span>
</div> `;

```


特点3、变量拼接
```js
let lovest ='dfsd';
let out = `${lovest}dgdgdgs`;
//out就为dfsddgdgdgs
```


特点4: 在模板字符串可以调用函数。

```js
const aryHello = function () {
    return '哈哈哈哈 追不到我吧 我就是这么强大';
};
let greet = `${sayHello()} 哈哈哈哈`;
console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈 
```


## 3.2 Array 
### 3.2.1 扩展运算符 (展开语法) 
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

### 3.2.2 构造函数方法： Array.from() 

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



### 3.2.3 实例方法：find() 
用于找出第一符合条件的数组成员，如果没有找到返回undefined
```js
let ary = [{
    id: 1,
    name: '张三' 
},{
    id: 2,
    name: '李四'
}];
let target = ary.find((item, index) => item.id == 2);
```


### 3.2.4 实例方法：findIndex()
用于找出第一个符合条件的数组成员的位置，如果没有找到返回-1
```js
let ary =[1, 5, 10, 15];
let index = ary.findIndex((value,index) => value > 9);
console.log(index); // 2   
```


### 3.2.5 实例方法：includes()
表示某个数组是否包含给定的值，返回布尔值

```js
[1, 2, 3].includes(2); // true
[1, 2, 3].includes(4); // false
```



## 3.3 String 的扩展方法 
### 3.3.1 实例方法：startsWith() 和 endsWith()
startsWith(): 表示参数字符串是否在原字符串的头部，返回布尔值
endsWith(): 表示参数字符串是否在原字符串的尾巴，返回布尔值

```js
let str = 'Hello world!';
str.startsWith('Hello') // true
str.endsWith('!')       // true
```


### 3.3.2 实例方法： repeat() 
repeat 方法表示将原字符串重复n次，返回一个新字符串。

'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"

## 3.4 Set 数据结构 
ES6 提供了新的数据结构 Set 它类似于数组 但是成员的值都是唯一的 没有重复的值

Set本身是一个构造函数，用来生成 Set 数据结构。
const s = new Set;

Set函数可以接受一个数组作为参数，用来初始化。
const set = new Set([1, 2 ,3 ,4 , 5]);

### 3.4.1 实例方法
add(value): 添加某个值，返回Set结构本身
delete(value): 删除某个值，返回一个布尔值，表示删除是否成功
has(value): 返回一个布尔值，表示该值是否为Set的成员
clear(): 清除所有成员，没有返回值


```js
const s = new Set();
s.add(1).add(2).add(3);     // 向 set 结构中添加值
s.delete(2)                 // 删除 set 结构中的2值
s.has(1)                    // 表示 set 结构中是否有1这个值 返回布尔值 
s.clear()                   // 清除 set 结构中的所有值    
```
                 

### 3.4.2 遍历
Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值
s.forEach(value => console.log(value))   
