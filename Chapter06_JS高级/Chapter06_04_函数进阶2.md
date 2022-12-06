![在这里插入图片描述](https://img-blog.csdnimg.cn/217fe88037bf47a394f147a8de0971f0.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70)

# 1 严格模式
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode?retiredLocale=de#invoking_strict_mode

JavaScript's strict mode is a way to opt in to a restricted variant of JavaScript, thereby implicitly opting-out of "sloppy mode". Strict mode isn't just a subset: it intentionally has different semantics from normal code. 

JavaScript 除了提供正常模式外，还提供了严格模式
ES5 的严格模式是采用具有限制性 JavaScript 变体的一种方式，即在严格的条件下运行 JS 代码
严格模式在IE10 以上版本的浏览器才会被支持，旧版本浏览器会被忽略

严格模式对正常的JavaScript语义做了一些更改：
- 消除了Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为
- 消除代码运行的一些不安全之处，保证代码运行的安全
- 提高编译器效率，增加运行速度
- 禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class, enum, export, extends, import, super 不能做变量名

Strict mode makes several changes to normal JavaScript semantics:
1.  Eliminates some JavaScript silent errors by changing them to throw errors.
2.  Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
3.  Prohibits some syntax likely to be defined in future versions of ECMAScript.

## 1.1 开启严格模式
严格模式可以应用到整个脚本或个别函数中。
因此在使用时，我们可以将严格模式分为为脚本开启严格模式和为函数开启严格模式两种情况

### 1.1.1 为整个脚本开启严格模式
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


### 1.1.2 为某个函数开启严格模式
若要给某个函数开启严格模式，需要把"use strict"或'use strict'声明放在函数体所有语句之前
将"use strict" 放在函数体的第一行，则整个函数以 "严格模式"运行。

```html
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


## 1.2 严格模式中的变化
严格模式对JavaScript的语法和行为，都做了一些改变

### 1.2.1 变量规定
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


### 1.2.2 严格模式下this指向问题
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



### 1.2.3 函数变化
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


# 2 高阶函数
高阶函数是对其他函数进行操作的函数，
1. 它接收函数作为参数或
2. 将函数作为返回值输出


## 2.1 接收函数作为参数

```html
<body>
    <div></div>
    <script>
        // 高阶函数- 函数可以作为参数传递
        function fn(a, b, callback) {
            console.log(a + b);
            callback && callback();
        }
        
        fn(1, 2, function() { 
                            console.log('我是最后调用的');
                            }
        );

    </script>
</body>
```


## 2.2 将函数作为返回值
```html
<script>
    function fn(){
        return function() {}
    }
</script>
```


此时 fn 就是一个高阶函数
函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数
同理函数也可以作为返回值传递回来


# 3 闭包
## 3.1 变量作用域
变量根据作用域的不同分为两种：全局变量和局部变量

函数内部可以使用全局变量
函数外部不可以使用局部变量
当函数执行完毕，本作用域内的局部变量会销毁。

## 3.2 什么是闭包
闭包指有权访问另一个函数作用域中的变量的函数
简单理解：一个作用域可以访问另外一个函数内部的局部变量

```html
<body>
    <script>
        // 闭包（closure）指有权访问另一个函数作用域中变量的函数。
        // 闭包: 我们fn2 这个函数作用域 访问了另外一个函数 fn1 里面的局部变量 num
        function fn1() {		// fn1就是闭包函数
            var num = 10;
            function fn2() {
                console.log(num); 	//10
            }
            fn2();
        }
        fn1();
    </script>
</body>

```


## 3.3 在chrome中调试闭包
打开浏览器，按 F12 键启动 chrome 调试工具。

设置断点。
找到 Scope 选项（Scope 作用域的意思）。
当我们重新刷新页面，会进入断点调试，Scope 里面会有两个参数（global 全局作用域、local 局部作用域）。
当执行到 fn2() 时，Scope 里面会多一个 Closure 参数 ，这就表明产生了闭包。

![在这里插入图片描述](https://img-blog.csdnimg.cn/487a2da725794758b4e1e2cf54c1aa18.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

## 3.4 闭包的作用
延伸变量的作用范围
```html
<body>
    <script>
        // 闭包（closure）指有权访问另一个函数作用域中变量的函数。
        // 一个作用域可以访问另外一个函数的局部变量 
        // 我们fn 外面的作用域可以访问fn 内部的局部变量
        // 闭包的主要作用: 延伸了变量的作用范围
        function fn() {
            var num = 10;
            return function() {
                console.log(num);
            }
        }
        var f = fn();
        f();
    </script>
</body>
```


## 3.5 闭包练习
### 3.5.1 点击li输出索引号
```html
<body>
    <ul class="nav">
        <li>榴莲</li>
        <li>臭豆腐</li>
        <li>鲱鱼罐头</li>
        <li>大猪蹄子</li>
    </ul>
    <script>
        // 闭包应用-点击li输出当前li的索引号
        // 1. 我们可以利用动态添加属性的方式
        var lis = document.querySelector('.nav').querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            lis[i].index = i;
            lis[i].onclick = function() {
                // console.log(i);
                console.log(this.index);

            }
        }
        // 2. 利用闭包的方式得到当前小li 的索引号
        for (var i = 0; i < lis.length; i++) {
            // 利用for循环创建了4个立即执行函数
            // 立即执行函数也成为小闭包因为立即执行函数里面的任何一个函数都可以使用它的i这变量
            (function(i) {
                // console.log(i);
                lis[i].onclick = function() {
                    console.log(i);

                }
            })(i);
        }
    </script>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/1d0b66c23bae4baabc2f014fc939c812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

### 3.5.2 定时器中的闭包
```html
<body>
    <ul class="nav">
        <li>榴莲</li>
        <li>臭豆腐</li>
        <li>鲱鱼罐头</li>
        <li>大猪蹄子</li>
    </ul>
    <script>
        // 闭包应用-3秒钟之后,打印所有li元素的内容
        var lis = document.querySelector('.nav').querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            (function(i) {
                setTimeout(function() {
                    console.log(lis[i].innerHTML);
                }, 3000)
            })(i);
        }
    </script>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/bf8930961044466f966d04b802286cf5.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)


# 4 递归 

如果一个函数在内部可以调用其本身，那么这个函数就是递归函数
简单理解： 函数内部自己调用自己，这个函数就是递归函数
由于递归很容易发生"栈溢出"错误，所以必须要加退出条件 return
```html

<body>
    <script>
        // 递归函数 : 函数内部自己调用自己, 这个函数就是递归函数
        var num = 1;

        function fn() {
            console.log('我要打印6句话');

            if (num == 6) {
                return; // 递归里面必须加退出条件
            }
            num++;
            fn();
        }
        fn();
    </script>
</body>
```



## 4.1 浅拷贝和深拷贝
1. 浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用
2. 深拷贝拷贝多层，每一级别的数据都会拷贝
3. Object.assign(target,....sources) ES6新增方法可以浅拷贝

### 4.1.1 浅拷贝

```js
// 浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用
var obj = {
    id: 1,
    name: 'andy',
    msg: {
        age: 18
    }
};
var o = {}
for(var k in obj){
    // k是属性名，obj[k]是属性值
    o[k] = obj.[k];
}
console.log(o);
// 浅拷贝语法糖
Object.assign(o,obj);
```


### 4.1.2 深拷贝
// 深拷贝拷贝多层，每一级别的数据都会拷贝

```js
var obj = {
    id: 1,
    name: 'andy',
    msg: {
        age: 18
    }
    color: ['pink','red']
};
var o = {};

// 封装函数
function deepCopy(newobj,oldobj){
    for(var k in oldobj){
        // 判断属性值属于简单数据类型还是复杂数据类型
        // 1.获取属性值   oldobj[k]
        var item = obldobj[k];
        // 2.判断这个值是否是数组
        if(item instanceof Array){
            newobj[k] = [];
            deepCopy(newobj[k],item)
        }else if (item instanceof Object){
              // 3.判断这个值是否是对象
            newobj[k] = {};
            deepCopy(newobj[k],item)
        }else {
            // 4.属于简单数据类型
            newobj[k] = item;
            
        } 
    }
}
deepCopy(o,obj);
```


