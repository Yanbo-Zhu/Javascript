

ES17 kennt die neuen Schlüsselworte async und await. Damit werden eine Methode als asynchron deklariert und mit await die Auswertung eines sog. Promises in der asynchronen Methode abgewartet. Ein Promise ist ein Ausdruck, der erst zu einem späteren Zeitpunkt evaluiert wird. 

Promises und async/await sind zwei verschiedene Ansätze in JavaScript, um mit asynchronem Code umzugehen. Beide haben ihre Vor- und Nachteile und können je nach Anwendungsfall eingesetzt werden.


# 1 中文解释(重要 ) 

`async` 和 `await` 是用于 **异步编程** 的关键字，主要出现在 Python 和 JavaScript 中（语法相似，概念一致）。它们的主要作用是：**让代码以非阻塞的方式执行等待操作（如 I/O、网络请求、定时器等）**。

- `async`：用于声明一个“异步函数”。
    - - `async` 表示函数内部可能有异步操作，返回值会被自动包装成一个 `Promise`。
- `await`：等待一个异步操作完成（非阻塞）. 只能在 `async` 函数中使用，用于等待一个“异步操作”的结果，而不阻塞后面的代码执行。   ==阻塞的的意思 是 后面的测地不执行了== 
    - - `await` 用来等待一个 `Promise` 的完成，并“暂停”后面的代码，直到该 Promise 被 `resolve`。
    - 只是暂停 async 标识的 function 中 指令的运行 , 直到 await 的 promise 返回结果, 然后执行 await 的 zuweisung 的下一行 (在 同一个async function 中的)
    - 一个程序 有很多个 function , 很多thread.  只是 暂停某一个 function 的运行  不妨碍其他的 




## 1.1 例子   async function 之外的 directive 的执行先后

```
console.log("A");

setTimeout(() => console.log("B"), 0);

async function test() {
  await Promise.resolve();
  console.log("C");
}

test();

console.log("D");
```


输出顺序是 
```
A
D
C
B
```

为什么？因为：

1. `await Promise.resolve()` 会让出执行权（放入微任务队列）。
2. 所以 `D` 先执行，接着微任务队列中的 `C` 执行。
3. `B` 是宏任务（定时器），最后执行。


## 1.2 例子  async function 之内的 directive 的执行先后

await 只能在 async 函数中使用，用于等待一个 Promise 的完成，它会“暂停”当前函数的执行，直到异步操作完成（resolved/rejected），不会阻塞主线程。


- 它“暂停”的是当前 `async` 函数，而不是整个程序。
- 它只对返回 Promise 的表达式起作用。
- 后面的代码虽然**写在下面**，但实际上会被延后执行，直到当前 `await` 的 Promise 完成。

```js
async function fetchData() {
  console.log("1. 开始获取数据...");
  const data = await fetch('https://example.com'); // 等待 fetch 完成
  console.log("2. 数据获取完毕");
}
```


输出顺序 
```
1. 开始获取数据...
（等待网络请求）
2. 数据获取完毕
```

# 2 async/await Funktionen

Async/Await ist eine syntaktische Verbesserung für die Arbeit mit Promises, die es ermöglicht, asynchronen Code wie synchronen Code zu schreiben.



async markiert eine Funktion als asynchron und gibt implizit ein Promise zurück.

await pausiert die Ausführung, bis das Promise aufgelöst ist (fulfilled oder rejected).
Das await-Schlüsselwort in JavaScript wird verwendet, um die Ausführung der Funktion so lange anzuhalten, bis ein Promise aufgelöst wird. Es pausiert also die Ausführung der Funktion, ohne den gesamten Programmablauf zu blockieren. Funktionsweise von await: 

Warten auf ein Promise:
- Wenn das Promise aufgelöst wird, gibt await dessen Ergebnis zurück.
- Wird das Promise erfüllt, gibt await den Wert zurück.
- Wird das Promise abgelehnt, löst await einen Fehler aus, der mit try/catch behandelt werden kann.

Pausiert nicht-blockierend:
- Während await auf das Promise wartet, kann der JavaScript-Event-Loop andere Aufgaben ausführen.




## 2.1 Vorteil und Nachteil 



Vorteile von Async/Await:
• Einfachere Lesbarkeit: Asynchroner Code wirkt wie synchroner.
• Einfachere Fehlerbehandlung: Durch können Fehler sauber try/ catch abgefangen werden.
• Kompatibel mit Promises: await arbeitet direkt mit Promises.

Nachteile:
- Kann in Kombination mit mehreren await Operationen dazu führen, dass die Ausführung länger dauert, wenn die Promises nicht parallel ausgeführt werden.
- Muss in einer async Funktion verwendet werden, was Einschränkungen in manchen Kontexten mit sich bringt.

# 3 Wann welches verwenden?

• Verwenden Sie Promises, wenn:
o Sie mehrere asynchrone Operationen in parallelen Abläufen ausführen möchten.
o Eine reine Verkettung ohne komplexe Logik erforderlich ist.

• Verwenden Sie async/await, wenn:
o Der Code leichter lesbar und wartbar sein soll.
o Sie mit sequentiellen Operationen arbeiten, bei denen der Output einer Operation als Input für die nächste dient.


![](image/Pasted%20image%2020241204224556.png)


## 3.1 Beispiel eines Promises ohne async und await

Zuerst ein simples Beispiel eines Promises ohne async und await, das mit function* notiert wird:

```js
// Beispiel f. e. Generator (Basis für async und await), der ein Promise zurück gibt
// mit function*
function* meingenerator() {
    let a = 1;
    let b = 1;
    while (true) {
        // Fibo-Zahlen
        [a, b] = [b, a + b];
        yield a;
    }
}
```

yield wartet auf das Entgegennehmen des Wertes, hier den Inhalt der Variable 'a'. Mit next() wird von außen der aktuelle Wert abgeholt und blockiert (d.h. gewartet), solange er noch nicht da ist. Technisch gesprochen löst next() das mit yield getroffene Promise ein.

Zur Verwendung unseres neuen Generators etwas Code:

```js
// generierte Werte, das Feld 'done' im Wertepaar aus next() ist hier stets FALSCH,
// weil der Generator nicht terminiert
let gg = meingenerator();
gg.next().value; // 1
gg.next().value; // 2
gg.next().value; // 3
```

Generatoren können, wie hier in diesem Beispiel, unendlich laufen, oder aber auch endlich sein.

AUFGABE

Warum sollte man nicht meingenerator() selbst in den Aufrufen nutzen? Probieren Sie es.

---


Nun async und await zur Veranschaulichung, sie sind sog. 'syntaktischer Zucker' auf Promises, yield und next(), d.h. machen sie genießbarer:

```js
async function deferred() {
  let promise = new Promise((resolve, reject) =>
  {resolve(3 + 4);});
  document.writeln(promise);
  let myeval = await promise;
  document.writeln(myeval);
}
deferred();
```

Das angezeigte Ergebnis lautet [object Promise] 7. Ersteres ist das Promise (nicht evaluiert), letzteres ist das evaluierte Ergebnis aus dem Promise. reject() wird im Fehlerfall aufgerufen (im Beispiel nicht gezeigt).



## 3.2 async

`async`函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。


- Präfix `**async**` vor Funktionen zeigt an, dass die Funktion ein Promise als Rückgabeargument liefert
- Der Rückgabewert kann explizit als Promise deklariert werden, wird der Rückgabewert mit einem anderen Datentyp deklariert wird er automatisch in ein Promise eingepackt

```js
async function meineFunktion() {
  return new Promise(resolve=>resolve(1));
}

async function meineFunktion() {
  return 1;
}

async function meineFunktion() {
  console.log("nix");
}

meineFunktion().then(wert=>console.log("Ergebnis: "+wert));
```


```js
async function meineFunktion() {
  return new Promise(resolve=>resolve(1));
}

async function meineFunktion() {
  return 1;
}

async function meineFunktion() {
  console.log("nix");
}

meineFunktion().then(wert=>console.log("Ergebnis: "+wert));
```


## 3.3 await

- Präfix `**await**` vor einem Promise zeigt an, dass auf die Finalisierung des Promise gewartet wird
- Warten geschieht asynchron, d.h. die Event Loop erledigt zwischenzeitlich andere Aufgaben
-  `**await**` ==ersetzt zudem die Referenz auf das Promise durch das Promise-Ergebnis==
- `**await**` darf nur in `**async**`-Funktionen angewendet werden

```js
let meinPromise=()=>{
  return new Promise((resolve, reject)=> {
    setTimeout(()=> resolve("Ich wurde ausgelöst"), 3000);
  });
};

async function ohneAwait() {
  let wert=meinPromise();
  console.log("Ergebnis: "+wert);
};
ohneAwait();
// output
// Ergebnis: [object Promise]

async function mitAwait() {
  let wert=await meinPromise();
  console.log("Ergebnis: "+wert);
};
mitAwait();
// output
// Ergebnis: Ich wurde ausgelöst

```

# 4 例子 

下面是一个例子。

```js
async function getStockPriceByName(name) {
  const symbol = await getStockSymbol(name);
  const stockPrice = await getStockPrice(symbol);
  return stockPrice;
}

getStockPriceByName('goog').then(function (result) {
  console.log(result);
});
```

上面代码是一个获取股票报价的函数，函数前面的`async`关键字，表明该函数内部有异步操作。调用该函数时，会立即返回一个`Promise`对象。


---

下面是另一个例子，指定多少毫秒后输出一个值。

```js
function timeout(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint('hello world', 50);
```

上面代码指定 50 毫秒以后，输出`hello world`。

---

由于`async`函数返回的是 Promise 对象，可以作为`await`命令的参数。所以，上面的例子也可以写成下面的形式。

```js
async function timeout(ms) {
  await new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint('hello world', 50);
```

async 函数有多种使用形式。

```js
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)

// 箭头函数
const foo = async () => {};
```

# 5 语法

`async`函数的语法规则总体上比较简单，难点是错误处理机制。

```js
async function myFunction() {
  try {
    const result = await someAsyncOperation();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
myFunction();
```

## 5.1 Syntaxvergleich

promise
```js
fetch('https://fakestoreapi.com/products/1')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Fehler', error));
```

async/await: ist klarer und lesbarer, insbesondere bei komplexeren Abläufen.
```js
async function fetchData() {
  try {
    const response = await fetch('https://fakestoreapi.com/products/1');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
fetchData();
```

1. fetch( https : //fakestoreapi.com/products/l') : liefert ein Promise zurück.
2. await response.json() : wartet auf die Umwandlung der Antwort in JSON.
3. Das Programm geht erst weiter, wenn die Operationen abgeschlossen Sind.

---

Was passiert ohne await ?
Ohne await würde die Funktion den Promise sofort zurückgeben, und derWert wäre nicht direkt verfügbar. Mit await Wird das tatsächliche Ergebnis des Promises verwendet.

```js
async function fetchData() {
    const response = await fetch('https://fakestoreapi.com/products/1');
    const data = await response.json();
    console.log(data);
}
fetchData();
```

![](image/Pasted%20image%2020241204224838.png)

---

```js
async function fetchData() {
    const response = fetch('https://fakestoreapi.com/products/1');
    const data = response.json();
    console.log(data);
}
fetchData();
```

![](image/Pasted%20image%2020241204224859.png)


---

```js
async function fetchData() {
    const response = fetch('https://fakestoreapi.com/products/1');
    const data = await response.json();
    console.log(data);
}
fetchData();
```

![](image/Pasted%20image%2020241204225137.png)

## 5.2 返回 Promise 对象

`async`函数返回一个 Promise 对象。

`async`函数内部`return`语句返回的值，会成为`then`方法回调函数的参数。

```js
async function f() {
  return 'hello world';
}

f().then(v => console.log(v))
// "hello world"
```

上面代码中，函数`f`内部`return`命令返回的值，会被`then`方法回调函数接收到。

`async`函数内部抛出错误，会导致返回的 Promise 对象变为`reject`状态。抛出的错误对象会被`catch`方法回调函数接收到。

```js
async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log('resolve', v),
  e => console.log('reject', e)
)
//reject Error: 出错了
```

## 5.3 Promise 对象的状态变化

`async`函数返回的 Promise 对象，必须等到内部所有`await`命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到`return`语句或者抛出错误。也就是说，只有`async`函数内部的异步操作执行完，才会执行`then`方法指定的回调函数。

下面是一个例子。

```js
async function getTitle(url) {
  let response = await fetch(url);
  let html = await response.text();
  return html.match(/<title>([\s\S]+)<\/title>/i)[1];
}
getTitle('https://tc39.github.io/ecma262/').then(console.log)
// "ECMAScript 2017 Language Specification"
```

上面代码中，函数`getTitle`内部有三个操作：抓取网页、取出文本、匹配页面标题。只有这三个操作全部完成，才会执行`then`方法里面的`console.log`。

## 5.4 async联合await使用

正常情况下，`await`命令后面是一个 Promise 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

```js
async function f() {
  // 等同于
  // return 123;
  return await 123;
}

f().then(v => console.log(v))
// 123
```

上面代码中，`await`命令的参数是数值`123`，这时等同于`return 123`。

这个例子还演示了如何实现休眠效果。JavaScript 一直没有休眠的语法，但是借助`await`命令就可以让程序停顿指定的时间。下面给出了一个简化的`sleep`实现。

```js
function sleep(interval) {
  return new Promise(resolve => {
    setTimeout(resolve, interval);
  })
}

// 用法
async function one2FiveInAsync() {
  for(let i = 1; i <= 5; i++) {
    console.log(i);
    await sleep(1000);
  }
}

one2FiveInAsync();
```

`await`命令后面的 Promise 对象如果变为`reject`状态，则`reject`的参数会被`catch`方法的回调函数接收到。

```js
async function f() {
  await Promise.reject('出错了');
}

f()
.then(v => console.log(v))
.catch(e => console.log(e))
// 出错了
```

注意，上面代码中，`await`语句前面没有`return`，但是`reject`方法的参数依然传入了`catch`方法的回调函数。这里如果在`await`前面加上`return`，效果是一样的。

任何一个`await`语句后面的 Promise 对象变为`reject`状态，那么整个`async`函数都会中断执行。

```js
async function f() {
  await Promise.reject('出错了');
  await Promise.resolve('hello world'); // 不会执行
}
```

上面代码中，第二个`await`语句是不会执行的，因为第一个`await`语句状态变成了`reject`。

有时，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个`await`放在`try...catch`结构里面，这样不管这个异步操作是否成功，第二个`await`都会执行。

```js
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
  }
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// hello world
```

另一种方法是`await`后面的 Promise 对象再跟一个`catch`方法，处理前面可能出现的错误。

```js
async function f() {
  await Promise.reject('出错了')
    .catch(e => console.log(e));
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// 出错了
// hello world
```

## 5.5 错误处理

如果`await`后面的异步操作出错，那么等同于`async`函数返回的 Promise 对象被`reject`。

```js
async function f() {
  await new Promise(function (resolve, reject) {
    throw new Error('出错了');
  });
}

f()
.then(v => console.log(v))
.catch(e => console.log(e))
// Error：出错了
```

上面代码中，`async`函数`f`执行后，`await`后面的 Promise 对象会抛出一个错误对象，导致`catch`方法的回调函数被调用，它的参数就是抛出的错误对象。

防止出错的方法，也是将其放在`try...catch`代码块之中。

```js
async function f() {
  try {
    await new Promise(function (resolve, reject) {
      throw new Error('出错了');
    });
  } catch(e) {
  }
  return await('hello world');
}
```

如果有多个`await`命令，可以统一放在`try...catch`结构中。

```js
async function main() {
  try {
    const val1 = await firstStep();
    const val2 = await secondStep(val1);
    const val3 = await thirdStep(val1, val2);

    console.log('Final: ', val3);
  }
  catch (err) {
    console.error(err);
  }
}
```

下面的例子使用`try...catch`结构，实现多次重复尝试。

```js
const superagent = require('superagent');
const NUM_RETRIES = 3;

async function test() {
  let i;
  for (i = 0; i < NUM_RETRIES; ++i) {
    try {
      await superagent.get('http://google.com/this-throws-an-error');
      break;
    } catch(err) {}
  }
  console.log(i); // 3
}

test();
```

上面代码中，如果`await`操作成功，就会使用`break`语句退出循环；如果失败，会被`catch`语句捕捉，然后进入下一轮循环。

# 6 使用注意点 

## 6.1 `await`命令后面的`Promise`对象，运行结果可能是`rejected`，所以最好把`await`命令放在`try...catch`代码块中。

```js
async function myFunction() {
  try {
    await somethingThatReturnsAPromise();
  } catch (err) {
    console.log(err);
  }
}

// 另一种写法

async function myFunction() {
  await somethingThatReturnsAPromise()
  .catch(function (err) {
    console.log(err);
  });
}
```

## 6.2 多个`await`命令后面的异步操作，如果不存在继发关系，最好让它们同时触发。

```js
let foo = await getFoo();
let bar = await getBar();
```

上面代码中，`getFoo`和`getBar`是两个独立的异步操作（即互不依赖），被写成继发关系。这样比较耗时，因为只有`getFoo`完成以后，才会执行`getBar`，完全可以让它们同时触发。

```js
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```

上面两种写法，`getFoo`和`getBar`都是同时触发，这样就会缩短程序的执行时间。

## 6.3 `await`命令只能用在`async`函数之中，如果用在普通函数，就会报错。

```js
async function dbFuc(db) {
  let docs = [{}, {}, {}];

  // 报错
  docs.forEach(function (doc) {
    await db.post(doc);
  });
}
```

上面代码会报错，因为`await`用在普通函数之中了。但是，如果将`forEach`方法的参数改成`async`函数，也有问题。

```js
function dbFuc(db) { //这里不需要 async
  let docs = [{}, {}, {}];

  // 可能得到错误结果
  docs.forEach(async function (doc) {
    await db.post(doc);
  });
}
```

上面代码可能不会正常工作，原因是这时三个`db.post()`操作将是并发执行，也就是同时执行，而不是继发执行。正确的写法是采用`for`循环。

```js
async function dbFuc(db) {
  let docs = [{}, {}, {}];

  for (let doc of docs) {
    await db.post(doc);
  }
}
```


---


另一种方法是使用数组的`reduce()`方法。

```js
async function dbFuc(db) {
  let docs = [{}, {}, {}];

  await docs.reduce(async (_, doc) => {
    await _;
    await db.post(doc);
  }, undefined);
}
```

上面例子中，`reduce()`方法的第一个参数是`async`函数，导致该函数的第一个参数是前一步操作返回的 Promise 对象，所以必须使用`await`等待它操作结束。另外，`reduce()`方法返回的是`docs`数组最后一个成员的`async`函数的执行结果，也是一个 Promise 对象，导致在它前面也必须加上`await`。

上面的`reduce()`的参数函数里面没有`return`语句，原因是这个函数的主要目的是`db.post()`操作，不是返回值。而且`async`函数不管有没有`return`语句，总是返回一个 Promise 对象，所以这里的`return`是不必要的。

如果确实希望多个请求并发执行，可以使用`Promise.all`方法。当三个请求都会`resolved`时，下面两种写法效果相同。

```js
async function dbFuc(db) {
  let docs = [{}, {}, {}];
  let promises = docs.map((doc) => db.post(doc));

  let results = await Promise.all(promises);
  console.log(results);
}

// 或者使用下面的写法

async function dbFuc(db) {
  let docs = [{}, {}, {}];
  let promises = docs.map((doc) => db.post(doc));

  let results = [];
  for (let promise of promises) {
    results.push(await promise);
  }
  console.log(results);
}
```




## 6.4 async 函数可以保留运行堆栈。

```js
const a = () => {
  b().then(() => c());
};
```

上面代码中，函数`a`内部运行了一个异步任务`b()`。当`b()`运行的时候，函数`a()`不会中断，而是继续执行。等到`b()`运行结束，可能`a()`早就运行结束了，`b()`所在的上下文环境已经消失了。如果`b()`或`c()`报错，错误堆栈将不包括`a()`。

现在将这个例子改成`async`函数。

```
const a = async () => {
  await b();
  c();
};
```

上面代码中，`b()`运行的时候，`a()`是暂停执行，上下文环境都保存着。一旦`b()`或`c()`报错，错误堆栈将包括`a()`。

# 7 es13新增

在 JavaScript 中，await 运算符用于暂停执行，直到 Promise 被解决（履行或拒绝）。以前，我们只能在 async 函数中使用此运算符 - 使用 async 关键字声明的函数。我们无法在全球范围内这样做。

```js
function setTimeoutAsync(timeout) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, timeout);
  });
}
// SyntaxError: await is only valid in async functions
await setTimeoutAsync(3000);
```

使用 ES13，现在我们可以：

```js
function setTimeoutAsync(timeout) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, timeout);
  });
}
// Waits for timeout - no error thrown
await setTimeoutAsync(3000);
```