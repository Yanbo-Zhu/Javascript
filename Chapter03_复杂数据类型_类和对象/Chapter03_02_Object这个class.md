
# 1 Object 这个类

为所有 自己定义的 object 的 prototype


# 2 Object 的 Method 

## 2.1 Object.getPrototypeOf()


1 对于 objet 使用 

```js

let obj = {};
console.log(obj);
console.log(Object.getPrototypeOf(obj));
console.log(Object.getPrototypeOf(obj) === Object.prototype);  // 为 ture
console.log(Object.getPrototypeOf(objFunc) === Object.prototype); //// 为 ture

```


2  对于 array 

为所有 自己定义的 array 的 prototype 为 Array 这个 对象, 不对 Object 这个 对象

```js

let arr = [];
console.log(Object.getPrototypeOf(arr));
console.log(Object.getPrototypeOf(arr) === Object.prototype); //// 为 false 
Object.getPrototypeOf(arr) === Array.Prototype  // 为 ture     
```

## 2.2 Object.getOwnPropertyDescriptor()
```js
console.log(Object.getOwnPropertyDescriptor(person, "firstName")); // Schmidt
```



## 2.3 Object.is() 

ES5 比较两个值是否相等，只有两个运算符：相等运算符（`==`）和严格相等运算符（`===`）。它们都有缺点，前者会自动转换数据类型，后者的`NaN`不等于自身，以及`+0`等于`-0`。JavaScript 缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。

ES6 提出“Same-value equality”（同值相等）算法，用来解决这个问题。`Object.is`就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

```js
Object.is('foo', 'foo')
// true
Object.is({}, {})
// false
```

不同之处只有两个：一是`+0`不等于`-0`，二是`NaN`等于自身。

```js
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

## 2.4 Object.assign()

`Object.assign()`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

```js
const target = { a: 1 };

const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```js
const target = { a: 1, b: 1 };

const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

**汇总**

```js
// 基本用法
// Object.assign(目标对象, 源对象1, 源对象2, ...);
const apple = {
    color: '红色',
    shape: '圆形',
    taste: '甜'
};
const pen = {
    color: '黑色',
    shape: '圆柱形',
    use: '写字'
};
console.log(Object.assign(apple, pen));	
// 后面的覆盖前面的（最终返回的不是新的，而是修改了前面的）
// { color: '黑色', shape: '圆柱形', taste: '甜', use: '写字' }
// Object.assign 直接合并到了第一个参数中，返回的就是合并后的对象
console.log(apple);	// { color: '黑色', shape: '圆柱形', taste: '甜', use: '写字' }
console.log(Object.assign(apple, pen) === apple);	// true


// 可以合并多个对象
// 第一个参数使用一个空对象来实现合并返回一个新对象的目的
console.log(Object.assign({}, apple, pen));	// { color: '黑色', shape: '圆柱形', taste: '甜', use: '写字' }
console.log(apple);	// { color: '红色', shape: '圆形', taste: '甜' }
console.log({...apple, ...pen}); // { color: '黑色', shape: '圆柱形', taste: '甜', use: '写字' }


// 注意事项
// (1) 基本数据类型作为源对象
// 与对象的展开类似，先转换成对象，再合并
console.log(Object.assign({}, undefined));	// {}
console.log(Object.assign({}, null));		// {}
console.log(Object.assign({}, 1));			// {}
console.log(Object.assign({}, true));		// {}
console.log(Object.assign({}, 'str'));		// { '0': 's', '1': 't', '2': 'r' }
// (2) 同名属性的替换
// 后面的直接覆盖前面的
const apple = {
    color: ['红色', '黄色'],
    shape: '圆形',
    taste: '甜'
};
const pen = {
    color: ['黑色', '银色'],
    shape: '圆柱形',
    use: '写字'
};
console.log(Object.assign({}, apple, pen));	// { color: [ '黑色', '银色' ], shape: '圆柱形', taste: '甜', use: '写字' }


// 应用
// 合并默认参数和用户参数
const logUser = userOptions => {
    const DEFAULTS = {
        username: 'ZhangSan',
        age: 0,
        sex: 'male'
    };

    const options = Object.assign({}, DEFAULTS, userOptions);
    console.log(options);
};
logUser();						// { username: 'ZhangSan', age: 0, sex: 'male' }
logUser({});					// { username: 'ZhangSan', age: 0, sex: 'male' }
logUser({username: 'Alex'});	// { username: 'Alex', age: 0, sex: 'male' }
```

## 2.5 Object.create()

按照一个已经有的 object 来创造 另外一个 object 
// 这个objekt  "objOneFormProto" wird nach Objekt  "protoObj"modelliert , 从而被产生 

```js

let protoObj = {
    show(par){
        console.log(`${this.type} is ${par}`);
    }
};

let objOneFromProto = Object.create(protoObj); // 这个objekt  "objOneFormProto" wird nach Objekt  "protoObj"modelliert , 从而被产生 


objOneFromProto.type = "simple object";
objOneFromProto.show("still an object"); 

console.log(Object.getPrototypeOf(objOneFromProto));
console.log(Object.getPrototypeOf(objOneFromProto) === Object.prototype);  // false
console.log(Object.getPrototypeOf(objOneFromProto) === protoObj); // true


```

## 2.6 Object.keys()、Object.values() 和 Object.entries()

`Object.keys`方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

`Object.values`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。

`Object.entries()`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。

```js
// 基本用法
const person = {
    name: 'Alex',
    age: 18
};
// 返回键数组
console.log(Object.keys(person));		// [ 'name', 'age' ]
// 返回值数组
console.log(Object.values(person));		// [ 'Alex', 18 ]
// 返回键值二维数组
console.log(Object.entries(person));	// [ [ 'name', 'Alex' ], [ 'age', 18 ] ]


// 与数组类似方法的区别
console.log([1, 2].keys());			// Object [Array Iterator] {}
console.log([1, 2].values());		// Object [Array Iterator] {}
console.log([1, 2].entries());		// Object [Array Iterator] {}
// 数组的 keys()、values()、entries() 等方法是实例方法，返回的都是 Iterator
// 对象的 Object.keys()、Object.values()、Object.entries() 等方法是构造函数方法，返回的是数组


// 应用（使用 for...of 循环遍历对象）
const person = {
    name: 'Alex',
    age: 18
};
for (const key of Object.keys(person)) {
    console.log(key);		
}
// name
// age
for (const value of Object.values(person)) {
    console.log(value);		
}
// Alex
// 18
for (const entries of Object.entries(person)) {
    console.log(entries);	
}
// [ 'name', 'Alex' ]
// [ 'age', 18 ]
for (const [key, value] of Object.entries(person)) {
    console.log(key, value);
}
// name Alex
// age 18

// Object.keys()/values()/entires() 并不能保证顺序一定是你看到的样子，这一点和 for in 是一样的
// 如果对遍历顺序有要求那么不能用 for in 以及这种方法，而要用其他方法
```


### 2.6.1 Object.keys()
Object.keys()用于获取对象自身所有的属性
效果类似for...in
返回一个由属性名组成的数组

```html
<body>
    <script>
        // 用于获取对象自身所有的属性
        var obj = {
            id: 1,
            pname: '小米',
            price: 1999,
            num: 2000
        };
        var arr = Object.keys(obj);
        console.log(arr);
        arr.forEach(function(value) {
            console.log(value);
            // id
            // pname
            // price
            // num
        })
    </script>
</body>
```




## 2.7 Object.defineProperty()

Object.defineProperty()定义对象中新属性或修改原有的属性(了解)
Object.defineProperty(obj, prop, descriptor)

obj : 目标对象
prop : 需定义或修改的属性的名字
descriptor : 目标属性所拥有的特性


第三个参数 descriptor 说明：以对象形式{ }书写
value：设置属性的值，默认为undefined
writeable: 值是否可以重写 true | false 默认为false
enumerable: 目标属性是否可以被枚举 true | false 默认为false
configurable: 目标属性是否可以被删除或是否可以再次修改特性 true | false 默认为false


```html
<body>
    <script>
        // Object.defineProperty() 定义新属性或修改原有的属性
        var obj = {
            id: 1,
            pname: '小米',
            price: 1999
        };
        // 1. 以前的对象添加和修改属性的方式
        // obj.num = 1000;
        // obj.price = 99;
        // console.log(obj);
        // 2. Object.defineProperty() 定义新属性或修改原有的属性
        Object.defineProperty(obj, 'num', {
            value: 1000,
            enumerable: true
        });
        console.log(obj);
        Object.defineProperty(obj, 'price', {
            value: 9.9
        });
        console.log(obj);
        Object.defineProperty(obj, 'id', {
            // 如果值为false 不允许修改这个属性值 默认值也是false
            writable: false,
        });
        obj.id = 2;
        console.log(obj);
        Object.defineProperty(obj, 'address', {
            value: '中国山东蓝翔技校xx单元',
            // 如果只为false 不允许修改这个属性值 默认值也是false
            writable: false,
            // enumerable 如果值为false 则不允许遍历, 默认的值是 false
            enumerable: false,
            // configurable 如果为false 则不允许删除这个属性 不允许在修改第三个参数里面的特性 默认为false
            configurable: false
        });
        console.log(obj);
        console.log(Object.keys(obj));
        delete obj.address;
        console.log(obj);
        delete obj.pname;
        console.log(obj);
        Object.defineProperty(obj, 'address', {
            value: '中国山东蓝翔技校xx单元',
            // 如果值为false 不允许修改这个属性值 默认值也是false
            writable: true,
            // enumerable 如果值为false 则不允许遍历, 默认的值是 false
            enumerable: true,
            // configurable 如果为false 则不允许删除这个属性 默认为false
            configurable: true
        });
        console.log(obj.address);
    </script>
</body>
```





### 2.7.1 writable
```js
	/*writable: change the value of a property*/
	Object.defineProperty(person, "firstName", {
		writable: true
	});

	person.firstName = "Petra";
	console.log(person.firstName);


```

### 2.7.2 configurable
```js
/*configurable: change the value of the property descriptor
Warning: this is a one way action!

if you set configurable:false, then 
You cannot configure any property after this statement
and you cannot delete this property*/

Object.defineProperty(person, "firstName", {configurable:false});

//Object.defineProperty(person, "firstName", {writable: true});
delete person.firstName;   // 会报错 12objectMutable.js:41 Uncaught TypeError: Cannot delete property 'firstName' of #<Object>

console.log(Object.keys(person));
console.clear()
```

### 2.7.3 enumerable

```js
Object.defineProperty(person, "age", {enumerable: false});  
for(let item in person){
    console.log(person[item]);   // 就不显示 age 这个 funtion 了
}
```


```js
console.log('----------2');

Object.defineProperty(person, "hobbies", {enumerable: false});
for(let i=0; i<person.hobbies.length; i++){
    console.log(person.hobbies[i]);
}

console.log('----------3');
Object.defineProperty(person.hobbies, 0, {enumerable: false});

for(let item in person.hobbies){
    console.log(person.hobbies[item]);  // 就不显示 person.hobbies 中的第一项 "turnen" 了 
}
```

## 2.8 综合的例子


```js
(function init(){
	"use strict";

	const person = {
		firstName : "Susi",
		lastName : "Schmidt",
		hobbies : ["turnen", "tanzen", "tischlern"],
		birthYear : 2000,
		happy : true,
		age : function(...a){
			let thisYear = new Date().getFullYear();
			return thisYear - person.birthYear;
		}
	};

	for(let item in person){
		console.log(item + " : " + person[item]);
	}

	console.log(Object.getOwnPropertyDescriptor(person, "firstName"));
	
	/*writable: change the value of a property*/
	Object.defineProperty(person, "firstName", {
		writable: true
	});

	person.firstName = "Petra";
	console.log(person.firstName);


	/*configurable: change the value of the property descriptor
	Warning: this is a one way action!
	if you set configurable:false, then 
	You cannot configure any property after this statement
	and you cannot delete this property*/

	//Object.defineProperty(person, "firstName", {configurable:false});
	Object.defineProperty(person, "firstName", {writable: true});
	delete person.firstName;
	console.log(Object.keys(person));

	console.clear()

	/*enumerable: change the enumerability of properties such as in a for...in loop*/
	for(let item in person){
		console.log(person[item]);
	}

	console.log('----------1');
	
	Object.defineProperty(person, "age", {enumerable: false});
	for(let item in person){
		console.log(person[item]);
	}

	console.log('----------2');

	Object.defineProperty(person, "hobbies", {enumerable: false});
	for(let i=0; i<person.hobbies.length; i++){
		console.log(person.hobbies[i]);
	}

	console.log('----------3');
	Object.defineProperty(person.hobbies, 0, {enumerable: false});

	for(let item in person.hobbies){
		console.log(person.hobbies[item]);
	}

})();
```

