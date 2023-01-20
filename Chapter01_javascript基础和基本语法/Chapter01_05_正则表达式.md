# 1 正则表达式总览
1 正则表达式是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也是对象。

2、作用：  
正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词(替换)，或从字符串中获取我们想要的特定部分(提取)等 。
通常被用来检索、替换那些符合某个模式（规则）的文本。例如：

-   匹配：用户名表单只能输入英文字母、数字或下划线，昵称输入框可以输入中文
-   替换：用于过滤掉页面内容中的一些敏感词
-   提取：从字符串中获取我们想要的特定部分


3 特点
-   灵活性、逻辑性和功能性非常强
-   可以迅速地用极简单的方式达到字符串的复杂控制


# 2 创建正则表达式
在JavaScript中，可以通过两种方式创建正则表达式

1. 通过调用 RegExp 对象的构造函数创建
2. 通过字面量创建

## 2.1 通过调用 RegExp 对象的构造函数创建
通过调用 RegExp 对象的构造函数创建
var 变量名 = new RegExp(/表达式/);

## 2.2 通过字面量创建
通过字面量创建
var 变量名 = /表达式/;

注释中间放表达式就是正则字面量

## 2.3 测试正则表达式 test
test()正则对象方法，用于检测字符串是否符合该规则，该对象会返回true或false,其参数是测试字符串
regexObj.test(str)

1. regexObj 写的是正则表达式
2. str 我们要测试的文本
3. 就是检测str文本是否符合我们写的正则表达式规范

示例
```html
<body>
    <script>
        // 正则表达式在js中的使用

        // 1. 利用 RegExp对象来创建 正则表达式
        var regexp = new RegExp(/123/);
        console.log(regexp);

        // 2. 利用字面量创建 正则表达式
        var rg = /123/;
        // 3.test 方法用来检测字符串是否符合正则表达式要求的规范
        console.log(rg.test(123));
        console.log(rg.test('abc'));
    </script>
</body>
```


# 3 正则表达式中的特殊的字符

一个正则表达式可以由简单的字符构成，比如/abc/，也可以时简单和特殊字符的组合，比如/ab*/。其中特殊字符也被称为**元字符**，在正则表达式中具有特殊意义的专有符号，如^、\、$等

|字符	|含义|
|---|---|
|^|	边界符，匹配输入的开始。例如，/^A/ 并不会匹配 “an A” 中的 ‘A’，但是会匹配 “An E” 中的 ‘A’。|
|$	|边界符，匹配输入的结束。例如，/t$/ 并不会匹配 “eater” 中的 ‘t’，但是会匹配 “eat” 中的 ‘t’。 如果^和$一起使用就是精确匹配，例如 /^abc$/|
|[abc]	|字符类，表示一系列字符（这里abc三个字符）可供选择，只要匹配其中一个就可以了。可以使用破折号（-）来指定一个字符范围。<br> 例如，[abcd] 和[a-d]是一样的。他们都匹配"brisket"中的‘b’,也都匹配“city”中的‘c’。|
|[^xyz]|	一个反向字符集。也就是说， 它匹配任何没有包含在方括号中的字符。你可以使用破折号（-）来指定一个字符范围。任何普通字符在这里都是起作用的。例如，[^abc] 和 [^a-c] 是一样的。他们匹配"brisket"中的‘r’，也匹配“chop”中的‘h’。|
|*|	量词符， 匹配前一个表达式 0 次或多次。等价于 {0,}。例如，/bo*/ 会匹配 “A ghost boooooed” 中的 ‘booooo’ 和 “A bird warbled” 中的 ‘b’，但是在 “A goat grunted” 中不会匹配任内容。|
|+|	量词符， 匹配前面一个表达式 1 次或者多次。等价于 {1,}。例如，/a+/ 会匹配 “candy” 中的 ‘a’ 和 “caaaaaaandy” 中所有的 ‘a’，但是在 “cndy” 中不会匹配任何内容。|
|?	|量词符， 匹配前面一个表达式 0 次或者 1 次。等价于 {0,1}。例如，/e?le?/ 匹配 “angel” 中的 ‘el’、“angle” 中的 ‘le’ 以及 "oslo’ 中的 ‘l’。<br> 如果紧跟在任何量词 *、 +、? 或 {} 的后面，将会使量词变为非贪婪（匹配尽量少的字符），和缺省使用的贪婪模式（匹配尽可能多的字符）正好相反。例如，对 “123abc” 使用 /\d+/ 将会匹配 “123”，而使用 /\d+?/ 则只会匹配到 “1”。|
|{n}	|量词符， n 是一个正整数，匹配了前面一个字符刚好出现了 n 次。比如， /a{2}/ 不会匹配“candy”中的’a’,但是会匹配“caandy”中所有的 a，以及“caaandy”中的前两个’a’。|
|{n,}	|量词符，n是一个正整数，匹配前一个字符至少出现了n次。例如, /a{2,}/ 匹配 “aa”, “aaaa” 和 “aaaaa” 但是不匹配 “a”。|
|{n,m}	|量词符，n 和 m 都是整数。匹配前面的字符至少n次，最多m次。如果 n 或者 m 的值是0， 这个值被忽略。例如，/a{1, 3}/ 并不匹配“cndy”中的任意字符，匹配“candy”中的a，匹配“caandy”中的前两个a，也匹配“caaaaaaandy”中的前三个a。注意，当匹配”caaaaaaandy“时，匹配的值是“aaa”，即使原始的字符串中有更多的a。|
|\d	|预定义类，匹配一个数字。等价于[0-9]。例如， /\d/ 或者 /[0-9]/ 匹配"B2 is the suite number."中的’2’。|
|\D	|预定义类，匹配一个非数字字符。等价于[^0-9]。例如， /\D/ 或者 /[^0-9]/ 匹配"B2 is the suite number."中的’B’ 。|
|\w	|预定义类，匹配一个单字字符（字母、数字或者下划线）。等价于 [A-Za-z0-9_]。例如, /\w/ 匹配 “apple,” 中的 ‘a’，"$5.28,"中的 ‘5’ 和 “3D.” 中的 ‘3’。|
|\W	|预定义类，匹配一个非单字字符。等价于 [^A-Za-z0-9_]。例如, /\W/ 或者 /[^A-Za-z0-9_]/ 匹配 “50%.” 中的 ‘%’。|
|\s	|预定义类，匹配一个空白字符，包括空格、制表符、换页符和换行符。等价于[ \f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]。例如, /\s\w*/ 匹配"foo bar."中的’ bar’。|
|\S	|预定义类，匹配一个非空白字符。等价于 [^ \f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]。例如，/\S\w*/ 匹配"foo bar."中的’foo’。|


## 3.1 边界符
正则表达式中的边界符(位置符)用来提示字符所处的位置，主要有两个字符

边界符	说明
^	表示匹配行首的文本(以谁开始)
$	表示匹配行尾的文本(以谁结束)
如果^ 和 $ 在一起，表示必须是精确匹配

```js
// 边界符 ^ $
var rg = /abc/;   //正则表达式里面不需要加引号，不管是数字型还是字符串型
// /abc/只要包含有abc这个字符串返回的都是true
console.log(rg.test('abc'));
console.log(rg.test('abcd'));
console.log(rg.test('aabcd'));

var reg = /^abc/;
console.log(reg.test('abc'));   //true
console.log(reg.test('abcd'));	// true
console.log(reg.test('aabcd')); // false

var reg1 = /^abc$/
// 以abc开头，以abc结尾，必须是abc
```


## 3.2 字符类
字符类表示有一系列字符可供选择，只要匹配其中一个就可以了
所有可供选择的字符都放在方括号内
①[] 方括号
/[abc]/.test('andy');     // true
1
后面的字符串只要包含 abc 中任意一个字符,都返回true

②[-]方括号内部 范围符
/^[a-z]$/.test()
1
方括号内部加上 - 表示范围，这里表示 a - z 26个英文字母都可以

③[^] 方括号内部 取反符 ^
/[^abc]/.test('andy')   // false
1
方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false

注意和边界符 ^ 区别，边界符写到方括号外面

④字符组合
/[a-z1-9]/.test('andy')    // true
1
方括号内部可以使用字符组合，这里表示包含 a 到 z的26个英文字母和1到9的数字都可以

```html
<body>
    <script>
        //var rg = /abc/;  只要包含abc就可以 
        // 字符类: [] 表示有一系列字符可供选择，只要匹配其中一个就可以了
        var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
        console.log(rg.test('andy'));
        console.log(rg.test('baby'));
        console.log(rg.test('color'));
        console.log(rg.test('red'));
        var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
        console.log(rg1.test('aa'));
        console.log(rg1.test('a'));
        console.log(rg1.test('b'));
        console.log(rg1.test('c'));
        console.log(rg1.test('abc'));
        console.log('------------------');

        var reg = /^[a-z]$/; // 26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
        console.log(reg.test('a'));
        console.log(reg.test('z'));
        console.log(reg.test(1));
        console.log(reg.test('A'));
        // 字符组合
        var reg1 = /^[a-zA-Z0-9_-]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
        console.log(reg1.test('a'));
        console.log(reg1.test('B'));
        console.log(reg1.test(8));
        console.log(reg1.test('-'));
        console.log(reg1.test('_'));
        console.log(reg1.test('!'));
        console.log('----------------');
        // 如果中括号里面有^ 表示取反的意思 千万和 我们边界符 ^ 别混淆
        var reg2 = /^[^a-zA-Z0-9_-]$/;
        console.log(reg2.test('a'));
        console.log(reg2.test('B'));
        console.log(reg2.test(8));
        console.log(reg2.test('-'));
        console.log(reg2.test('_'));
        console.log(reg2.test('!'));
    </script>
</body>
```


## 3.3 量词符
量词符用来设定某个模式出现的次数

量词	说明
*	重复零次或更多次
+	重复一次或更多次
?	重复零次或一次
{n}	重复n次
{n,}	重复n次或更多次
{n,m}	重复n到m次

```html
<body>
    <script>
        // 量词符: 用来设定某个模式出现的次数
        // 简单理解: 就是让下面的a这个字符重复多少次
        // var reg = /^a$/;


        //  * 相当于 >= 0 可以出现0次或者很多次 
        // var reg = /^a*$/;
        // console.log(reg.test(''));
        // console.log(reg.test('a'));
        // console.log(reg.test('aaaa'));



        //  + 相当于 >= 1 可以出现1次或者很多次
        // var reg = /^a+$/;
        // console.log(reg.test('')); // false
        // console.log(reg.test('a')); // true
        // console.log(reg.test('aaaa')); // true

        //  ?  相当于 1 || 0
        // var reg = /^a?$/;
        // console.log(reg.test('')); // true
        // console.log(reg.test('a')); // true
        // console.log(reg.test('aaaa')); // false

        //  {3 } 就是重复3次
        // var reg = /^a{3}$/;
        // console.log(reg.test('')); // false
        // console.log(reg.test('a')); // false
        // console.log(reg.test('aaaa')); // false
        // console.log(reg.test('aaa')); // true
        //  {3, }  大于等于3
        var reg = /^a{3,}$/;
        console.log(reg.test('')); // false
        console.log(reg.test('a')); // false
        console.log(reg.test('aaaa')); // true
        console.log(reg.test('aaa')); // true
        //  {3,16}  大于等于3 并且 小于等于16
        var reg = /^a{3,6}$/;
        console.log(reg.test('')); // false
        console.log(reg.test('a')); // false
        console.log(reg.test('aaaa')); // true
        console.log(reg.test('aaa')); // true
        console.log(reg.test('aaaaaaa')); // false
    </script>
</body>
```


## 3.4 例子: 用户名验证
功能需求：
1. 如果用户名输入合法, 则后面提示信息为 : 用户名合法,并且颜色为绿色
2. 如果用户名输入不合法, 则后面提示信息为: 用户名不符合规范, 并且颜色为绿色

分析：
1. 用户名只能为英文字母,数字,下划线或者短横线组成, 并且用户名长度为 6~16位.
2. 首先准备好这种正则表达式模式 /$[a-zA-Z0-9-_]{6,16}^/
3. 当表单失去焦点就开始验证.
4. 如果符合正则规范, 则让后面的span标签添加 right 类.
5. 如果不符合正则规范, 则让后面的span标签添加 wrong 类.

```html
<body>
    <input type="text" class="uname"> <span>请输入用户名</span>
    <script>
        //  量词是设定某个模式出现的次数
        var reg = /^[a-zA-Z0-9_-]{6,16}$/; // 这个模式用户只能输入英文字母 数字 下划线 短横线但是有边界符和[] 这就限定了只能多选1
        // {6,16}  中间不要有空格
        // console.log(reg.test('a'));
        // console.log(reg.test('8'));
        // console.log(reg.test('18'));
        // console.log(reg.test('aa'));
        // console.log('-------------');
        // console.log(reg.test('andy-red'));
        // console.log(reg.test('andy_red'));
        // console.log(reg.test('andy007'));
        // console.log(reg.test('andy!007'));
        var uname = document.querySelector('.uname');
        var span = document.querySelector('span');
        uname.onblur = function() {
            if (reg.test(this.value)) {
                console.log('正确的');
                span.className = 'right';
                span.innerHTML = '用户名格式输入正确';
            } else {
                console.log('错误的');
                span.className = 'wrong';
                span.innerHTML = '用户名格式输入不正确';
            }
        }
    </script>
</body>

```

# 4 括号总结
大括号 量词符 里面面表示重复次数
中括号 字符集合 匹配方括号中的任意字符
小括号 表示优先级

```js
// 中括号 字符集合 匹配方括号中的任意字符
var reg = /^[abc]$/;
// a || b || c

// 大括号 量词符 里面表示重复次数
var reg = /^abc{3}$/;   // 它只是让c 重复3次 abccc

// 小括号 表示优先级
var reg = /^(abc){3}$/;  //它是让 abc 重复3次
```


在线测试正则表达式：https://c.runoob.com/

# 5 预定义类
预定义类指的是 某些常见模式的简写写法

预定类	说明
\d	匹配0-9之间的任一数字，相当于[0-9]
\D	匹配所有0-9以外的字符，相当于[ ^ 0-9]
\w	匹配任意的字母、数字和下划线,相当于[A-Za-z0-9_ ]
\W	除所有字母、数字、和下划线以外的字符，相当于[ ^A-Za-z0-9_ ]
\s	匹配空格（包括换行符，制表符，空格符等），相当于[\t\t\n\v\f]
\S	匹配非空格的字符，相当于[ ^ \t\r\n\v\f]


## 5.1 例子: 表单验证
分析：

1.手机号码: /^1[3|4|5|7|8][0-9]{9}$/
2.QQ: [1-9][0-9]{4,} (腾讯QQ号从10000开始)
3.昵称是中文: ^[\u4e00-\u9fa5]{2,8}$

```html
<body>
    <script>
        // 座机号码验证:  全国座机号码  两种格式:   010-12345678  或者  0530-1234567
        // 正则里面的或者 符号  |  
        // var reg = /^\d{3}-\d{8}|\d{4}-\d{7}$/;
        var reg = /^\d{3,4}-\d{7,8}$/;
    </script>
</body>
```


# 6 正则表达式中的替换
## 6.1 replace 替换
replace()方法可以实现替换字符串操作，用来替换的参数可以是一个字符串或是一个正则表达式
    stringObject.replace(regexp/substr,replacement)

第一个参数: 被替换的字符串或者正则表达式
第二个参数：替换为的字符串
返回值是一个替换完毕的新字符串

```js
// 替换 replace
var str = 'andy和red';
var newStr = str.replace('andy','baby');
var newStr = str.replace(/andy/,'baby');
```


## 6.2 正则表达式参数
/表达式/[switch]

switch按照什么样的模式来匹配，有三种
- g: 全局匹配
- i:忽略大小写
- gi: 全局匹配 + 忽略大小写
