https://blog.csdn.net/Augenstern_QXL/article/details/119249534


# 1 运算符

运算符（operator）也被称为**操作符**，是用于实现赋值、比较和执行算数运算等功能的符号

JavaScript 中常用的运算符有：

-   算数运算符
-   递增和递减运算符
-   比较运算符
-   逻辑运算符
-   赋值运算符

## 1.1 算术运算符
概念：算术运算使用的符号，用于执行两个变量或值的算术运算。

运算符	描述	实例
+	加	10 + 20 =30
-	减	10 - 20 =-10
*	乘	10 * 20 =200
/	除	10 / 20 =0.5
%	取余数（取模）	返回出发的余数 9 % 2 =1

## 1.2 浮点数的精度问题
浮点数值的最高精度是17位小数，但在进行算数计算时其精确度远远不如整数

var result = 0.1 +0.2; //结果不是0.3，0.30000000000000004
console.log(0.07 * 100); //结果不是7，而是7.000000000000001


所以不要直接判断两个浮点数是否相等

## 1.3 递增和递减运算符
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


## 1.4 比较(关系)运算符
比较运算符是两个数据进行比较时所使用的运算符，比较运算后，会返回一个布尔值(true / false)作为比较运算的结果。

运算符名称	说明	案例	结果
<	小于号	1 < 2	true
`>` 大于号	1 > 2	false
`>=`	大于等于号(大于或者等于)	2 >= 2	true
<=	小于等于号(小于或者等于)	3 <= 2	false
==	判等号(会转型)	37 == 37	得到 true.   1 == true  , 结果为 true. 0 == true  , 结果为 false.   <mark> 2 == true  , 结果为 false. </mark>
!=	不等号	37 != 37	false
=== !==	全等 要求值和数据类型都一致	37 === ‘37’	false

① 小结
符号	作用	用法
=	赋值	把右边给左边
==	判断	判断两边值是否相等(注意此时有隐士转换)
===	全等	判断两边的值和数据类型是否完全相同
console.log(18 == '18');		//true
console.log(18 === '18');		//false


## 1.5 逻辑运算符
逻辑运算符是用来进行布尔值运算的运算符，其返回值也是布尔值

逻辑运算符	说明	案例
&&	“逻辑与”，简称"与" and	     true && false
||	“逻辑或”，简称"或" or      	true || false
！	“逻辑非”，简称"非" not Negationen    	!true

逻辑与：两边都是 true才返回 true，否则返回 false
逻辑或：两边都为 false 才返回 false，否则都为true
逻辑非：逻辑非（!）也叫作取反符，用来取一个布尔值相反的值，如 true 的相反值是 false

var isOk = !true;
console.log(isOk);  // false
//逻辑非（!）也叫作取反符，用来取一个布尔值相反的值，如 true 的相反值是 false


### 1.5.1 短路运算(逻辑中断)
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

## 1.6 赋值运算符

概念：用来把数据赋值给变量的运算符。

赋值运算符	说明	案例
=	直接赋值	var usrName = ‘我是值’
+= ，-=	加，减一个数后再赋值	var age = 10； age+=5；//15
*=，/=，%=	成，除，取模后再赋值	var age = 2; age*=5; //10


var age = 10;
age += 5;  // 相当于 age = age + 5;
age -= 5;  // 相当于 age = age - 5;
age *= 10; // 相当于 age = age * 10;

## 1.7 运算符优先级🔥
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

### 1.7.1 练习题
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



# 1 运算符的扩展
## 1.1 指数运算符

ES2016 新增了一个指数运算符（`**`）。

```js
2 ** 2 // 4
2 ** 3 // 8
```

这个运算符的一个特点是右结合，而不是常见的左结合。多个指数运算符连用时，是从最右边开始计算的。

```js
// 相当于 2 ** (3 ** 2)
2 ** 3 ** 2
// 512
```

上面代码中，首先计算的是第二个指数运算符，而不是第一个。

指数运算符可以与等号结合，形成一个新的赋值运算符（`**=`）。

```js
let a = 1.5;
a **= 2;
// 等同于 a = a * a;

let b = 4;
b **= 3;
// 等同于 b = b * b * b;
```

## 1.2 链判断运算符

编程实务中，如果读取对象内部的某个属性，往往需要判断一下，属性的上层对象是否存在。比如，读取`message.body.user.firstName`这个属性，安全的写法是写成下面这样。

```js
// 错误的写法
const  firstName = message.body.user.firstName || 'default';

// 正确的写法
const firstName = (message
  && message.body
  && message.body.user
  && message.body.user.firstName) || 'default';
```

上面例子中，`firstName`属性在对象的第四层，所以需要判断四次，每一层是否有值。

三元运算符`?:`也常用于判断对象是否存在。

```js
const fooInput = myForm.querySelector('input[name=foo]')
const fooValue = fooInput ? fooInput.value : undefined
```

上面例子中，必须先判断`fooInput`是否存在，才能读取`fooInput.value`。

这样的层层判断非常麻烦，因此 ES2020 引入了“链判断运算符”（optional chaining operator）`?.`，简化上面的写法。

```js
const firstName = message?.body?.user?.firstName || 'default';
const fooValue = myForm.querySelector('input[name=foo]')?.value
```

上面代码使用了`?.`运算符，直接在链式调用的时候判断，左侧的对象是否为`null`或`undefined`。如果是的，就不再往下运算，而是返回`undefined`。

下面是判断对象方法是否存在，如果存在就立即执行的例子。

```js
iterator.return?.()
```

上面代码中，`iterator.return`如果有定义，就会调用该方法，否则`iterator.return`直接返回`undefined`，不再执行`?.`后面的部分。

对于那些可能没有实现的方法，这个运算符尤其有用。

```js
if (myForm.checkValidity?.() === false) {
  // 表单校验失败
  return;
}
```

上面代码中，老式浏览器的表单对象可能没有`checkValidity()`这个方法，这时`?.`运算符就会返回`undefined`，判断语句就变成了`undefined === false`，所以就会跳过下面的代码。

链判断运算符`?.`有三种写法。

- `obj?.prop` // 对象属性是否存在
- `obj?.[expr]` // 同上
- `func?.(...args)` // 函数或对象方法是否存在

下面是`obj?.[expr]`用法的一个例子。

```js
let hex = "#C0FFEE".match(/#([A-Z]+)/i)?.[1];
```

上面例子中，字符串的`match()`方法，如果没有发现匹配会返回`null`，如果发现匹配会返回一个数组，`?.`运算符起到了判断作用。

下面是`?.`运算符常见形式，以及不使用该运算符时的等价形式。

```js
a?.b
// 等同于
a == null ? undefined : a.b

a?.[x]
// 等同于
a == null ? undefined : a[x]

a?.b()
// 等同于
a == null ? undefined : a.b()

a?.()
// 等同于
a == null ? undefined : a()
```

上面代码中，特别注意后两种形式，如果`a?.b()`和`a?.()`。如果`a?.b()`里面的`a.b`有值，但不是函数，不可调用，那么`a?.b()`是会报错的。`a?.()`也是如此，如果`a`不是`null`或`undefined`，但也不是函数，那么`a?.()`会报错。

使用这个运算符，有几个注意点。

（1）短路机制

本质上，`?.`运算符相当于一种短路机制，只要不满足条件，就不再往下执行。

```js
a?.[++x]
// 等同于
a == null ? undefined : a[++x]
```

上面代码中，如果`a`是`undefined`或`null`，那么`x`不会进行递增运算。也就是说，链判断运算符一旦为真，右侧的表达式就不再求值。

（2）括号的影响

如果属性链有圆括号，链判断运算符对圆括号外部没有影响，只对圆括号内部有影响。

```js
(a?.b).c
// 等价于
(a == null ? undefined : a.b).c
```

上面代码中，`?.`对圆括号外部没有影响，不管`a`对象是否存在，圆括号后面的`.c`总是会执行。

一般来说，使用`?.`运算符的场合，不应该使用圆括号。

（3）报错场合

以下写法是禁止的，会报错。

```js
// 构造函数
new a?.()
new a?.b()

// 链判断运算符的右侧有模板字符串
a?.`{b}`
a?.b`{c}`

// 链判断运算符的左侧是 super
super?.()
super?.foo

// 链运算符用于赋值运算符左侧
a?.b = c
```

## 1.3 Null 判断运算符

读取对象属性的时候，如果某个属性的值是`null`或`undefined`，有时候需要为它们指定默认值。常见做法是通过`||`运算符指定默认值。

```js
const headerText = response.settings.headerText || 'Hello, world!';
const animationDuration = response.settings.animationDuration || 300;
const showSplashScreen = response.settings.showSplashScreen || true;
```

上面的三行代码都通过`||`运算符指定默认值，但是这样写是错的。开发者的原意是，只要属性的值为`null`或`undefined`，默认值就会生效，但是属性的值如果为空字符串或`false`或`0`，默认值也会生效。

为了避免这种情况，ES2020引入了一个新的 Null 判断运算符`??`。它的行为类似`||`，但是只有运算符左侧的值为`null`或`undefined`时，才会返回右侧的值。

```js
const headerText = response.settings.headerText ?? 'Hello, world!';
const animationDuration = response.settings.animationDuration ?? 300;
const showSplashScreen = response.settings.showSplashScreen ?? true;
```

上面代码中，默认值只有在左侧属性值为`null`或`undefined`时，才会生效。

这个运算符的一个目的，就是跟链判断运算符`?.`配合使用，为`null`或`undefined`的值设置默认值。

```js
const animationDuration = response.settings?.animationDuration ?? 300;
```

上面代码中，如果`response.settings`是`null`或`undefined`，或者`response.settings.animationDuration`是`null`或`undefined`，就会返回默认值300。也就是说，这一行代码包括了两级属性的判断。

这个运算符很适合判断函数参数是否赋值。

```js
function Component(props) {
  const enable = props.enabled ?? true;
  // …
}
```

上面代码判断`props`参数的`enabled`属性是否赋值，基本等同于下面的写法。

```js
function Component(props) {
  const {
    enabled: enable = true,
  } = props;
  // …
}
```

`??`本质上是逻辑运算，它与其他两个逻辑运算符`&&`和`||`有一个优先级问题，它们之间的优先级到底孰高孰低。优先级的不同，往往会导致逻辑运算的结果不同。

现在的规则是，如果多个逻辑运算符一起使用，必须用括号表明优先级，否则会报错。

```js
// 报错
lhs && middle ?? rhs
lhs ?? middle && rhs
lhs || middle ?? rhs
lhs ?? middle || rhs
```

上面四个表达式都会报错，必须加入表明优先级的括号。

```js
(lhs && middle) ?? rhs;
lhs && (middle ?? rhs);

(lhs ?? middle) && rhs;
lhs ?? (middle && rhs);

(lhs || middle) ?? rhs;
lhs || (middle ?? rhs);

(lhs ?? middle) || rhs;
lhs ?? (middle || rhs);
```

## 2 逻辑赋值运算符 

ES2021 引入了三个新的逻辑赋值运算符（logical assignment operators），将逻辑运算符与赋值运算符进行结合。

```js
// 或赋值运算符
x ||= y
// 等同于
x || (x = y)

// 与赋值运算符
x &&= y
// 等同于
x && (x = y)

// Null 赋值运算符
x ??= y
// 等同于
x ?? (x = y)
```

这三个运算符`||=`、`&&=`、`??=`相当于先进行逻辑运算，然后根据运算结果，再视情况进行赋值运算。

它们的一个用途是，为变量或属性设置默认值。

```js
// 老的写法
user.id = user.id || 1;

// 新的写法
user.id ||= 1;
```

上面示例中，`user.id`属性如果不存在，则设为`1`，新的写法比老的写法更紧凑一些。

下面是另一个例子。

```js
function example(opts) {
  opts.foo = opts.foo ?? 'bar';
  opts.baz ?? (opts.baz = 'qux');
}
```

上面示例中，参数对象`opts`如果不存在属性`foo`和属性`baz`，则为这两个属性设置默认值。有了“Null 赋值运算符”以后，就可以统一写成下面这样。

```js
function example(opts) {
  opts.foo ??= 'bar';
  opts.baz ??= 'qux';
}
```