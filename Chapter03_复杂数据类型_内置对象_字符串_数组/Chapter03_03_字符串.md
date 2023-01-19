

# 1 字符串对象
## 1.1 基本包装类型
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


## 1.2 字符串的不可变
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



## 1.3 根据字符返回位置
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



### 1.3.1 返回字符位置
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



## 1.4 根据位置返回字符
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


# 2 Umwandlung von Variablentypen 

```JS
let bekanntesGedicht = true ;
bekanntesGedicht = bekanntesGedicht + "" ; //der Wahrheitswert wird zur Zeichenkette

let jahreszahl = " 2000 " ;
jahreszahl = jahreszahl * 1; //die Zeichenkette wird zur Zahl (also 2000)

let veroeffentlichung = jahreszahl + 9; //das Ergebnis ist 2009, nicht 20009
```

# 3 字符串方法


## 3.1 杂

let nachname="Goethe";

|x|x|
|---|--|
|nachname.charAt(x)|liefert das Zeichen an der Stelle x. Achtung: Zählung beginnt bei 0 nicht bei 1|
|nachname.substring(anfang, ende)| liefert einen Teil der Zeichenkette vom Zeichen anfang bis zum Zeichen ende, anfang und Ende sind hierbei numerische Variablen (Zahlen). Die Zählung beginnt wieder bei 0|
|nachname.length|liefert die Zeichenanzahl|
|nachname.replace( "zeichen1" , "zeichen2" ) |ersetzt das im String vorhandene Zeichen 1 mit dem neuen Zeichen 2|


```
let a = nachname.charAt(4); //liefert a = "h"
let b = nachname.substring(2,5); //liefert b = "ethe"
let c = nachname.length; //liefert c = 6
let d = nachname.replace("e", "u"); //liefert d = "Gouthu"
```

## 3.2 拼接

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


## 3.3 replace()方法
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



## 3.4 split()方法
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

## 3.5 大小写转换 toUpperCase(), toLowerCase()
toUpperCase() 转换大写
toLowerCase() 转换小写

# 4 CSS3 的 字符串的方法
## 4.1 trim()
​ str.trim()
trim()方法会从一个字符串的两端删除空白字符
trim()方法并不影响原字符串本身，它返回的是一个新的字符串

```html
<body>
    <input type="text"> <button>点击</button>
    <div></div>
    <script>
        // trim 方法去除字符串两侧空格
        var str = '   an  dy   ';
        console.log(str);
        var str1 = str.trim();
        console.log(str1);
        var input = document.querySelector('input');
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        btn.onclick = function() {
            var str = input.value.trim();
            if (str === '') {
                alert('请输入内容');
            } else {
                console.log(str);
                console.log(str.length);
                div.innerHTML = str;
            }
        }
    </script>
</body>
```



## 4.2 内插 string Interpolation 

使用 ${} 两边必须写上  \`\`, 不能用""
`` 代表 string literal .  man muss nicht mit ""  arbeiten. Es ist ganz hilfreich bei css selectoren

```js

1 
let objFunc = {};
objFunc.show = function(par){
    return console.log(`Parameter: ${par}`, this);
};
objFunc.show(true);

2 
let n = 1;
console.log(n);
console.log(`${n*5} weiter Text`);
```




## 4.3 includes(), startsWith(), endsWith()

传统上，JavaScript 只有`indexOf`方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。

- **includes()**：返回布尔值，表示是否找到了参数字符串。
- **startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。

```js
let s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```

这三个方法都支持第二个参数，表示开始搜索的位置。

```js
let s = 'Hello world!';

s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

上面代码表示，使用第二个参数`n`时，`endsWith`的行为与其他两个方法有所不同。它针对前`n`个字符，而其他两个方法针对从第`n`个位置直到字符串结束。

## 4.4 repeat()

`repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

```js
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```

参数如果是小数，会被取整。

```js
'na'.repeat(2.9) // "nana"
```

如果`repeat`的参数是负数或者`Infinity`，会报错。

```js
'na'.repeat(Infinity)
// RangeError
'na'.repeat(-1)
// RangeError
```

但是，如果参数是 0 到-1 之间的小数，则等同于 0，这是因为会先进行取整运算。0 到-1 之间的小数，取整以后等于`-0`，`repeat`视同为 0。

```js
'na'.repeat(-0.9) // ""
```

参数`NaN`等同于 0。

```js
'na'.repeat(NaN) // ""
```

如果`repeat`的参数是字符串，则会先转换成数字。

```js
'na'.repeat('na') // ""
'na'.repeat('3') // "nanana"
```

## 4.5 padStart()，padEnd()

ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。`padStart()`用于头部补全，`padEnd()`用于尾部补全。

```js
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```

上面代码中，`padStart()`和`padEnd()`一共接受两个参数，第一个参数是字符串补全生效的最大长度，第二个参数是用来补全的字符串。

如果原字符串的长度，等于或大于最大长度，则字符串补全不生效，返回原字符串。

```js
'xxx'.padStart(2, 'ab') // 'xxx'
'xxx'.padEnd(2, 'ab') // 'xxx'
```

如果用来补全的字符串与原字符串，两者的长度之和超过了最大长度，则会截去超出位数的补全字符串。

```js
'abc'.padStart(10, '0123456789')
// '0123456abc'
```

如果省略第二个参数，默认使用空格补全长度。

```js
'x'.padStart(4) // '   x'
'x'.padEnd(4) // 'x   '
```

`padStart()`的常见用途是为数值补全指定位数。下面代码生成 10 位的数值字符串。

```js
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"
```

另一个用途是提示字符串格式。

```js
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

## 4.6 trimStart()，trimEnd()

`trimStart()`和`trimEnd()`这两个方法，它们的行为与`trim()`一致，`trimStart()`消除字符串头部的空格，`trimEnd()`消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

```js
const s = '  abc  ';

s.trim() // "abc"
s.trimStart() // "abc  "
s.trimEnd() // "  abc"
```

上面代码中，`trimStart()`只消除头部的空格，保留尾部的空格。`trimEnd()`也是类似行为。

除了空格键，这两个方法对字符串头部（或尾部）的 tab 键、换行符等不可见的空白符号也有效。

浏览器还部署了额外的两个方法，`trimLeft()`是`trimStart()`的别名，`trimRight()`是`trimEnd()`的别名。

## 4.7 at()

`at()`方法接受一个整数作为参数，返回参数指定位置的字符，支持负索引（即倒数的位置）。

```js
const str = 'hello';
str.at(1) // "e"
str.at(-1) // "o"
```

如果参数位置超出了字符串范围，`at()`返回`undefined`。
