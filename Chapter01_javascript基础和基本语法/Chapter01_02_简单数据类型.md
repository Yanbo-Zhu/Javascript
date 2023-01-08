https://blog.csdn.net/Augenstern_QXL/article/details/119249534


# 2 数据类型

## 2.1 数据类型简介

（1）为何需要数据类型
在计算机中，不同的数据所需占用的存储空间是不同的，为了便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型。

简单来说，数据类型就是数据的类别型号。

比如姓名“张三”，年龄18，这些数据的类型是不一样的。

（2）变量的数据类型
变量是用来存储值的所在处，它们有名字和数据类型。 变量的数据类型决定了如何将代表这些值的位存储到计算机的内存中。
JavaScript 是一种弱类型或者说动态语言。
这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。
js 中根据值就就可以自动确定数据类型 , Datentypen werden in js bestimmt durch den Wert, der in ihnen gerade enthalten ist: 
java就需要提前声明变量的类型了

```js
<script>
    //int num = 10;  这是java的
    var num;// 这里的num 我们是不确定属于哪种数据类型的
    var num = 10;
    //js 的变量数据类型是只有程序在运行过程中，根据等号右边的值来确定的
    var str = '秀儿'; //str 是字符串型
    // js是动态语言，变量的数据类型是可以变化的
    var x = 20; // x 是数字型
    x = '洛水'; //x变成了字符串型
</script>
```

（3）数据类型的分类
简单数据类型 （Number,String,Boolean,Undefined,Null）
复杂数据类型 （object)

(4) <mark> 变量的数据类型随时可以更换, 只要给入的值变了 </mark> 
und sind somit veränderbar über die Laufzeit des Skriptes:

## 2.2 简单数据类型 / 基本数据类型 Number,String,Boolean,Undefined,Null, empty
|简单数据类型	|说明	|默认值|
|--|---|---|
|Number	|数字型，包含整型值和浮点型值，如21，0.21	|0|
|Boolean	|布尔值类型，如true，false ，等价于1和0	|false|
|Undefined	|var a; 声明了变量a但是没有赋值，此时a=undefined.  kein Wert, kein Typ	|undefined（未定义的）|
|string	|字符串类型，如“张三”|“”
|Null	|var a = null;声明了变量a为空值	|null|
|object| hat Untertypen: object, array, function, null: kein Wert||

undefined und null sind gleichzeitig Typ und Wert

例子:
```javascript
const NUM = 2; 
let nothing = undefined;
let nothingAgain = null;
let n = 0;
let m = 1;
let test = true;
let sign = "1";

// strings
let text1 = "doppelte Anführungszeichen";
let text2 = 'einfache Anführungszeichen';
// Beides ist erlaubt und richtig.
// Seien Sie konsistent und tun Sie es immer gleich!
    
```

### 2.2.1 数字型 Number
JavaScript 数字类型既可以用来保存整数值，也可以保存小数(浮点数）。

var age = 21; // 整数
var Age = 21.3747; // 小数

(1)数字型进制
最常见的进制有二进制、八进制、十进制、十六进制。
```js
// 1.八进制 0~7 程序里面数字前面加0 表示八进制
var num1 = 010;//8
console.log(num1); //010 八进制转十进制 就是8
var num2 = 012;
console.log(num2);//10
// 2.十六进制 0~9 a~f数字前面加上0x表示十六进制
var num3 = 0x9;
console.log(num3);//9
var num4 = 0xa;
console.log(num4);//10
```

现阶段只需要记住，在JS中八进制前面加0，十六进制前面加 0x

(2 )数字型范围
JavaScript中数值的最大和最小值

**最大值：**Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
**最小值：**Number.MIN_VALUE，这个值为：5e-32

// 3.数字型的最大值
console.log(Number.MAX_VALUE);
// 4.数字型的最小值
console.log(Number.MIN_VALUE);

(3)数字型三个特殊值

Infinity ，代表无穷大，大于任何数值
Infinity ，代表无穷小，小于任何数值
NaN ，Not a number，代表一个非数值

alert(Infinity); // Infinity
alert(-Infinity); // -Infinity
alert(NaN); // NaN

(4) isNaN()

用来判断一个变量是否为非数字的类型，返回 true 或者 false
isNaN(x) x是一个非数字类型
- x是数字 返回false
- x不是数字 返回true

console.log(isNaN(12));//false
console.log(isNaN('风云溪'));//true

### 2.2.2 字符串型 string

字符串型可以是引号中的任意文本，其语法为 “双引号” 和 "单引号’’
var strMsg = "我爱北京天安门~";		//使用双引号表示字符串
var strMsg = '我爱北京';			  //使用单引号表示字符串


因为 HTML 标签里面的属性使用的是双引号，JS 这里我们更推荐使用单引号。  

(1)字符串引号嵌套
JS可以用 单引号嵌套双引号，或者用 双引号嵌套单引号（外双内单，外单内双）
```js
var strMsg ='我是一个“高富帅”' //可以用 ' ' 包含 " "
var strMsg2 ="我是'高富帅'" //可以用" "  包含  ''


// strings
let text1 = "doppelte Anführungszeichen";
let text2 = 'einfache Anführungszeichen';
// Beides ist erlaubt und richtig.
// Seien Sie konsistent und tun Sie es immer gleich!

```




(2)字符串转义符🔥
类似HTML里面的特殊字符，字符串中也有特殊字符，我们称之为转义符。

转义符都是 \ 开头的，常用的转义符及其说明如下：

转义符	解释说明
\n	 换行符，n是newline
\ \	斜杠\
\ ’	   单引号
\ ‘’	双引号
\ t	tab 缩进
\ b	空格，b是blank的意思

(3)字符串长度🔥
字符串是由若干字符组成的，这些字符的数量就是字符串的长度。通过字符串的 length 属性可以获取整个字符串的长度。
```js
//通过字符串的length属性可以获取整个字符串的长度
var strMsg = "我是高富帅！";
alert(strMsg.length);     //显示6
```




(4)字符串的拼接🔥
多个字符串之间可以使用 + 进行拼接，其拼接方式为 字符串 + 任何类型 = 拼接之后的新字符串
拼接前会把与字符串相加的任何类型转成字符串，再拼接成一个新的字符串
注意：字符串 + 任何类型 =拼接之后的新字符串

```js

//1 字符串相加
alert('hello' + ' ' + 'World');  //hello World

//2 数值字符串相加
alert('100' + '100'); //100100

//3 数值字符串+数值
alert('12'+12); //1212

//4 数值+数值
alert(12+12); //24
```


+ 号总结口诀：🌏数值相加，字符相连🌏
```js
var  age = 18;
console.log('我今年'+age+'岁');
console.log('我今年'+age+'岁');  //引引加加，最终也是上面的形式
```


(5)字符串拼接加强🔥


我们经常会将字符串和变量来拼接，因为变量可以很方便地修改里面的值
变量是不能添加引号的，因为加引号的变量会变成字符串
如果变量两侧都有字符串拼接，口诀==🌏“引引加加 ”，删掉数字🌏==变量写加中间


```js
console.log('Pink老师' + 18);			//只要有字符就会相连
var age = 18;
// console.log('Pink老师age岁了');		//这样不行,会输出 "Pink老师age岁了"

console.log('Pink老师' + age);		 // Pink老师18
console.log('Pink老师' + age + '岁啦');	// Pink老师18岁啦
```


#### 2.2.2.1 template literals
template literals sind auch strings

```js
    let tempLit = `literal`;
    console.log(tempLit, typeof tempLit);
    // Damit können wir auch gut Variablen auslesen.
    console.log(`Strings können ${text1} und ${text2} enthalten!`);


对比: 
console.log(m + " ist gleich " + test);
console.log(`${m} ist ungleich ${test}`);
```



### 2.2.3 布尔型Boolean
布尔类型有两个值：true 和 false ，其中 true 表示真（对），而 false 表示假（错）。
布尔型和数字型相加的时候， true 的值为 1 ，false 的值为 0。
```js
var flag = true;
console.log(flag + 1); // 2 true当加法来看当1来看，flase当0来看

```


### 2.2.4 undefined未定义🔥
一个声明后没有被赋值的变量会有一个默认值 undefined ( 如果进行相连或者相加时，注意结果）
```js
// 如果一个变量声明未赋值，就是undefined 未定义数据类型
var str;
console.log(str);				//undefined
var variable = undefined;
console.log(variable + 'Pink'); //undefinedPink
console.log(variable + 18); //NaN 
```

1.undefined 和 字符串 相加，会拼接字符串

2.undefined 和 数字相加，最后结果是NaN

### 2.2.5 空值null
一个声明变量给 null 值，里面存的值为空
```js
var space = null;
console.log(space + 'pink'); //nullpink
console.llog(space + 1); // 1 
```



## 2.3 获取变量数据类型

### 2.3.1 typeof
typeof 可用来获取检测变量的数据类型
```js
var num = 18;
console.log(typeof num) // 结果 number  
```


不同类型的返回值

|类型	|例	|结果|
|--|---|---|
|string	|typeof “小白”	|“string”|
|number	|typeof 18	|“number”|
|boolean	|typeof true	|“boolean”|
|undefined	|typeof undefined	|“undefined”|
|null|	typeof null	|“object”|

```js
var num = 20;
console.log(typeof num);//number
var str ='码农';
console.log(typeof str);//string
var flag = true;
console.log(typeof flag);//boolean
var vari = undefined;
console.log(typeof vari);//undefined
var timer = null;
console.log(typeof timer);//object(对象)
// prompt 取过来的值是字符串型
var age = prompt("请输入你的年龄");
console.log(age);
console.log(typeof age);//string
```

### 2.3.2 字面量
字面量是在源代码中一个固定值的表示法，通俗来说，就是字面量表示 如何表达这个值。

- 数字字面量：8，9，10
- 字符串字面量：‘大前端’，‘后端’
- 布尔字面量：true、false

通过控制台的颜色判断属于哪种数据类型: 
黑色: 字符串
蓝色: 数值
灰色: undefined 和 null

```js
	<script>
        // 以下每一类型的颜色都是不一样的
        console.log(10);
        console.log('10');
        console.log("10");
        console.log(true);
        console.log(undefined);
        console.log(null);
    </script>

```

## 2.4 数据类型转换
使用表单、prompt 获取过来的数据默认是字符串类型的，此时就不能直接简单的进行加法运算，而需要转换变量的数据类型。通俗来说，就是把一种数据类型的变量转换成另外一种数据类型。

我们通常会实现3种方式的转换：

转换为字符串类型
转换为数字型
转换为布尔型

### 2.4.1 转换为字符串型🔥
|方式	|说明	|案例|
|--|--|--|
|toString()	|转成字符串	|var num = 1; alert(num.toString());|
|String()强制转换	|转成字符串	|var num = 1; alert(String(num));|
|加号拼接字符串|	和字符串拼接的结果都是字符串|	var num =1; alert(num+“我是字符串”);|


toString() 和 String() 使用方式不一样
三种转换方式，我们更喜欢用第三种加号拼接字符串转换方式，这一方式也称为隐士转换

```js
//1.把数字型转换为字符串型 toString()  变量.toString()
var num = 10;
var str = num.toString();
console.log(str);

//2.强制转换
console.log(String(num));
1
```



### 2.4.2 转换为数字型🔥
|方式	|说明|	案例|
|---|---|---|
|parselnt(string)函数	|将string类型转成整数数值型	|parselnt(‘78’)|
|parseFloat(string)函数	|将string类型转成浮点数数值型	|parseFloat(‘78.21’)|
|Number()强制转换函数	|将string类型转换为数值型	|Number(‘12’)|
|js 隐式转换(- * /)	|利用算术运算隐式转换为数值型	|‘12’-0|

```js
// 1.parseInt()
var age =prompt('请输入您的年龄');
consolo.log(parseInt(age));  //数字型18
consolo.log(parseInt('3.14'));  //3取整
consolo.log(parseInt('3.94'));  //3,不会四舍五入
consolo.log(parseInt('120px'));  //120,会去掉单位

// 2.parseFloat()
console.log(parseFloat('3.14'));  //3.14
consolo.log(parseFloat('120px'));  //120,会去掉单位


// 3.利用Number(变量)
var str ='123';
console.log(Number(str));
console.log(Number('12'));   

// 4.利用了算术运算 - * /   隐式转换
console.log('12'-0);  // 12
console.log('123' - '120');  //3
console.log('123' * 1);  // 123
```


1.注意 parseInt 和 parseFloat ，这两个是重点
2.隐式转换是我们在进行算数运算的时候，JS自动转换了数据类型

### 2.4.3 转换为布尔型
|方法	|说明	|案例|
|---|---|---|
|Boolean()函数	|其他类型转成布尔值	|Boolean(‘true’);|

- 代表空，否定的值会被转换为false，如 ’ ’ , 0, NaN , null , undefined
- 其余的值都会被被转换为true

```js
console.log(Boolean('')); //false
console.log(Boolean(0));  //false
console.log(Boolean(NaN)); //false
console.log(Boolean(null)); //false
console.log(Boolean(undefined)); //false
console.log(Boolean('小白')); //true
console.log(Boolean(12));   //true
```


