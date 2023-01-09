
# 1 类中的method: 添加新方法

sind Klassen bei ihrer Deklaration fest? Oder können z.b. Methoden oder Attribute in der Laufzeit hinzufügen/löschen
答案是  man 可以 in laufzeit 中随便 往一个 已经存在的 class 中 添加 Methoden oder Attribute

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



# 2 类中的properties: 实例属性的新写法

[ES2022](https://github.com/tc39/proposal-class-fields) 为类的实例属性，又规定了一种新写法。
实例属性现在除了可以定义在`constructor()`方法里面的`this`上面，也可以定义在类内部的最顶层。

```js
// 原来的写法
class IncreasingCounter {
  constructor() {
    this._count = 0;
  }
  get value() {
    console.log('Getting the current value!');
    return this._count;
  }
  increment() {
    this._count++;
  }
}
```

上面示例中，实例属性`_count`定义在`constructor()`方法里面的`this`上面。

现在的新写法是，这个属性也可以定义在类的最顶层，其他都不变。

```js
class IncreasingCounter {
  _count = 0;
  get value() {
    console.log('Getting the current value!');
    return this._count;
  }
  increment() {
    this._count++;
  }
}
```

上面代码中，实例属性`_count`与取值函数`value()`和`increment()`方法，处于同一个层级。这时，不需要在实例属性前面加上`this`。

注意，新写法定义的属性是实例对象自身的属性，而不是定义在实例对象的原型上面。

这种新写法的好处是，所有实例对象自身的属性都定义在类的头部，看上去比较整齐，一眼就能看出这个类有哪些实例属性。

```js
class foo {
  bar = 'hello';
  baz = 'world';

  constructor() {
    // ...
  }
}
```

上面的代码，一眼就能看出，`foo`类有两个实例属性，一目了然。另外，写起来也比较简洁。

# 3 取值函数（getter）和存值函数（setter）

## 3.1 getter

get 语法将一个对象属性绑定到查询该属性时将被调用的一个函数上。

 ```js
 {get prop() { ... } }  // prop:要绑定到给定函数的属性名
 {get [expression]() { ... } } // expression:从ECMAScript 2015 (ES6)开始，还可以使用一个计算的属性名的表达式绑定到给定的函数。
 ```

有时候希望访问属性时能返回一个动态计算后的值, 或希望不通过使用明确的方法调用而显示内部变量的状态.在JavaScript中, 能通过使用 getter 实现. 尽管可能结合使用getter和setter创建一个伪属性,但不能既使用getter绑定到一个属性上,同时又用该属性真实的存储一个值.

在新对象初始化时定义一个getter

这会为obj创建一个虚假的属性latest, 该属性会返回log数组的最后一个元素.

```js
var log = ['test'];
var obj = {
  get latest () {
    if (log.length == 0) return undefined;
    return log[log.length - 1]
  }
}
console.log (obj.latest); // Will return "test".
```

注意,试图赋给latest新值的话不会改变该值.

使用delete操作符删除getter

```js
delete obj.latest;
```

使用defineProperty在存在的对象上定义 getter

在任意时间添加getter到一个存在的对象,使用 Object.defineProperty()

```js
var o = { a:0 }
Object.defineProperty(o, "b", { get: function () { return this.a + 1; } });
console.log(o.b) // Runs the getter, which yields a + 1 (which is 1)
```

## 3.2 setter

 ```js
 {set prop(val) { . . . }}  //prop :要绑定到给定函数的属性名。
 {set [expression](val) { . . . }} 
 //val:用于保存尝试分配给prop的值的变量的一个别名。
 //expression:从ECMAScript 2015 (ES6)开始，还可以使用一个计算的属性名的表达式绑定到给定的函数。
 ```

在 javascript 中，如果试着改变一个属性的值，那么对应的 setter 将被执行。setter 经常和 getter 连用以创建一个伪属性。一个拥有真实值的属性就不能再有 setter 了。

在对象初始化时定义 setter

对象 o 定义一个伪属性 current ，当对它赋值时，将会把值更新到 log：

```js
var o = {
  set current (str) {
    return this.log[this.log.length] = str;
  },
  log: []
}
```

注意，current 属性是未定义的，访问它时将会返回 undefined。

用 delete 操作符移除一个 setter

```js
delete o.current;
```

使用 defineProperty 为已存在的对象定义 setter

可以随时使用Object.defineProperty() 给一个已经存在的对象添加一个 setter。

```javascript
var o = { a:0 };



Object.defineProperty(o, "b", { set: function (x) { this.a = x / 2; } });



o.b = 10; // Runs the setter, which assigns 10 / 2 (5) to the 'a' property
```

## 3.3 es6中的使用 prop

与 ES5 一样，在“类”的内部可以使用`get`和`set`关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。

```js
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

上面代码中，`prop`属性有对应的存值函数和取值函数，因此赋值和读取行为都被自定义了。

存值函数和取值函数是设置在属性的 Descriptor 对象上的。

```js
class CustomHTMLElement {
  constructor(element) {
    this.element = element;
  }

  get html() {
    return this.element.innerHTML;
  }

  set html(value) {
    this.element.innerHTML = value;
  }
}

var descriptor = Object.getOwnPropertyDescriptor(
  CustomHTMLElement.prototype, "html"
);

"get" in descriptor  // true
"set" in descriptor  // true
```

上面代码中，存值函数和取值函数是定义在`html`属性的描述对象上面，这与 ES5 完全一致。

# 4 实例属性、静态方法和静态属性

## 4.1 实例属性

我们之前将类的属性利用 this 的方式写在了构造方法里，把类的方法写在了 class 里。

现在我们还可以把类的属性和方法写在 class 里，然后在构造方法里进行值的修改，或者是提供一个 get set 方法来间接控制变量。

```javascript
class Person {
    _age = 0;        // 类属性之前不能加 var 或 let
    _sex = 'male';   // 类属性被赋予的值相当于就是属性的默认值
    
    /*
    // get、set 还可以用这样的格式来写
    // 这里其实本质上就是定义一个类属性，只不过这个属性指向一个函数而已
    getSex = function() {
        return this._age;
    };
    */

    get age() {
        return this._age;
    }

    set age(value) {
        this._age = value;
    }

    get sex() {
        return this._sex;
    }

    set sex(value) {
        this._sex = value;
    }

    constructor(age, sex) {
        this._age = age;
        this._sex = sex;
    }

    // 类的方法不能用 function 关键字
    speak() {
        console.log(this._age + " " + this._sex);
    }
}
```

## 4.2 静态方法

类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上`static`关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。

```js
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```

上面代码中，`Foo`类的`classMethod`方法前有`static`关键字，表明该方法是一个静态方法，可以直接在`Foo`类上调用（`Foo.classMethod()`），而不是在`Foo`类的实例上调用。如果在实例上调用静态方法，会抛出一个错误，表示不存在该方法。

静态方法的 this 指向问题：静态方法的 this 指向这个类本身。

注意：普通方法 this 指向具体的对象，而静态方法的 this 指向类本身。

```javascript
class Person {
    // 静态属性
    static _name = "user";
    static _age = 18;

    constructor(name, age) {
        this._name = name;
        this._age = age;
    }

    static test() {
        console.log("静态方法");
    }

    // 静态方法
    static readme() {
        // 静态方法中的 this 指向 Person 类本身
        // 并且静态方法的 this 只能引用到类的静态属性及静态方法
        console.log(this._name + " " + this._age);
        this.test();
    }
}

Person.readme();
console.log(Person._name);
/*
user 18
静态方法
user
*/

/*
再次注意：静态方法中只能使用类的静态属性与静态方法
*/
```

注意，如果静态方法包含`this`关键字，这个`this`指的是类，而不是实例。

父类的静态方法，可以被子类继承。

```js
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
}

Bar.classMethod() // 'hello'
```

上面代码中，父类`Foo`有一个静态方法，子类`Bar`可以调用这个方法。

静态方法也是可以从`super`对象上调用的。

```js
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
  static classMethod() {
    return super.classMethod() + ', too';
  }
}

Bar.classMethod() // "hello, too"
```

## 4.3 静态属性

静态属性指的是 Class 本身的属性，即`Class.propName`，而不是定义在实例对象（`this`）上的属性。

```js
class Foo {
}

Foo.prop = 1;
Foo.prop // 1
```

上面的写法为`Foo`类定义了一个静态属性`prop`。

目前，只有这种写法可行，因为 ES6 明确规定，Class 内部只有静态方法，没有静态属性。现在有一个[提案](https://github.com/tc39/proposal-class-fields)提供了类的静态属性，写法是在实例属性的前面，加上`static`关键字。

```js
class MyClass {
  static myStaticProp = 42;

  constructor() {
    console.log(MyClass.myStaticProp); // 42
  }
}
```

这个新写法大大方便了静态属性的表达。

```js
// 老写法
class Foo {
  // ...
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
```

上面代码中，老写法的静态属性定义在类的外部。整个类生成以后，再生成静态属性。这样让人很容易忽略这个静态属性，也不符合相关代码应该放在一起的代码组织原则。另外，新写法是显式声明（declarative），而不是赋值处理，语义更好。

注意：静态属性 static 的定义方法目前只是一个提案，目前不推荐这样写！某些浏览器不支持。

```js
class Person {
    constructor(name) {
        this.name = name;
    }
    
    // 目前不推荐 static 这种写法，因为还只是一个提案
    // static version = "1.0";
    
    // 推荐利用静态方法来间接实现静态属性
    static getVersion() {
        return "1.0";
    }
}
```

# 5 私有方法和私有属性

## 5.1 早期解决方案

```js
// 方式一：在属性开头加上 _ 表示私有
class Person {
    constructor(name) {
        this._name = name;
    }
    
    _speak() {
        console.log("speak");
    }
    
    getName() {
        return this._name;
    }
}

const p = new Person('Alex');
console.log(p.name);	// 报错！
// console.log(p._name);	// Alex，但是这样做就无意义了，违背了私有化的初衷

/*
注意：加下划线的方式实际上只是行业中约定俗成的一种方法，
我们依旧可以通过 p._name，来访问，但是这样做就无意义了！所以这种方法的使用纯靠程序员自觉。
*/
```

```js
// 方式二：将私有属性和方法移出类（使用模块）
// 我们目前用立即执行函数（闭包原理）来模拟
(function () {
    let name = "";
    let speak = function () {
        console.log("speak");
    }

    class Person {
        constructor(username) {
            name = username;
        }

        getName() {
            return name;
        }

        runSpeak() {
            speak();
        }
    }

    // 将类添加到全局作用域中暴露
    window.Person = Person;
})();

const p = new Person('Alex');
console.log(p.name);	// 报错
console.log(p.getName());	// Alex
p.runSpeak();	// speak
```

## 5.2 私有属性的正式写法

[ES2022](https://github.com/tc39/proposal-class-fields)正式为`class`添加了私有属性，方法是在属性名之前使用`#`表示。

```js
class IncreasingCounter {
  #count = 0;
  get value() {
    console.log('Getting the current value!');
    return this.#count;
  }
  increment() {
    this.#count++;
  }
}
```

上面代码中，`#count`就是私有属性，只能在类的内部使用（`this.#count`）。如果在类的外部使用，就会报错。

```js
const counter = new IncreasingCounter();
counter.#count // 报错
counter.#count = 42 // 报错
```

上面示例中，在类的外部，读取或写入私有属性`#count`，都会报错。

另外，不管在类的内部或外部，读取一个不存在的私有属性，也都会报错。这跟公开属性的行为完全不同，如果读取一个不存在的公开属性，不会报错，只会返回`undefined`。

```js
class IncreasingCounter {
  #count = 0;
  get value() {
    console.log('Getting the current value!');
    return this.#myCount; // 报错
  }
  increment() {
    this.#count++;
  }
}

const counter = new IncreasingCounter();
counter.#myCount // 报错
```

上面示例中，`#myCount`是一个不存在的私有属性，不管在函数内部或外部，读取该属性都会导致报错。

注意，私有属性的属性名必须包括`#`，如果不带`#`，会被当作另一个属性。

```js
class Point {
  #x;

  constructor(x = 0) {
    this.#x = +x;
  }

  get x() {
    return this.#x;
  }

  set x(value) {
    this.#x = +value;
  }
}
```

上面代码中，`#x`就是私有属性，在`Point`类之外是读取不到这个属性的。由于井号`#`是属性名的一部分，使用时必须带有`#`一起使用，所以`#x`和`x`是两个不同的属性。

这种写法不仅可以写私有属性，还可以用来写私有方法。

```js
class Foo {
  #a;
  #b;
  constructor(a, b) {
    this.#a = a;
    this.#b = b;
  }
  #sum() {
    return this.#a + this.#b;
  }
  printSum() {
    console.log(this.#sum());
  }
}
```

上面示例中，`#sum()`就是一个私有方法。

另外，私有属性也可以设置 getter 和 setter 方法。

```js
class Counter {
  #xValue = 0;

  constructor() {
    console.log(this.#x);
  }

  get #x() { return this.#xValue; }
  set #x(value) {
    this.#xValue = value;
  }
}
```

上面代码中，`#x`是一个私有属性，它的读写都通过`get #x()`和`set #x()`操作另一个私有属性`#xValue`来完成。

私有属性不限于从`this`引用，只要是在类的内部，实例也可以引用私有属性。

```js
class Foo {
  #privateValue = 42;
  static getPrivateValue(foo) {
    return foo.#privateValue;
  }
}

Foo.getPrivateValue(new Foo()); // 42
```

上面代码允许从实例`foo`上面引用私有属性。

私有属性和私有方法前面，也可以加上`static`关键字，表示这是一个静态的私有属性或私有方法。

```js
class FakeMath {
  static PI = 22 / 7;
  static #totallyRandomNumber = 4;

  static #computeRandomNumber() {
    return FakeMath.#totallyRandomNumber;
  }

  static random() {
    console.log('I heard you like random numbers…')
    return FakeMath.#computeRandomNumber();
  }
}

FakeMath.PI // 3.142857142857143
FakeMath.random()
// I heard you like random numbers…
// 4
FakeMath.#totallyRandomNumber // 报错
FakeMath.#computeRandomNumber() // 报错
```

上面代码中，`#totallyRandomNumber`是私有属性，`#computeRandomNumber()`是私有方法，只能在`FakeMath`这个类的内部调用，外部调用就会报错。

