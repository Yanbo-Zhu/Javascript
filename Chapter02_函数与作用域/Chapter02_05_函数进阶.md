![在这里插入图片描述](https://img-blog.csdnimg.cn/217fe88037bf47a394f147a8de0971f0.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70)



# 1 高阶函数 (对其他函数进行操作的函数，)
高阶函数是对其他函数进行操作的函数，
1. 它接收函数作为参数或
2. 将函数作为返回值输出


## 1.1 接收函数作为参数

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


## 1.2 将函数作为返回值
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


# 2 闭包(访问另一个函数作用域中的变量的函数)
## 2.1 变量作用域
变量根据作用域的不同分为两种：全局变量和局部变量

函数内部可以使用全局变量
函数外部不可以使用局部变量
当函数执行完毕，本作用域内的局部变量会销毁。

## 2.2 什么是闭包
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


## 2.3 在chrome中调试闭包
打开浏览器，按 F12 键启动 chrome 调试工具。

设置断点。
找到 Scope 选项（Scope 作用域的意思）。
当我们重新刷新页面，会进入断点调试，Scope 里面会有两个参数（global 全局作用域、local 局部作用域）。
当执行到 fn2() 时，Scope 里面会多一个 Closure 参数 ，这就表明产生了闭包。

![在这里插入图片描述](https://img-blog.csdnimg.cn/487a2da725794758b4e1e2cf54c1aa18.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

## 2.4 闭包的作用
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


## 2.5 闭包练习
### 2.5.1 点击li输出索引号
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

### 2.5.2 定时器中的闭包
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


# 3 递归函数 

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



## 3.1 浅拷贝和深拷贝
1. 浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用
2. 深拷贝拷贝多层，每一级别的数据都会拷贝
3. Object.assign(target,....sources) ES6新增方法可以浅拷贝

### 3.1.1 浅拷贝

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


### 3.1.2 深拷贝
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


