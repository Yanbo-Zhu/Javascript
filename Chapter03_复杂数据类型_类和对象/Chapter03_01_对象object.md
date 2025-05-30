![在这里插入图片描述](https://img-blog.csdnimg.cn/b55a7b4391df4f058cc8003baf0565db.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

# 1 3种对象

JavaScript 中的对象分为3种：自定义对象 、内置对象、 浏览器对象

# 2 对象理论


- **_Objekte_** sind Kollektionen von Eigenschaften und werden durch geschweifte Klammern zusammen gehalten
- Eigenschaften bestehen aus einem Namen und ihrem Wert
- Wert einer _**Eigenschaft**_ kann ein Literal, eine Variable eines primitiven Datenobjekts, ein Feld, ein Objekt oder eine Funktion sein
- Eigenschaften, die Funktionen als Wert haben, heissen _**Methoden**_
- Mehrere Eigenschaften werden durch Komma getrennt

在 JavaScript 中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串、数值、数组、函数等。

对象是由属性和方法组成的：

属性：事物的特征，在对象中用属性来表示（常用名词）
方法：事物的行为，在对象中用方法来表示（常用动词）




对象的 数据类型是 object
```js
let anyObject = {
    firstName:	"me",
    lastName:	"Object",
    human:	false
};

console.log(anyObject, typeof anyObject);
```



```js
let vorlesung = {
  title: "Webtechnologien",
  description: "Vorlesung für *informatiker*innen",
  seats: 18,
  readSeats: function() {
    console.log("Anzahl der Plätze für "+this.title+": "+this.seats);
  },
  writeSeats: function(newNumber) {
    this.seats=newNumber;
  },
  "5": "fünf"
};
```


![](image/Pasted%20image%2020250218102049.png)

![](image/Pasted%20image%2020250218102228.png)

# 3 Naming der Objekt 

- Namen von Eigenschaften müssen gültige Bezeichner sein, die Groß- und Kleinbuchstaben, Zahlen, `**$**` und `**_**` enthalten und nicht mit einer Zahl beginnen 
- Namen, die hiervon abweichen, müssen in Anführungszeichen geschrieben werden
- Neue Elemente können einem Objekt hinzugefügt werden durch Zuweisung eines Wertes an eine Eigenschaft mit einem noch nicht vergebenen Namen
- Eigenschaften werden aus einem Objekt mit Hilfe des `**delete**`-Operators gelöscht
- Der `**in**`-Operator prüft, ob ein Objekt eine Eigenschaft mit dem in Anführungszeichen angegeben Namen besitzt



# 4 创建对象

在 JavaScript 中，现阶段我们可以采用三种方式创建对象（object）：

利用字面量创建对象
利用 new Object创建对象
利用构造函数创建对象

## 4.1 与创建数组的不同 

```js
let objectNoProps = {};
console.log(objectNoProps, typeof objectNoProps);

let arrNoProps = [];
console.log(arrNoProps, typeof arrNoProps);	
```

## 4.2 利用字面量创建对象 

对象字面量：就是花括号 { } 里面包含了表达这个具体事物（对象）的属性和方法

{ } 里面采取键值对的形式表示
键：相当于属性名
值：相当于属性值，可以是任意类型的值（数字类型、字符串类型、布尔类型，函数类型等）

```js
var star = {
    name : 'pink',
    age : 18,
    sex : '男',
    sayHi : function(){
        alert('大家好啊~');
    }
};
// 多个属性或者方法中间用逗号隔开
// 方法冒号后面跟的是一个匿名函数
```

### 4.2.1 属性简写
ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
const foo = 'bar';
const baz = {foo};
baz // {foo: "bar"}

// 等同于
const baz = {foo: foo};
```

上面代码中，变量`foo`直接写在大括号里面。这时，属性名就是变量名, 属性值就是变量值。下面是另一个例子。

```js
function f(x, y) {
  return {x, y};
}

// 等同于

function f(x, y) {
  return {x: x, y: y};
}

f(1, 2) // Object {x: 1, y: 2}
```


### 4.2.2 方法简写
除了属性简写，方法也可以简写。

```js
const o = {
  method() {
    return "Hello!";
  }
};

// 等同于

const o = {
  method: function() {
    return "Hello!";
  }
};
```

### 4.2.3 例子

```js
let birth = '2000/01/01';

const Person = {

  name: '张三',

  //等同于birth: birth
  birth,

  // 等同于hello: function ()...
  hello() { console.log('我的名字是', this.name); }

};
```

这种写法用于函数的返回值，将会非常方便。

```js
function getPoint() {
  const x = 1;
  const y = 10;
  return {x, y};
}

getPoint()
// {x:1, y:10}
```



## 4.3 利用 new Object 创建对象
跟之前的 new Array() 原理一致：var 对象名 = new Object();

使用的格式：对象.属性 = 值
```js
var obj = new Object(); //创建了一个空的对象
obj.name = '张三丰';
obj.age = 18;
obj.sex = '男';
obj.sayHi = function() {
    console.log('hi~');
}

//1.我们是利用等号赋值的方法添加对象
//2.每个属性和方法之间用分号结束
console.log(obj.name);
console.log(obj['sex']);
obj.sayHi();

```

## 4.4 用 Object.create ()

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


## 4.5 利用构造函数创建对象 ( function 构造函数名() { } )
构造函数 ：是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与 new 运算符一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。

Eine Konstruktorfunktion in JavaScript wird verwendet, um Objekte mit denselben Eigenschaften oder Methoden zu erstellen. Sie wird mit dem Schlüsselwort new aufgerufen.

在 js 中，使用构造函数要时要注意以下两点：
- 构造函数用于创建某一类对象，其首字母要大写
- 构造函数要和 new 一起使用才有意义
- 构造函数名字首字母要大写
- 函数内的属性和方法前面需要添加 this ，表示当前对象的属性和方法。
- 构造函数中不需要 return 返回结果。
- 当我们创建对象的时候，必须用 new 来调用构造函数。

构造函数和对象
- 构造函数，如 Stars()，抽象了对象的公共部分，封装到了函数里面，它泛指某一大类（class）
- 创建对象，如 new Stars()，特指某一个，通过 new 关键字创建对象的过程我们也称为对象实例化


new关键字
new 在执行时会做四件事:
1. 在内存中创建一个新的空对象。
2. 让 this 指向这个新的对象。
3. 执行构造函数里面的代码，给这个新对象添加属性和方法
4. 返回这个新对象（所以构造函数里面不需要return）


```js
//构造函数的语法格式
function 构造函数名() {
    this.属性 = 值;
    this.方法 = function() {}
}
new 构造函数名();

// this: In einer Konstruktorfunktion verweist this auf das neue Objekt, das gerade erstellt wird. Jede Eigenschaft, die man mit this definiert, wird dem neuen Objekt hinzugefügt. 

```

```js

// noch einfacher
function Tree(type){
    this.type = type;
}

let oakTree = new Tree();
oakTree.type = "Oak";
console.log(oakTree);

```

```js
//1. 构造函数名字首字母要大写
//2. 构造函数不需要return就可以返回结果
//3. 调用构造函数必须使用 new
//4. 我们只要new Star() 调用函数就创建了一个对象
//5. 我们的属性和方法前面必须加this
function Star(uname,age,sex) {
    this.name = uname;
    this.age = age;
    this.sex = sex;
    this.sing = function(sang){
        console.log(sang);
    }
}
var ldh = new Star('刘德华',18,'男');
console.log(typeof ldh) // object对象，调用函数返回的是对象

console.log(ldh.name);
console.log(ldh['sex']);
ldh.sing('冰雨');
//把冰雨传给了sang

var zxy = new Star('张学友',19,'男');
```


---

![](image/Pasted%20image%2020241122223730.png)
Beispiel-Erklärung:
- Auto ist die Konstruktorfunktion.
- this.marke = marke bedeutet, dass das neue Objekt (z. B. auto1) die Eigenschaft (Schlüssel/key) marke mit dem übergebenen Wert (z. B. "BMW") erhält.
- Mit new Auto(...) wird ein neues Objekt erstellt, und this verweist in diesem Moment auf dieses Objekt.


### 4.5.1 Verwendung von Prototype für Klassenähnliche Konstrukte

```js
1 
let protoFlower = {
    showType(type){
        console.log(`I am a ${type}!`);
    }
};

// Konstruktor Funktion
function CreateFlower(type){
    let flower = Object.create(protoFlower);
    flower.type = type;
    return flower;
}

console.log(CreateFlower("Rose"));
console.log(CreateFlower("Tulip"));


```


# 5 object的property


## 5.1 object的property 的调用

- 对象里面的属性调用 (Punktnotation) : 对象.属性名 ，这个小点 . 就理解为“ 的 ”
- 对象里面属性的另一种调用方式 (Klammernotation) : 对象[‘属性名’]，注意方括号里面的属性必须加引号，我们后面会用
- 对象里面的方法调用：对象.方法名() ，注意这个方法名字后面一定加括号

变量、属性、函数、方法总结
- 变量：单独声明赋值，单独存在
- 属性：对象里面的变量称为属性，不需要声明，用来描述该对象的特征
- 函数：单独存在的，通过==“函数名()”==的方式就可以调用
- 方法：对象里面的函数称为方法，方法不需要声明，使用==“对象.方法名()”==的方式就可以调用，方法用来描述该对象的行为和功能。



```js

objektname.eigenschaftsname // Punktnotation
objekt['eigenschaftsname'] // Klammernotation

console.log(star.name)     // 调用名字属性
console.log(star['name'])  // 调用名字属性

myObject["name"] = "Alice"; // legel
myObject[name] = "Alice"; // legal
myObject.name = "Alice"; // legal, Alternative Schreibweise
myObject."name2" = "Alice"; // 这是不合法的语法。 在 JavaScript 中，属性访问不能直接使用 . 后跟引号的形式。
 

myObject[123] = "Zahl als Schlüssel"; // legel
myObject["12"] = "Zahl als Schlüssel"; // legel
myObject.1 = "Zahl als Schlüssel"; // Syntaxfehler, 不行 
myObject."1" = "Zahl als Schlüssel" // 这是不合法的语法。 在 JavaScript 中，属性访问不能直接使用 . 后跟引号的形式。


star.sayHi();              // 调用 sayHi 方法,注意，一定不要忘记带后面的括号
```



## 5.2 call some unknown property
```js
console.log(anyObject.living); // 返回 undefined
```


## 5.3 检查一个属性是否存在 
```js

//方法一
// check for a property
console.log("firstName" in anyObject); // 返回 true or false 

// 方法2 使用 hasOwnProperty()
let hasName = obj.hasOwnProperty('name'); 
console.log(hasName); // true

```


## 5.4 showing keys and values
```js
console.log(Object.keys(anyOtherObject));
console.log(Object.values(anyOtherObject));
```


## 5.5 遍历对象的属性


### 5.5.1 for...in 

Um über alle Key-Value-Paare eines Objekts zu iterieren, eignet sich die `for…in`-Schleife. Der `for...in `Loop wird verwendet, um über die enumerierbaren (aufzählbaren) Eigenschaften eines Objekts zu iterieren. Er durchläuft die Schlüssel (Property-Namen) eines Objekts.

- for...in 语句用于对数组或者对象的属性进行循环操作
- let item in 

语法中的变量是自定义的，它需要符合命名规范，通常我们会将这个变量写为 k 或者 key。

```js

js
for(变量 in 对象名字){
    // 在此执行代码
}


for(var k in obj) {
    console.log(k);		//这里的 k 是属性名
    console.log(obj[k]);//这里的 obj[k] 是属性值
}


var obj = {
    name: '秦sir',
    age: 18,
    sex: '男',
    fn:function() {};
};
console.log(obj.name);
console.log(obj.age);
console.log(obj.sex);

//for in 遍历我们的对象
//for (变量 in 对象){}
//我们使用for in 里面的变量 我们喜欢写k 或者key
for(var k in obj){
    console.log(k); // k 变量 输出得到的是属性名
    console.log(obj[k]); // obj[k] 得到的是属性值
}

```


```js
for (let item in anyObject){
    console.log(item+" : "+anyObject[item]);
}


const person = { name: "Alice", age: 25, city: "Berlin" };
for (let key in person) {
  console.log(key + ": " + person[key]);
}
// name: Alice
// age: 25 
// city: Berlin

```


property 为 array 类型
```js
(function init(){
	"use strict";

	// everything can be an object property

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

	// function(...a)
	// spreads arguments into real Array
	// https://www.mediaevent.de/javascript/spread-operator.html

	console.log(Object.values(person));
	console.log(person.age());
	
	console.log(person.hobbies);

	console.log('--------- for')
	for(let i=0; i<person.hobbies.length;i++){
		console.log(person.hobbies[i]);
	}

	console.log('--------- for..in')
	for(let item in person.hobbies){
		console.log(person.hobbies[item]);
	}

	console.log('--------- forEach')

	person.hobbies.forEach(element => {
		console.log(element);
	});

	person.hobbies.push("trinken");
	person.hobbies.forEach(element => console.log(element));
})();
```

### 5.5.2 `for...of`

The **`for...of`** statement executes a loop that operates on a sequence of values sourced from an [iterable object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol). Iterable objects include instances of built-ins such as [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array), [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray), [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map), [`Set`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set), [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) (and other DOM collections), as well as the [`arguments`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) object, [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator) produced by [generator functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*), and user-defined iterables.

```js
const array1 = ['a', 'b', 'c'];

for (const element of array1) {
  console.log(element);
}

// Expected output: "a"
// Expected output: "b"
// Expected output: "c"
```


## 5.6 添加删除 property

Der delete-Operator in JavaScript wird verwendet, um Eigenschaften aus Objekten zu entfernen. 

```js
anyObject.living = true; // 即使living 这个 attribute 之前不存在, 通过这个statement 也可以直接生成出来 这个 attribute 
console.log(anyObject);

delete anyObject.living;
console.log(anyObject.living);  // 返回 undefined

```







# 6 object 的 method
## 6.1 method can also be properties of objects

Funktionsdeklaration, die den neuen Objekten als Property hinzugefügt wird.

```js
//  Das Objekt computer wird mit seinen Eigenschaften und der Methode hochfahren() in Literal-Schreibweise angelegt. Die Methode hochfahren() wird aufgerufen.
var computer = { 
marke :  'Dell',
farbe : 'silber',
art : 'Laptop',
hochfahren: function () { alert('Herzlich Willkommen');}
};

computer.hochfahren();

```

```js
1 
anyObject.func = () => { return console.log("function as property of an object!") };

anyObject.func();
console.log(typeof anyObject.func);  // 返回值为 function

```

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

console.log(objOne);
console.log(objTwo);

objOne.showThis("my property");
objTwo.showThis("MY property!!");

```

## 6.2 concatenate objects

assign 或者 { ...obj, ...obj2 }

```js
let anyOtherObject = {};
Object.assign(anyOtherObject, anyObject);

let obj2 = { city: 'Berlin', country: 'Germany' };

let o = Object.assign(obj, obj2);
// mit assign()-Methode

let o = { ...obj, ...obj2 };
// mit dem Spread-Operator
```




# 7 Constructors

But, don't overuse Object() or Array(), there are some problems you should know of.
	1. Declare as expression. It's short and easy to read.
	2. Objects are mutable.
	3. Objects don't belong to a certain class
	4. There is delegation to other Constructors of the type object, which might surprise you!


## 7.1 Customized constructors

```js
function Vorlesung(title, description, seats) {
  this.title=title;
  this.description=description;
  this.seats=seats;
  this.readSeats=function() {
    console.log("Anzahl der Plätze: "+this.seats);
  };
  this.writeSeats=function(newNumber) {
    this.seats=newNumber;
  };
  this[5]="fünf";
};
```

```js
// 不需要提前 instantiate a object , like let webtech = new vorlesung("", "" , 0). 也不报错, 只是 webtech 中 seat 为 undefined 
let webtech = new Vorlesung("Webtechnologien", "Vorlesung für *informatiker*innen", 300);

webtech;


```



- Ein **_Konstruktor_** (**_constructor_**) ist eine Funktion, die ein Objekt mit bestimmten Eigenschaften erstellt
- Ein Konstruktor wird aufgerufen mit dem Schlüsselwort `**new**` gefolgt vom Namen des Konstruktors und den Werten der Eigenschaften als Argumente
- Durch `**new**` wird `**this**` innerhalb des Konstruktors auf das neue Objekt gesetzt
- `**this**` ist der Präfix für die Referenzierung lokaler Variablen, die dann zu den Eigenschaften des Objekts werden 
- Konvention: Konstruktorfunktionen sollten mit einem Großbuchstaben beginnen




Customized constructors instead of built-in-constructors!
```js
/*Declaration as Constructor*/
function Plant(leaves, color, species) {
    this.leaves = leaves;
    this.color = color;
    this.species = species;
    return console.log("I am a " + this.species + " and I am " + this.color + "!");
}

console.log(Plant); //try hoisting, 就是 使用 referenz 
// 返回值为 
/*
ƒ Plant(leaves, color, species) {
		this.leaves = leaves;
		this.color = color;
		this.species = species;
		return console.log("I am a " + this.species + " and I am " + this.color + "!");
	}
*/

```

sometimes better: using a function expression depends on if you need hoisting.
```js

	let PlantExpression = function (leaves, color, species) {
		this.leaves = leaves;
		this.color = color;
		this.species = species;
		return console.log("I am a " + species);
	};

console.log(PlantExpression);
// 返回值为 
/*
ƒ (leaves, color, species) {
		this.leaves = leaves;
		this.color = color;
		this.species = species;
		return console.log("I am a " + species);
	}
*/
```

Does it work with arrow functions? -> yes 可以用的 
在 arrow function 中 不要去使用 this, no arguments in arrow functions
```js
const PlantArrow = (leaves, color, species) => {
    this.leaves = leaves;
    this.color = color;
    this.species = species;
};

console.log(PlantArrow);

// 返回值为 
/*
(leaves, color, species) => {
		this.leaves = leaves;
		this.color = color;
		this.species = species;
	}
*/
```


### 7.1.1 使用上述的Customized constructors
```js
// defining objects
let tree = new Plant(10000, "green", "Tree");
let flower = new PlantExpression(5, "red", "Flower");

console.log(tree.leaves);
flower.color = "blue";
console.log(flower.color);
console.log(flower.constructor, typeof flower);

```

## 7.2 return 值
objects invoked with new always return an object usually this, but you can return any object

```js
/*constructor-function as function-expression*/
let ObjectMaker = function () {
    this.name = "This is it";
    // return;
    // return this;
    // let that={};
    // return that;
}

let o = new ObjectMaker();
console.log(o);  // ObjectMaker {name: 'This is it'}
//console.clear();
```


## 7.3 object 的constructors的 rules
- declare objects as literals whenever possible
- if using DOM-objects like <img>, use built-in-constructors
- sometimes you need a constructor 
    for similar objects : make your own constructor 
    function ConstruktorName(){};
    let o=new ConstruktorName();

## 7.4 打印object的constructor

```js
console.log(anyObject.constructor); // 返回值为 Object() { [native code] }
```


## 7.5 built in Constructors:
Object();
Array();
Function();
Number();
String();
Boolean();
RegEx()


```js
let obj = new Object();
console.log(obj);   // {}
console.log(obj.constructor);  // Object() { [native code] }
console.log(typeof obj); // object
```


### 7.5.1 i.e. in DOM:  Image()

```js
/*Use of built-in-constructors with browsers.*/

let sonneDOM = document.querySelector("img");
console.log(sonneDOM, typeof sonneDOM);

let sonne = new Image();
sonne.src = "pics/sonne.png";
console.log(sonne, typeof sonne);

console.log(sonneDOM.width, sonneDOM.height, sonneDOM.src, sonneDOM.alt, sonneDOM.title);
console.log(sonne.width, sonne.height, sonne.src, sonne.alt, sonne.title);
```

