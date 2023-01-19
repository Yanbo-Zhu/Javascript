# 1 对象的扩展

## 1.1 方括号语法 (得到某个properties 的值)

### 1.1.1 方括号语法的用法

```javascript
const prop = 'age';
const person = {};
person.prop = 18;
console.log(person);	// { prop: 18 }

// -----------------------------------------

const prop = 'age';
const person = {};
person[prop] = 18;
console.log(person);	// { age: 18 }

// -----------------------------------------

// ES6 增强
const prop = 'age';
const person = {
    [prop]: 18
};
console.log(person);	// { age: 18 }
```

### 1.1.2 方括号中可以放什么

```javascript
// [值、可以得到值的表达式]
const prop = 'age';
const func = () => 'age2';
const person = {
    [prop]: 18,
    [func()]: 24,
    ['sex']: 'man',
    ['s' + 'ex2']: 'womam'
};
console.log(person);	// { age: 18, age2: 24, sex: 'man', sex2: 'womam' }
```

注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串`[object Object]`，这一点要特别小心。

```js
const keyA = {a: 1};
const keyB = {b: 2};

const myObject = {
  [keyA]: 'valueA',
  [keyB]: 'valueB'
};

myObject // Object {[object Object]: "valueB"}
```

上面代码中，`[keyA]`和`[keyB]`得到的都是`[object Object]`，所以`[keyB]`会把`[keyA]`覆盖掉，而`myObject`最后只有一个`[object Object]`属性。

### 1.1.3 方括号语法和点语法的区别

1. 点语法是方括号语法的特殊形式
2. 属性名由数字、字母、下划线以及 $ 构成，并且数字还不能打头的时候可以使用点语法（合法标识符）
3. 能用点语法优先使用点语法

```javascript
const person = {
    age: 18
};

person.age 等价于 person['age']
```

## 1.2 super 关键字

我们知道，`this`关键字总是指向函数所在的当前对象，ES6 又新增了另一个类似的关键字`super`，指向当前对象的原型对象。

```js
const proto = {
  foo: 'hello'
};

const obj = {
  foo: 'world',
  find() {
    return super.foo;
  }
};

Object.setPrototypeOf(obj, proto);
obj.find() // "hello"
```

上面代码中，对象`obj.find()`方法之中，通过`super.foo`引用了原型对象`proto`的`foo`属性。

注意，`super`关键字表示原型对象时，只能用在对象的方法之中，用在其他地方都会报错。

```js
// 报错
const obj = {
  foo: super.foo
}

// 报错
const obj = {
  foo: () => super.foo
}

// 报错
const obj = {
  foo: function () {
    return super.foo
  }
}
```

上面三种`super`的用法都会报错，因为对于 JavaScript 引擎来说，这里的`super`都没有用在对象的方法之中。第一种写法是`super`用在属性里面，第二种和第三种写法是`super`用在一个函数里面，然后赋值给`foo`属性。目前，只有对象方法的简写法可以让 JavaScript 引擎确认，定义的是对象的方法。

JavaScript 引擎内部，`super.foo`等同于`Object.getPrototypeOf(this).foo`（属性）或`Object.getPrototypeOf(this).foo.call(this)`（方法）。

```js
const proto = {
  x: 'hello',
  foo() {
    console.log(this.x);
  },
};

const obj = {
  x: 'world',
  foo() {
    super.foo();
  }
}

Object.setPrototypeOf(obj, proto);

obj.foo() // "world"
```

上面代码中，`super.foo`指向原型对象`proto`的`foo`方法，但是绑定的`this`却还是当前对象`obj`，因此输出的就是`world`。

## 1.3 对象的展开运算符

### 1.3.1 展开对象

对象不能直接展开，必须在 {} 中展开。

```javascript
const apple = {
    color: '红色',
    shape: '球形',
    taste: '甜'
};
console.log({...apple});			// { color: '红色', shape: '球形', taste: '甜' }
console.log({...apple} === apple);	// false
```

### 1.3.2 合并对象

```javascript
const apple = {
    color: '红色',
    shape: '球形',
    taste: '甜'
};

const pen = {
    color: '黑色',
    shape: '圆柱形',
    use: '写字'
};

// 新对象拥有全部属性，相同属性，后者覆盖前者
console.log({...apple, ...pen});	// { color: '黑色', shape: '圆柱形', taste: '甜', use: '写字' }
console.log({...pen, ...apple});	// { color: '红色', shape: '球形', use: '写字', taste: '甜' }
```

### 1.3.3 注意事项

#### 1.3.3.1 空对象的展开

如果展开一个空对象，则没有任何效果。

```javascript
console.log({...{}});			// {}
console.log({...{}, a: 1});		// { a: 1 }
```

#### 1.3.3.2 非对象的展开

如果展开的不是对象，则会自动将其转为对象，再将其属性罗列出来（没有属性便为空）。

```javascript
console.log({...1});			// {}
console.log(new Object(1));		// [Number: 1]
console.log({...undefined});	// {}
console.log({...null});			// {}
console.log({...true});			// {}
```

#### 1.3.3.3 字符串的展开

如果展开运算符后面是字符串，它会自动转成一个类似数组的对象，因此返回的不是空对象。

```javascript
// 字符串在对象中展开
console.log({...'alex'});		// { '0': 'a', '1': 'l', '2': 'e', '3': 'x' }

// 字符串在数组中展开
console.log([...'alex']);		// [ 'a', 'l', 'e', 'x' ]

// 字符串直接展开
console.log(...'alex');			// a l e x
```

#### 1.3.3.4 数组的展开

```javascript
console.log({...[1, 2, 3]});	// { '0': 1, '1': 2, '2': 3 }
```

#### 1.3.3.5 对象中对象属性的展开

不会展开对象中的对象属性。

```javascript
const apple = {
    feature: {
        taste: '甜'
    }
};

const pen = {
    feature: {
        color: '黑色',
        shape: '圆柱形'
    },
    use: '写字'
};

console.log({...apple});			// { feature: { taste: '甜' } }

// feature 会直接覆盖，因为 feature 不能展开
console.log({...apple, ...pen});	// { feature: { color: '黑色', shape: '圆柱形' }, use: '写字' }
```

### 1.3.4 对象展开运算符的应用

#### 1.3.4.1 复制对象

```javascript
const a = {x: 1, y: 2};
const c = {...a};
console.log(c, c === a);
// { x: 1, y: 2 } false
```

#### 1.3.4.2 用户参数和默认参数

```javascript
const logUser = userParam => {
    const defaultPeram = {
        username: 'ZhangSan',
        age: 0,
        sex: 'male'
    };

    const param = {...defaultPeram, ...userParam};
    console.log(param.username, param.age, param.sex);
};

logUser({username: 'jerry'});	// jerry 0 male
```

再优化：

```javascript
const logUser = userParam => {
    const defaultPeram = {
        username: 'ZhangSan',
        age: 0,
        sex: 'male'
    };

    const {username, age, sex} = {...defaultPeram, ...userParam};
    console.log(username, age, sex);
};

logUser({username: 'jerry'});	// jerry 0 male
```

