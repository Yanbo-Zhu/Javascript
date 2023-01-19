
# 1 总览
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode?retiredLocale=de#invoking_strict_mode

**Der strict-mode bewirkt, daß Entwickler sich an die gängigen Konventionen halten müssen. 
Jegliche Fehler werden in der Konsole dokumentiert und unterstützen so den Entwickler bei der Erstellung eines sauber strukturierten und gutlesbaren Programms. **



JavaScript's strict mode is a way to opt in to a restricted variant of JavaScript, thereby implicitly opting-out of "sloppy mode". Strict mode isn't just a subset: it intentionally has different semantics from normal code. 

JavaScript 除了提供正常模式外，还提供了严格模式
ES5 的严格模式是采用具有限制性 JavaScript 变体的一种方式，即在严格的条件下运行 JS 代码
严格模式在IE10 以上版本的浏览器才会被支持，旧版本浏览器会被忽略

## 1.1 细节

严格模式对正常的JavaScript语义做了一些更改：
- 消除了Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为
- 消除代码运行的一些不安全之处，保证代码运行的安全
- 提高编译器效率，增加运行速度
- 禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class, enum, export, extends, import, super 不能做变量名

Strict mode makes several changes to normal JavaScript semantics:
1.  Eliminates some JavaScript silent errors by changing them to throw errors.
2.  Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
3.  Prohibits some syntax likely to be defined in future versions of ECMAScript.


Folgende Programmieränderungen ergebens sich so durch das ECMAScript 5:
-   Variablen und Objekte müssen deklariert werden
-   Variablen, Objekte oder Funktionen können nicht gelöscht werden
-   Oktalzahlen sind nicht erlaubt
-   Verkürzte Schreibweisen durch with gelten nicht
-   Doppelte Parameternamen erzeugen einen Fehler
-   eval oder arguments können nicht als Variable oder benannte Funktionsargumente genutzt werden
-   reservierte Schlüsselwörte wie implements, interface, let, package, private, protected, public, static und yield mit Hinblick auf ECMAScript 6 ezeugen eine Fehlermeldung
-   Funktionsblöcke müssen deklariert werden

# 2 开启严格模式
严格模式可以应用到整个脚本或个别函数中。
因此在使用时，我们可以将严格模式分为为脚本开启严格模式和为函数开启严格模式两种情况

## 2.1 为整个脚本开启严格模式
为整个脚本文件开启严格模式，需要在所有语句之前放一个特定语句
"use strict" 或'use strict'

```html

<script>
    'user strict';
	console.log("这是严格模式。");
</script>
```


因为"use strict"加了引号，所以老版本的浏览器会把它当作一行普通字符串而忽略。
有的 script 基本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他 script 脚本文件。

```html
// 防止变量污染，可以写成立即执行函数：
<script>
	(function (){
    	'use strict';
    	 var num = 10;
    	 function fn() {}
	})();   
</script>
```


## 2.2 为某个函数开启严格模式
若要给某个函数开启严格模式，需要把"use strict"或'use strict'声明放在函数体所有语句之前
将"use strict" 放在函数体的第一行，则整个函数以 "严格模式"运行。

```html
function f(x) {

 "use strict";
}


<body>
    <!-- 为整个脚本(script标签)开启严格模式 -->
    <script>
        'use strict';
        //   下面的js 代码就会按照严格模式执行代码
    </script>

     <!-- 为某个函数开启严格模式 -->
    <script>
        (function() {
            'use strict';
        })();
    </script>
   

    <script>
        // 此时只是给fn函数开启严格模式
        function fn() {
            'use strict';
            // 下面的代码按照严格模式执行
        }

        function fun() {
            // 里面的还是按照普通模式执行
        }
    </script>
</body>
```


# 3 严格模式中的变化
严格模式对JavaScript的语法和行为，都做了一些改变

## 3.1 变量规定
在正常模式中，如果一个变量没有声明就赋值，默认是全局变量
严格模式禁止这种用法，变量都必须先用var 命令声明，然后再使用
严禁删除已经声明变量，例如，``delete x` 语法是错误的
```html
<body>
    <script>
        'use strict';
        // 1. 我们的变量名必须先声明再使用
        // num = 10;
        // console.log(num);
        var num = 10;
        console.log(num);
        // 2.我们不能随意删除已经声明好的变量
        // delete num;
    </script>
</body>
```


## 3.2 严格模式下this指向问题
1. 以前在全局作用域函数中的this指向window对象
    1. 严格模式下全局作用域中函数中的this 是 undefined
2. 以前构造函数时不加 new 也可以调用，当普通函数，this指向全局对象. 
    1. 严格模式下，如果构造函数不加 new 调用，this指向的是 undefined ，如果给它赋值，会报错
    2. 严格模式下，new 实例化的构造函数指向创建的对象实例
3. 定时器this 还是指向window
4. 事件、对象还是指向调用者

```html
<body>
    <script>
        'use strict';
		//3. 严格模式下全局作用域中函数中的 this 是 undefined。
        function fn() {
            console.log(this); // undefined。

        }
        fn();
    
        //4. 严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给他赋值则 会报错.
        function Star() {
            this.sex = '男';
        }
        // Star();
        var ldh = new Star();
        console.log(ldh.sex);
        
        
        //5. 定时器 this 还是指向 window 
        setTimeout(function() {
            console.log(this);

        }, 2000);
        
    </script>
</body>
```



## 3.3 函数变化
函数不能有重名的参数
函数必须声明在顶层，新版本的JavaScript会引入“块级作用域”（ES6中已引入）。为了与新版本接轨，不允许在非函数的代码块内声明函数

```html
<body>
    <script>
        'use strict';
        // 6. 严格模式下函数里面的参数不允许有重名
        function fn(a, a) {
           console.log(a + a);

        };
        // fn(1, 2);
        function fn() {}
    </script>
</body>
```

