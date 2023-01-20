
# 1 函数内this的指向
this指向，是当我们调用函数的时候确定的，调用方式的不同决定了this的指向不同，一般我们指向我们的调用者

|调用方式|	this指向|
|---|---|
|普通函数调用	|window|
|构造函数调用	|实例对象，原型对象里面的方法也指向实例对象|
|对象方法调用	|该方法所属对象|
|事件绑定方法	|绑定事件对象|
|定时器函数	|window|
|立即执行函数	|window|


```html
<body>
    <button>点击</button>
    <script>
        // 函数的不同调用方式决定了this 的指向不同
        // 1. 普通函数 this 指向window
        function fn() {
            console.log('普通函数的this' + this);
        }
        window.fn();
        // 2. 对象的方法 this指向的是对象 o
        var o = {
            sayHi: function() {
                console.log('对象方法的this:' + this);
            }
        }
        o.sayHi();
        // 3. 构造函数 this 指向 ldh 这个实例对象 原型对象里面的this 指向的也是 ldh这个实例对象
        function Star() {};
        Star.prototype.sing = function() {

        }
        var ldh = new Star();
        // 4. 绑定事件函数 this 指向的是函数的调用者 btn这个按钮对象
        var btn = document.querySelector('button');
        btn.onclick = function() {
            console.log('绑定时间函数的this:' + this);
        };
        // 5. 定时器函数 this 指向的也是window
        window.setTimeout(function() {
            console.log('定时器的this:' + this);

        }, 1000);
        // 6. 立即执行函数 this还是指向window
        (function() {
            console.log('立即执行函数的this' + this);
        })();
    </script>
</body>
```


# 2 改变函数内部this指向
JavaScript 为我们专门提供了一些函数方法来帮我们处理函数内部 this 的指向问题，常用的有 bind(), call(), apply()三种方法

## 2.1 call() 方法
- call()方法调用一个对象，简单理解为调用函数的方式，但是它可以改变函数的this指向
- fun.call(thisArg,arg1,arg2,.....)
    - thisArg: 在 fun 函数运行时指定的 this 值
    - arg1,arg2: 传递的其他参数
- 返回值就是函数的返回值，因为它就是调用函数
- 因此当我们想改变 this 指向，同时想调用这个函数的时候，可以使用 call，比如继承


```js
function showThis(par){
    console.log(`The ${this.type} is ${par}`);
}

let objOne = {
    type : 42,
    showThis
};

let objTwo = {
    type : "blablabla",
    showThis
};

console.log(objOne); // 显示为 {type: 42, showThis: f }
console.log(objTwo); // 显示为 {type: 'blablabla', showThis: f }

objOne.showThis("my property");  // The 42 is my property
objTwo.showThis("MY property!!");  // The blablabla is MY property!!

// passing "this" mit call()
showThis.call(objOne, "called with call()!");  // The 42 is called with call()!

```

```html
<body>
    <script>
        // 改变函数内this指向  js提供了三种方法  call()  apply()  bind()

        // 1. call()
        var o = {
            name: 'andy'
        }

        function fn(a, b) {
            console.log(this);
            console.log(a + b);

        };
        fn.call(o, 1, 2);
        // call 第一个可以调用函数 第二个可以改变函数内的this 指向
        // call 的主要作用可以实现继承
        function Father(uname, age, sex) {
            this.uname = uname;
            this.age = age;
            this.sex = sex;
        }

        function Son(uname, age, sex) {
            Father.call(this, uname, age, sex);
        }
        var son = new Son('刘德华', 18, '男');
        console.log(son);
    </script>
</body>
```


## 2.2 apply()方法
- apply()方法调用一个函数，简单理解为调用函数的方式，但是它可以改变函数的 this指向
- fun.apply(thisArg,[argsArray])
    - thisArg: 在 fun 函数运行时指定的 this 值
    - argsArray : 传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数
- 因此 apply 主要跟数组有关系，比如使用 Math.max() 求数组的最大值

```html
<body>
    <script>
        // 改变函数内this指向  js提供了三种方法  call()  apply()  bind()

        // 2. apply()  应用 运用的意思
        var o = {
            name: 'andy'
        };

        function fn(arr) {
            console.log(this);
            console.log(arr); // 'pink'

        };
        fn.apply(o, ['pink']);
        // 1. 也是调用函数 第二个可以改变函数内部的this指向
        // 2. 但是他的参数必须是数组(伪数组)
        // 3. apply 的主要应用 比如说我们可以利用 apply 借助于数学内置对象求数组最大值 
        // Math.max();
        var arr = [1, 66, 3, 99, 4];
        var arr1 = ['red', 'pink'];
        // var max = Math.max.apply(null, arr);
        var max = Math.max.apply(Math, arr);
        var min = Math.min.apply(Math, arr);
        console.log(max, min);
    </script>
</body>

```


## 2.3 bind()方法
bind()方法不会调用函数。但是能改变函数内部 this指向
fun.bind(thisArg,arg1,arg2,....)
返回由指定的 this值和初始化参数改造的 原函数拷贝
因此当我们只是想改变 this 指向，并且不想调用这个函数的时候，可以使用bind

```html
<body>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <script>
        // 改变函数内this指向  js提供了三种方法  call()  apply()  bind()

        // 3. bind()  绑定 捆绑的意思
        var o = {
            name: 'andy'
        };

        function fn(a, b) {
            console.log(this);
            console.log(a + b);


        };
        var f = fn.bind(o, 1, 2);
        f();
        // 1. 不会调用原来的函数   可以改变原来函数内部的this 指向
        // 2. 返回的是原函数改变this之后产生的新函数
        // 3. 如果有的函数我们不需要立即调用,但是又想改变这个函数内部的this指向此时用bind
        // 4. 我们有一个按钮,当我们点击了之后,就禁用这个按钮,3秒钟之后开启这个按钮
        // var btn1 = document.querySelector('button');
        // btn1.onclick = function() {
        //     this.disabled = true; // 这个this 指向的是 btn 这个按钮
        //     // var that = this;
        //     setTimeout(function() {
        //         // that.disabled = false; // 定时器函数里面的this 指向的是window
        //         this.disabled = false; // 此时定时器函数里面的this 指向的是btn
        //     }.bind(this), 3000); // 这个this 指向的是btn 这个对象
        // }
        var btns = document.querySelectorAll('button');
        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function() {
                this.disabled = true;
                setTimeout(function() {
                    this.disabled = false;
                }.bind(this), 2000);
            }
        }
    </script>
</body>

```


## 2.4 总结
call apply bind 总结：

相同点：
都可以改变函数内部的 this指向

区别点：
call和apply会调用函数，并且改变函数内部的this指向
call和apply传递的参数不一样，call 传递参数，apply 必须数组形式
bind不会调用函数，可以改变函数内部this指向


主要应用场景: 
call经常做继承
apply经常跟数组有关系，比如借助于数学对线实现数组最大值与最小值
bind不调用函数，但是还想改变this指向，比如改变定时器内部的this指向
