https://blog.csdn.net/Augenstern_QXL/article/details/119249534

# 1 注释

1 单行注释 :  // xxx
快捷键ctrl + /

2 多行注释
快捷键 shift + alt + a

```
/*
    多行注释
*/    
```

# 2 输入输出语句

| 方法                     | 说明                            | 归属  |
| ---------------------- | ----------------------------- | --- |
| alert(msg);            | 浏览器弹出警示框. 主要用来显示消息给用户         | 浏览器 |
| console.log(msg);      | 浏览器控制台打印输出信息. 用来给程序员看自己运行时的消息 | 浏览器 |
| prompt(info);          | 浏览看弹出输入框，用户可以输入               | 浏览器 |
| document.write()文档页面输出 |                               |     |

- alert()警告框  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/cd5487e3cc4c48a8ae252aa4dbe87ac2.png#pic_center)

- prompt() 输入框  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/4723f1b1f1a6485c8501e6ee2e5bb90d.png#pic_center)

- console.log()控制台输出  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/818421338119471c89a76d287655c805.png#pic_center)

- document.write()文档页面输出 : 直接在页面输出

## 2.1 例子

```js
    <script>
        // 1.弹出警示框  输出的 展示给用户的
        alert('秀儿同学,请你坐下！');
        // 2.输入框
        prompt('请输入密码:','1234');
        prompt('请输入你的名字:');
        // 3.控制台输出 控制台可见
        console.log('看到了吗,码农兄弟?');
        //4.文档页面输出
        document.write('666');
    </script>
```

# 3 变量

变量是用于存放数据的容器，我们通过变量名获取数据，甚至数据可以修改
本质：变量是程序在内存中申请的一块用来存放数据的空间

## 3.1 变量初始化🔥

1. var是一个JS关键字，用来声明变量(variable变量的意思)。使用该关键字声明变量后，计算机会自动为变量分配内存空间。
2. age 是程序员定义的变量名，我们要通过变量名来访问内存中分配的空间

```js
//声明变量同时赋值为18
var age = 18; 
//同时声明多个变量时，只需要写一个 var， 多个变量名之间使用英文逗号隔开。

var age = 18, address ='火影村',salary = 15000;
```

```js
<script>
        // 变量的使用：
        // 1.声明变量  声明了一个age 的变量
        var age; //age 为变量名
        //2.赋值 把值存入这个变量中
        age = 20;
        // 3.在控制台输出结果
        console.log(age); 

        alert(userName);
        // 4.变量的初始化 （常用）
        // 声明一个变量并赋值，称之为变量的初始化
        var onename = '血灵';//尽量不用name作为变量名，因为name在一些浏览器中是有关键字
        console.log(onename);
</script>
```

## 3.2 变量的声明和赋值

同时声明多个变量时，只需要写一个 var， 多个变量名之间使用英文逗号隔开。

```js
var age = 10, name = 'zs', sex = 2;
var oneName = '白夜',
    address = '地球',
              age = 500;
```

声明变量特殊情况

| 情况                         | 说明           | 结果        |
| -------------------------- | ------------ | --------- |
| var age; console.log(age); | 只声明，不赋值      | undefined |
| console.log(age)           | 不声明 不赋值 直接使用 | 报错        |
| age = 10;console.log(age); | 不声明 只赋值      | 10        |

```js
// 1只声明不赋值 输出undefined 因为程序也不知道里面存的是啥  未定义的
var sex;
console.log(sex);
// 2不声明 不赋值 直接使用会报错
// console.log(tel);  //需注释掉，否则下行无法执行，因为js是逐行解释，解释一句，执行一句....
// 3不声明 直接赋值使用
//不提倡如此使用
qq = 123232;
console.log(qq);
```

## 3.3 变量的命名规范

1. 由字母(A-Za-z)、数字(0-9)、下划线(_)、美元符号( $ )组成
   1. 如：usrAge, num01, _name
2. 严格区分大小写
   1. var app; 和 var App; 是两个变量
3. 不能 以数字开头
   1. 18age 是错误的
4. 不能 是关键字、保留字
   1. 例如：var、for、while
5. 变量名必须有意义，做到 见其名，知其意
   1. MMD 、BBD、 nl → age
6. 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。 myFirstName

## 3.4 标识符、关键字、保留字

（1）标识符
标识(zhi)符：就是指开发人员为变量、属性、函数、参数取的名字。
标识符不能是关键字或保留字。

（2）关键字
关键字：是指 JS本身已经使用了的字，不能再用它们充当变量名、方法名。
包括：break、case、catch、continue、default、delete、do、else、finally、for、function、if、in、instanceof、new、return、switch、this、throw、try、typeof、var、void、while、with 等。

（3）保留字
保留字：实际上就是预留的“关键字”，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。
包括：boolean、byte、char、class、const、debugger、double、enum、export、extends、fimal、float、goto、implements、import、int、interface、long、mative、package、private、protected、public、short、static、super、synchronized、throws、transient、volatile 等。

# 4 数据类型

## 4.1 数据类型简介

（1）为何需要数据类型
在计算机中，不同的数据所需占用的存储空间是不同的，为了便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型。

简单来说，数据类型就是数据的类别型号。

比如姓名“张三”，年龄18，这些数据的类型是不一样的。

（2）变量的数据类型
变量是用来存储值的所在处，它们有名字和数据类型。 变量的数据类型决定了如何将代表这些值的位存储到计算机的内存中。
JavaScript 是一种弱类型或者说动态语言。
这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。
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

## 4.2 简单数据类型 / 基本数据类型
|简单数据类型	|说明	|默认值|
|--|---|---|
|Number	|数字型，包含整型值和浮点型值，如21，0.21	|0|
|Boolean	|布尔值类型，如true，false ，等价于1和0	|false|
|Undefined	|var a; 声明了变量a但是没有赋值，此时a=undefined	|undefined（未定义的）|
|string	|字符串类型，如“张三”|“”
|Null	|var a = null;声明了变量a为空值	|null|

### 4.2.1 数字型 Number
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

### 4.2.2 字符串型 String

字符串型可以是引号中的任意文本，其语法为 “双引号” 和 "单引号’’
var strMsg = "我爱北京天安门~";		//使用双引号表示字符串
var strMsg = '我爱北京';			  //使用单引号表示字符串

因为 HTML 标签里面的属性使用的是双引号，JS 这里我们更推荐使用单引号。

(1)字符串引号嵌套
JS可以用 单引号嵌套双引号，或者用 双引号嵌套单引号（外双内单，外单内双）
```js
var strMsg ='我是一个“高富帅”' //可以用 ' ' 包含 " "
var strMsg2 ="我是'高富帅'" //可以用" "  包含  ''
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

### 4.2.3 布尔型Boolean
布尔类型有两个值：true 和 false ，其中 true 表示真（对），而 false 表示假（错）。
布尔型和数字型相加的时候， true 的值为 1 ，false 的值为 0。
```js
var flag = true;
console.log(flag + 1); // 2 true当加法来看当1来看，flase当0来看

```


### 4.2.4 undefined未定义🔥
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

### 4.2.5 空值null
一个声明变量给 null 值，里面存的值为空
```js
var space = null;
console.log(space + 'pink'); //nullpink
console.llog(space + 1); // 1 
```

## 4.3 获取变量数据类型

### 4.3.1 typeof
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

### 4.3.2 字面量
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

## 4.4 数据类型转换
使用表单、prompt 获取过来的数据默认是字符串类型的，此时就不能直接简单的进行加法运算，而需要转换变量的数据类型。通俗来说，就是把一种数据类型的变量转换成另外一种数据类型。

我们通常会实现3种方式的转换：

转换为字符串类型
转换为数字型
转换为布尔型

### 4.4.1 转换为字符串型🔥
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



### 4.4.2 转换为数字型🔥
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

### 4.4.3 转换为布尔型
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


# 5 运算符

运算符（operator）也被称为**操作符**，是用于实现赋值、比较和执行算数运算等功能的符号

JavaScript 中常用的运算符有：

-   算数运算符
-   递增和递减运算符
-   比较运算符
-   逻辑运算符
-   赋值运算符

## 5.1 算术运算符
概念：算术运算使用的符号，用于执行两个变量或值的算术运算。

运算符	描述	实例
+	加	10 + 20 =30
-	减	10 - 20 =-10
*	乘	10 * 20 =200
/	除	10 / 20 =0.5
%	取余数（取模）	返回出发的余数 9 % 2 =1

## 5.2 浮点数的精度问题
浮点数值的最高精度是17位小数，但在进行算数计算时其精确度远远不如整数

var result = 0.1 +0.2; //结果不是0.3，0.30000000000000004
console.log(0.07 * 100); //结果不是7，而是7.000000000000001


所以不要直接判断两个浮点数是否相等

## 5.3 递增和递减运算符
递增（++）

递减（- -）

放在变量前面时，我们称为前置递增(递减)运算符

放在变量后面时，我们称为后置递增(递减)运算符

注意：递增和递减运算符必须和变量配合使用。

①前置递增运算符
++num 为  num = num + 1
使用口诀:先自加，后返回值

var num = 10;
alert (++num + 10); // 21

先自加 10+1=11，返回11，此时num=11

②后置递增运算符
num ++  为 num = num +1
使用口诀:先返回原值，后自加

var num = 10;
alert(10 + num++); // 20


③小结
前置递增和后置递增运算符可以简化代码的编写，让变量的值 + 1 比以前写法更简单
单独使用时，运行结果相同，与其他代码联用时，执行结果会不同
开发时，大多使用后置递增/减，并且代码独占一行


## 5.4 比较(关系)运算符
比较运算符是两个数据进行比较时所使用的运算符，比较运算后，会返回一个布尔值(true / false)作为比较运算的结果。

运算符名称	说明	案例	结果
<	小于号	1 < 2	true
`>` 大于号	1 > 2	false
`>=`	大于等于号(大于或者等于)	2 >= 2	true
<=	小于等于号(小于或者等于)	3 <= 2	false
==	判等号(会转型)	37 == 37	true
!=	不等号	37 != 37	false
=== !==	全等 要求值和数据类型都一致	37 === ‘37’	false

① 小结
符号	作用	用法
=	赋值	把右边给左边
==	判断	判断两边值是否相等(注意此时有隐士转换)
===	全等	判断两边的值和数据类型是否完全相同
console.log(18 == '18');		//true
console.log(18 === '18');		//false


## 5.5 逻辑运算符
逻辑运算符是用来进行布尔值运算的运算符，其返回值也是布尔值

逻辑运算符	说明	案例
&&	“逻辑与”，简称"与" and	true && false
||	“逻辑或”，简称"或" or	true || false
！	“逻辑非”，简称"非" not	！true

逻辑与：两边都是 true才返回 true，否则返回 false
逻辑或：两边都为 false 才返回 false，否则都为true
逻辑非：逻辑非（!）也叫作取反符，用来取一个布尔值相反的值，如 true 的相反值是 false

var isOk = !true;
console.log(isOk);  // false
//逻辑非（!）也叫作取反符，用来取一个布尔值相反的值，如 true 的相反值是 false


### 5.5.1 短路运算(逻辑中断)
短路运算的原理：当有多个表达式（值）时,左边的表达式值可以确定结果时,就不再继续运算右边的表达式的值

①逻辑与🔥
语法：表达式1 && 表达式2
如果第一个表达式的值为真，则返回表达式2
如果第一个表达式的值为假，则返回表达式1

```js
console.log(123 && 456);   //456
console.log(0 && 456);     //0
console.log(123 && 456 && 789);  //789
```


②逻辑或
语法：表达式1 || 表达式2
如果第一个表达式的值为真，则返回表达式1
如果第一个表达式的值为假，则返回表达式2

```js
console.log(123 || 456); //123
console.log(0 || 456);   //456
console.log(123 || 456 || 789);  //123

var num = 0;
console.log(123 || num++);
// 先返回在加，相当于 (123 || 0)
console.log(num);    // 123
```

## 5.6 赋值运算符

概念：用来把数据赋值给变量的运算符。

赋值运算符	说明	案例
=	直接赋值	var usrName = ‘我是值’
+= ，-=	加，减一个数后再赋值	var age = 10； age+=5；//15
*=，/=，%=	成，除，取模后再赋值	var age = 2; age*=5; //10


var age = 10;
age += 5;  // 相当于 age = age + 5;
age -= 5;  // 相当于 age = age - 5;
age *= 10; // 相当于 age = age * 10;

## 5.7 运算符优先级🔥
优先级	运算符	顺序
1	小括号	()
2	一元运算符	++ – ！
3	算数运算符	先 * / 后 + -
4	关系运算符	>, >= , < , <=,
5	相等运算符	，！=，=，！==
6	逻辑运算符	先 && 后 ||（先与后或）
7	赋值运算符	=
8	逗号运算符	，


1.一元运算符里面的逻辑非优先级很高
2.逻辑与 比 逻辑或 优先级高

### 5.7.1 练习题
```js
1 
console.log( 4 >= 6 || '人' != '阿凡达' && !(12 * 2 == 144) && true)	// true

2
var a = 3 > 5 && 2 < 7 && 3 == 4; 
console.log(a); 	//false 

var b = 3 <= 4 || 3 > 1 || 3 != 2; 
console.log(b); 	//true

var c = 2 === "2"; 
console.log(c);  	//false

var d = !c || b && a ;
console.log(d);		//true
```

