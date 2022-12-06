# 1 面向对象
面向对象更贴近我们的实际生活, 可以使用面向对象描述现实世界事物. 但是事物分为具体的事物和抽象的事物

面向对象的思维特点：
1. 抽取（抽象）对象共用的属性和行为组织(封装)成一个类(模板)
2. 对类进行实例化, 获取类的对象

## 1.1 对象
在 JavaScript 中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串、数值、数组、函数等。

对象是由属性和方法组成的

属性：事物的特征，在对象中用属性来表示
方法：事物的行为，在对象中用方法来表示

## 1.2 类
在 ES6 中新增加了类的概念，可以使用 class 关键字声明一个类，之后以这个类来实例化对象。

类抽象了对象的公共部分，它泛指某一大类（class）
对象特指某一个，通过类实例化一个具体的对象

## 1.3 创建类

```js
class name {
    // class body
}
```


### 1.3.1 创建实例
var XX = new name();

注意：类必须使用new 实例化对象

### 1.3.2 构造函数
constructor() 方法是类的构造函数(默认方法)，用于传递参数,返回实例对象，通过 new 命令生成对象实例时，自动调用该方法。如果没有显示定义, 类内部会自动给我们创建一个constructor()

```html
<script>
    // 1. 创建类 class  创建一个 明星类
    class Star {
        // constructor 构造器或者构造函数
        constructor(uname, age) {
            this.uname = uname;
            this.age = age;
        }
    }

    // 2. 利用类创建对象 new
    var ldh = new Star('刘德华', 18);
    var zxy = new Star('张学友', 20);
    console.log(ldh);
    console.log(zxy);
</script>

```



通过 class 关键字创建类，类名我们还是习惯性定义首字母大写
类里面有个 constructor函数，可以接收传递过来的参数，同时返回实例对象
constructor函数只要 new 生成实例时，就会自动调用这个函数，如果我们不写这个函数，类也会自动生成这个函数
最后注意语法规范
- 创建类➡类名后面不要加小括号
- 生成实例➡类名后面加小括号
- 构造函数不需要加 function 关键字

### 1.3.3 类中添加方法
语法：
```js
class Person {
  constructor(name,age) {   
      // constructor 称为构造器或者构造函数
      this.name = name;
      this.age = age;
    }
   say() {
      console.log(this.name + '你好');
   }
}      
var ldh = new Person('刘德华', 18); 
ldh.say() 
```


注意： 方法之间不能加逗号分隔，同时方法不需要添加 function 关键字。

类的共有属性放到constructor 里面
类里面的函数都不需要写 function 关键字

```html
<script>
    // 1. 创建类 class  创建一个 明星类
    class Star {
        // 类的共有属性放到 constructor 里面
        constructor(uname, age) {
            this.uname = uname;
            this.age = age;
        }
        sing(song) {
            console.log(this.uname + song);
        }
    }

    // 2. 利用类创建对象 new
    var ldh = new Star('刘德华', 18);
    var zxy = new Star('张学友', 20);
    console.log(ldh);
    console.log(zxy);
    
    // (1) 我们类里面所有的函数不需要写function 
    // (2) 多个函数方法之间不需要添加逗号分隔
    ldh.sing('冰雨');
    zxy.sing('李香兰');
</script>
```




## 1.4 类的继承
现实中的继承：子承父业，比如我们都继承了父亲的姓。
程序中的继承：子类可以继承父类的一些属性和方法。

语法：
```js
// 父类
class Father {
    
}
// 子类继承父类
class Son extends Father {
    
}
```


看一个实例：
```html
<script>
    // 父类有加法方法
    class Father {
        constructor(x, y) {
            this.x = x;
            this.y = y;
        }
        sum() {
            console.log(this.x + this.y);
        }
    }
    // 子类继承父类加法方法 同时 扩展减法方法
    class Son extends Father {
        constructor(x, y) {
            // 利用super 调用父类的构造函数
            // super 必须在子类this之前调用
            super(x, y);
            this.x = x;
            this.y = y;
        }
        subtract() {
            console.log(this.x - this.y);
        }
    }
    var son = new Son(5, 3);
    son.subtract();
    son.sum();
</script>
```

## 1.5 super关键字
super 关键字用于访问和调用对象父类上的函数，可以调用父类的构造函数，也可以调用父类的普通函数

### 1.5.1 调用父类的构造函数
语法：
```js
// 父类
class Person {
    constructor(surname){
        this.surname = surname;
    }
}
// 子类继承父类
class Student entends Person {
    constructor(surname,firstname) {
        super(surname);					//调用父类的 constructor(surname)
        this.firstname = firstname;		//定义子类独有的属性
    }
}
```


注意：子类在构造函数中使用super,必须放到this前面（必须先调用父类的构造方法，在使用子类构造方法）

案例：
```js
// 父类
class Father {
    constructor(surname){
        this.surname = surname;
    }
    saySurname() {
        console.log('我的姓是' + this.surname);
    }
}
// 子类继承父类
class Son entends Father {
    constructor(surname,firstname) {
        super(surname);					//调用父类的 constructor(surname)
        this.firstname = firstname;		//定义子类独有的属性
    }
    sayFirstname() {
        console.log('我的名字是:' + this.firstname);
    }
}

var damao = new Son('刘','德华');
damao.saySurname();
damao.sayFirstname();
```



### 1.5.2 调用父类的普通函数

多个方法之间不需要添加逗号分隔
继承中属性和方法的查找原则：就近原则，先看子类，再看父类

语法：
```js
class Father {
    say() {
        return '我是爸爸';
    }
}
class Son extends Father {
    say(){
        // super.say() super调用父类的方法
        return super.say() + '的儿子';
    }
}

var damao = new Son();
console.log(damao.say());
```



## 1.6 注意点
在ES6中类没有变量提升，所以必须先定义类，才能通过类实例化对象

## 1.7 this 的使用
类里面的共有属性和方法一定要加 this使用
类里面的this指向：
- constructor 里面的 this指向实例对象
- 方法里面的this指向这个方法的调用者

```html
<body>
    <button>点击</button>
    <script>
        var that;
        var _that;
        class Star {
            constructor(uname, age) {
                // constructor 里面的this 指向的是 创建的实例对象
                that = this;
                this.uname = uname;
                this.age = age;
                // this.sing();
                this.btn = document.querySelector('button');
                this.btn.onclick = this.sing;
            }
            sing() {
            // 这个sing方法里面的this 指向的是 btn 这个按钮,因为这个按钮调用了这个函数
                console.log(that.uname); 
                // that里面存储的是constructor里面的this
            }
            dance() {
                // 这个dance里面的this 指向的是实例对象 ldh 因为ldh 调用了这个函数
                _that = this;
                console.log(this);
            }
        }
        var ldh = new Star('刘德华');
        console.log(that === ldh);
        ldh.dance();
        console.log(_that === ldh);

        // 1. 在 ES6 中类没有变量提升，所以必须先定义类，才能通过类实例化对象

        // 2. 类里面的共有的属性和方法一定要加this使用.
    </script>
</body>

```


# 2 构造函数和原型
## 2.1 概述
在典型的 OOP 的语言中（如 Java），都存在类的概念，类就是对象的模板，对象就是类的实例，但在 ES6之前， JS 中并没用引入类的概念。

ES6， 全称 ECMAScript 6.0 ，2015.06 发版。但是目前浏览器的 JavaScript 是 ES5 版本，大多数高版本的浏览器也支持 ES6，不过只实现了 ES6 的部分特性和功能。

在 ES6之前 ，对象不是基于类创建的，而是用一种称为构建函数的特殊函数来定义对象和它们的特征。

## 2.2 创建对象有三种方式
- 对象字面量
- new Object()
- 自定义构造函数


```js
// 1. 利用 new Object() 创建对象
var obj1 = new Object();

// 2. 利用对象字面量创建对象
var obj2 = {}；

// 3.利用构造函数创建对象
function Star(uname,age) {
    this.uname = uname;
    this.age = age;
    this.sing = function() {
        console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华',18);
```



注意：
构造函数用于创建某一类对象，其首字母要大写
构造函数要和new一起使用才有意义


## 2.3 构造函数
构造函数是一种特殊的函数，主要用来初始化对象(为对象成员变量赋初始值)，它总与new一起使用
我们可以把对象中的一些公共的属性和方法抽取出来，然后封装到这个函数里面

new 在执行时会做四件事
- 在内存中创建一个新的空对象。
- 让 this 指向这个新的对象。
- 执行构造函数里面的代码，给这个新对象添加属性和方法。
- 返回这个新对象（所以构造函数里面不需要 return ）。

### 2.3.1 静态成员和实例成员
JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的this上添加。通过这两种方式添加的成员，就分别称为静态成员和实例成员。

静态成员: 在构造函数本身上添加的成员为静态成员，只能由构造函数本身来访问
实例成员: 在构造函数内部创建的对象成员称为实例成员，只能由实例化的对象来访问

```js
// 构造函数中的属性和方法我们称为成员，成员可以添加
function Star(uname,age) {
    this.uname = uname;
    this.age = age;
    this.sing = function() {
        console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华',18);

// 实例成员就是构造函数内部通过this添加的成员  uname age sing  就是实例成员
// 实例成员只能通过实例化的对象来访问
ldh.sing();
Star.uname; // undefined     不可以通过构造函数来访问实例成员

// 静态成员就是在构造函数本身上添加的成员 sex 就是静态成员
// 静态成员只能通过构造函数来访问
Star.sex = '男';
Star.sex;
ldh.sex; // undefined  不能通过对象来访问
```



### 2.3.2 构造函数的问题
构造函数方法很好用，但是存在浪费内存的问题。
我们希望所有的对象使用同一个函数，这样就比较节省内存

![在这里插入图片描述](https://img-blog.csdnimg.cn/080f8513ab074159abf16942fd009b2b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)



## 2.4 构造函数原型 prototype
构造函数通过原型分配的函数是所有对象所共享的,这样就解决了内存浪费问题
JavaScript 规定，每一个构造函数都有一个prototype属性，指向另一个对象，注意这个prototype就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有
我们可以把那些不变的方法，直接定义在prototype 对象上，这样所有对象的实例就可以共享这些方法

一般情况下,我们的公共属性定义到构造函数里面, 公共的方法我们放到原型对象身上
-   原型就是一个对象，我们也称为prototype为对象
-   原型的作用就是 共享方法。

```html
<body>
    <script>
        // 1. 构造函数的问题. 
        function Star(uname, age) {
    		//公共属性定义到构造函数里面
            this.uname = uname;
            this.age = age;
            // this.sing = function() {
            //     console.log('我会唱歌');
            // }
        }
		//公共的方法我们放到原型对象身上
        Star.prototype.sing = function() {
            console.log('我会唱歌');
        }
        var ldh = new Star('刘德华', 18);
        var zxy = new Star('张学友', 19);
        console.log(ldh.sing === zxy.sing);
        ldh.sing();
        zxy.sing();
        // 2. 一般情况下,我们的公共属性定义到构造函数里面, 公共的方法我们放到原型对象身上
    </script>
</body>
```





## 2.5 对象原型 __ proto __
- 对象都会有一个属性 __ proto __ 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 __ proto __ 原型的存在。
- __ proto __ 对象原型和原型对象 prototype 是等价的
- __ proto __ 对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是他是一个非标准，因此在实际开发中，不可以使用这个属性，他只是内部向原型对象 prototype。
- __ proto __ 对象原型
- prototype 原型对象


![在这里插入图片描述](https://img-blog.csdnimg.cn/e8e771c189c548f7b67209722f6289dc.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

1 Star.prototype 和 ldh._proto_ 指向相同
```html
<body>
    <script>
        function Star(uname, age) {
            this.uname = uname;
            this.age = age;
        }
        Star.prototype.sing = function() {
            console.log('我会唱歌');
        }
        var ldh = new Star('刘德华', 18);
        var zxy = new Star('张学友', 19);
        ldh.sing();
        console.log(ldh); 
		// 对象身上系统自己添加一个 __proto__ 指向我们构造函数的原型对象 prototype
        console.log(ldh.__proto__ === Star.prototype);
        // 方法的查找规则: 首先先看ldh 对象身上是否有 sing 方法,如果有就执行这个对象上的sing
        // 如果没有sing 这个方法,因为有 __proto__ 的存在,就去构造函数原型对象prototype身上去查找sing这个方法
    </script>
</body>
```

## 2.6 constructor 构造函数
对象原型(__ proto __) 和构造函数(prototype)原型对象 里面都有一个属性 constructor 属性， constructor 我们称为构造函数，因为它指回构造函数本身。

constructor主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数

一般情况下，对象的方法都在构造函数(prototype)的原型对象中设置

如果有多个对象的方法，我们可以给原型对象prototype采取对象形式赋值，但是这样会覆盖构造函数原型对象原来的内容，这样修改后的原型对象constructor就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个constructor指向原来的构造函数

具体请看实例配合理解
```html
<body>
    <script>
        function Star(uname, age) {
            this.uname = uname;
            this.age = age;
        }
        // 很多情况下,我们需要手动的利用constructor 这个属性指回 原来的构造函数
        // Star.prototype.sing = function() {
        //     console.log('我会唱歌');
        // };
        // Star.prototype.movie = function() {
        //     console.log('我会演电影');
        // }
        Star.prototype = {
            // 如果我们修改了原来的原型对象,给原型对象赋值的是一个对象,则必须手动的利用constructor指回原来的构造函数
            constructor: Star,
            sing: function() {
                console.log('我会唱歌');
            },
            movie: function() {
                console.log('我会演电影');
            }
        }
        var ldh = new Star('刘德华', 18);
        var zxy = new Star('张学友', 19);
    </script>
</body>
```




## 2.7 构造函数、实例、原型对象三者关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/8ee8345e99974afd93ce053e7988712d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

## 2.8 js的成员查找机制(原型链)
1. 当访问一个对象的属性(包括方法)时，首先查找这个对象自身有没有该属性
2. 如果没有就查找它的原型(也就是_proto_指向的prototype原型对象)
3. 如果还没有就查找原型对象的原型(Object的原型对象)
4. 依次类推一直找到Object为止(null)
5. __ proto __对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。
   
![在这里插入图片描述](https://img-blog.csdnimg.cn/c1cbd18ff3444621bf151654714b85cd.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

```html
<body>
    <script>
        function Star(uname, age) {
            this.uname = uname;
            this.age = age;
        }
        Star.prototype.sing = function() {
            console.log('我会唱歌');
        }
        var ldh = new Star('刘德华', 18);
        // 1. 只要是对象就有__proto__ 原型, 指向原型对象
        console.log(Star.prototype);
        console.log(Star.prototype.__proto__ === Object.prototype);
        // 2.我们Star原型对象里面的__proto__原型指向的是 Object.prototype
        console.log(Object.prototype.__proto__);
        // 3. 我们Object.prototype原型对象里面的__proto__原型  指向为 null
    </script>
</body>
```



## 2.9 原型对象this指向
- 构造函数中的 this指向我们的实例对象
- 原型对象里面放的是方法，这个方法里面的this指向的是这个方法的调用者，也就是这个实例对象

```html
<body>
    <script>
        function Star(uname, age) {
            this.uname = uname;
            this.age = age;
        }
        var that;
        Star.prototype.sing = function() {
            console.log('我会唱歌');
            that = this;
        }
        var ldh = new Star('刘德华', 18);
        // 1. 在构造函数中,里面this指向的是对象实例 ldh
        ldh.sing();
        console.log(that === ldh);

        // 2.原型对象函数里面的this 指向的是 实例对象 ldh
    </script>
</body>
```


## 2.10 扩展内置对象
可以通过原型对象，对原来的内置对象进行扩展自定义的方法. 比如给数组增加自定义求偶数和的功能
注意： 数组和字符串内置对象不能给原型对象覆盖操作Array.prototype = {}，只能是Array.prototype.xxx = function(){}的方式


```html
<body>
    <script>
        // 原型对象的应用 扩展内置对象方法

        Array.prototype.sum = function() {
            var sum = 0;
            for (var i = 0; i < this.length; i++) {
                sum += this[i];
            }
            return sum;
        };
        // Array.prototype = {
        //     sum: function() {
        //         var sum = 0;
        //         for (var i = 0; i < this.length; i++) {
        //             sum += this[i];
        //         }
        //         return sum;
        //     }

        // }
        var arr = [1, 2, 3];
        console.log(arr.sum());
        console.log(Array.prototype);
        var arr1 = new Array(11, 22, 33);
        console.log(arr1.sum());
    </script>
</body>
```


# 3 继承
ES6 之前并没有给我们提供extends继承

我们可以通过构造函数+原型对象模拟实现继承，被称为组合继承

## 3.1 call()
调用这个函数，并且修改函数运行时的 this 指向

fun.call(thisArg,arg1,arg2,......)
- thisArg：当前调用函数 this 的指向对象
- arg1,arg2： 传递的其他参数

```html
<body>
    <script>
        // call 方法
        function fn(x, y) {
            console.log('我希望我的希望有希望');
            console.log(this);		// Object{...}
            console.log(x + y);		// 3
        }

        var o = {
            name: 'andy'
        };
        // fn();
        // 1. call() 可以调用函数
        // fn.call();
        // 2. call() 可以改变这个函数的this指向 此时这个函数的this 就指向了o这个对象
        fn.call(o, 1, 2);
    </script>
</body>
```

## 3.2 继承
ES 6之前并没有给我们提供extends继承 我们可以通过构造函数+原型对象模拟实训继承，被称为组合继承
借用构造函数继承父类型属性 (2-11)
核心原理：通过call() 把父类型的this 指向子类型的this ， 这样就可以实现子类型继承父类型的属性。
借用原型对象继承父类型方法 (2-12)


### 3.2.1 借用构造函数继承父类型属性/继承父构造函数属性
核心原理: 通过 call() 把父类型的 this 指向子类型的 this，这样就可以实现子类型继承父类型的属性

```html
<body>
    <script>
        // 借用父构造函数继承属性
        // 1. 父构造函数
        function Father(uname, age) {
            // this 指向父构造函数的对象实例
            this.uname = uname;
            this.age = age;
        }
        // 2 .子构造函数 
        function Son(uname, age, score) {
            // this 指向子构造函数的对象实例
            Father.call(this, uname, age);
            this.score = score;
        }
        var son = new Son('刘德华', 18, 100);
        console.log(son);
    </script>
</body>
```



### 3.2.2 借用原型对象继承父类型方法
一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法

核心原理：
将子类所共享的方法提取出来，让子类的 prototype 原型对象 = new 父类()
本质： 子类原型对象等于是实例化父类，因为父类实例化之后另外开辟空间，就不会影响原来父类原型对象
将子类的constructor重新指向子类的构造函数

```html
<body>
    <script>
        // 借用父构造函数继承属性
        // 1. 父构造函数
        function Father(uname, age) {
            // this 指向父构造函数的对象实例
            this.uname = uname;
            this.age = age;
        }
        Father.prototype.money = function() {
            console.log(100000);

        };
        // 2 .子构造函数 
        function Son(uname, age, score) {
            // this 指向子构造函数的对象实例
            Father.call(this, uname, age);
            this.score = score;
        }
        // Son.prototype = Father.prototype;  这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化
        Son.prototype = new Father();
        // 如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数
        Son.prototype.constructor = Son;
        // 这个是子构造函数专门的方法
        Son.prototype.exam = function() {
            console.log('孩子要考试');

        }
        var son = new Son('刘德华', 18, 100);
        console.log(son);
        console.log(Father.prototype);
        console.log(Son.prototype.constructor);
    </script>
</body>
```


## 3.3 类的本质
- class 本质还是 function
- 类的所有方法都定义在类的 prototype属性上
- 类创建的实例，里面也有_proto_指向类的prototype原型对象
- 所以 ES6 的类它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
- 所以 ES6 的类其实就是语法糖
- 语法糖：语法糖就是一种便捷写法，简单理解
