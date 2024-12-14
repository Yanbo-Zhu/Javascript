

Promise 是异步操作的一种解决方案。
Promise是ES6引入的异步编程（回调地狱）的新解决方案。语法上Promise是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。

# 1 基础 

“Promises (in anderen Programmiersprachen auch Futures genannt) sind ein sehr nützliches Werkzeug für die asynchrone Programmierung mit JavaScript. Sie repräsentieren Platzhalter für Ergebnisse, die erst in der Zukunft eintreffen. Indem man den Promises Callback-Funktionen übergibt, kann man Funktionalität definieren, die asynchron ausgeführt wird, also erst dann, wenn das Ergebnis vorliegt.”

就是将 function 的具体内容, 就是在之前某一个function 中写下这个 function 作为 placeholder,  之后再定义这个function , 在给入这个function具体要干什么 

In JavaScript sind _Promises_ ein Konzept, das dazu dient, **asynchrone** Operationen auf eine einfache und gut lesbare Weise zu behandeln. Ein Promise repräsentiert den zukünftigen Wert einer asynchronen Operation – entweder den Erfolg oder das Scheitern.

Promises helfen, das sogenannte "Callback Hell" zu vermeiden – ein häufiges Problem, wenn man viele verschachtelte Callback-Funktionen verwendet. Sie verbessern die Lesbarkeit und Strukturierung von asynchronem Code und machen Fehlerbehandlung einfacher.

## 1.1 Was ist eine Callback-Funktion


Eine Callback-Funktion in JavaScript ist eine Funktion, die als Argument an eine andere Funktion übergeben wird und in dieser aufgerufen wird, um eine bestimmte Aktion auszuführen.


```js
function sayHello(name) {
    console.log(`Hello, ${name}!`);
}

function greetUser(callback, userName) {
    console.log("Fetching user information...");
    setTimeout(() => {
        // Aufruf der Callback-Funktion nach 2 Sekunden
        callback(userName);
    }, 2000);
}

// Die Funktion sayHello wird als Callback übergeben
greetUser(sayHello, "Szymon");

```


![](image/Pasted%20image%2020241204222416.png)

## 1.2 Sind Callback-Funktionen also Funktionen höherer Ordnung?

Nein

- Eine Callback-Funktion ist eine Funktion, die von einer anderen Funktion verwendet wird.
- Funktionen höherer Ordnung sind Funktionen, die entweder andere Funktionen akzeptieren (z. B. Array.map) oder Funktionen zurückgeben.
- Eine Funktion höherer Ordnung verwendet oft Callback-Funktionen. Zum Beispiel ist Array.map eine Funktion höherer Ordnung, die einen Callback akzeptiert:

```js
[1, 2, 3].map(x => x * 2); 
// Die Lambda-Funktion `x => x * 2` ist ein Callback.
```

---

**Callback-Funktionen:**

Eine Callback-Funktion ist eine Funktion, die als Argument an eine andere Funktion **übergeben** **wird**, um später innerhalb dieser aufgerufen zu werden. Callbacks ****selbst sind also **keine** Funktionen höherer Ordnung – sie sind oft normale Funktionen, die von einer höheren Ordnungs-Funktion verwendet werden.

```js
function callbackExample(callback) {
    console.log("Before calling the callback...");
    callback(); // Aufruf der übergebenen Funktion
    console.log("After calling the callback...");
}

function myCallback() {
    console.log("This is a callback function.");
}

callbackExample(myCallback);
```

Hier ist myCallback eine normale Funktion, die als Callback verwendet wird. Sie selbst ist keine Funktion höherer Ordnung.

---


**Funktionen höherer Ordnung:**

Eine Funktion höherer Ordnung ist eine Funktion, die entweder:
Eine andere Funktion als Argument akzeptiert (wie callbackExample rechts), oder Eine Funktion zurückgibt.

```js
function higherOrderFunction() {
    return function () {
        console.log("This is a returned function.");
    };
}

// Aufruf der HOF
const returnedFunction = higherOrderFunction();
returnedFunction(); // Gibt "This is a returned function." aus

```

Hier ist higherOrderFunction eine Funktion höherer Ordnung, da sie eine Funktion zurückgibt.

# 2 什么时候使用 Promise 呢: 回调地狱 callback hell

Promise 一般用来解决层层嵌套的回调函数（回调地狱 callback hell）的问题。
Als Callback-Hölle (Callback Hell) werden mehrere ineinander verschachtelte Callbacks bezeichnet, deren Code nur noch sehr schwer nachvollziehbar ist

```js
function x(callback) {
  setTimeout(function() {
    console.log("Ergebnis von x()");
    callback();
  }, 2000);
};
function y(callback) {
  setTimeout(function() {
    console.log("Ergebnis von y()");
    callback();
  }, 1000);
};
function z(callback) {
  setTimeout(function() {
    console.log("Ergebnis von z()");
    callback();
  }, 3000);
};

x(()=>{
  console.log("x() ist fertig");
  y(()=>{
   console.log("y() ist fertig");
   z(()=>{
    console.log("z() ist fertig");
   });
  });
});
```


## 2.1 例子1：分别间隔一秒打印省市县

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>回调举例</title>
</head>

<body>
<script>
    /*
    // 此种方式，省市县都会在一秒后同时打印，没有实现要求
    setTimeout(() => {
        console.log("云南省");
    }, 1000);
    setTimeout(() => {
        console.log("玉溪市");
    }, 1000);
    setTimeout(() => {
        console.log("峨山县");
    }, 1000);
    */

    // 通过回调函数的方式，实现异步
    setTimeout(() => {
        console.log("云南省");
        let str01 = "云南省";
        setTimeout(() => {
            console.log(str01 + "玉溪市");
            let str02 = "云南省玉溪市";
            setTimeout(() => {
                console.log(str02 + "峨山县");
            }, 1000, str02);
        }, 1000, str01);
    }, 1000);
    console.log("通过回调函数的方式，实现异步");
</script>
</body>

</html>
```

![555](https://i0.hdslb.com/bfs/album/a45ebe3c65367ca98ec1e4932a40f978cae5e818.gif)

## 2.2 例子2：当我们点击窗口后，盒子依次 “右——>下——>左” 移动

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <title>Promise</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        #box {
            width: 300px;
            height: 300px;
            background-color: red;
            transition: all 0.5s;
        }
    </style>
</head>
<body>
<div id="box"></div>
<script>    
    // 运动函数
    const move = (el, {x = 0, y = 0} = {}, end = () => {}) => {
        el.style.transform = `translate3d(${x}px, ${y}px, 0)`;
        el.addEventListener(
            // transitionend 事件在 CSS 完成过渡后触发。
            'transitionend',
            () => {
                end();
            },
            false
        );
    };

    const boxEl = document.getElementById('box');

    // 形成回调地狱
    document.addEventListener(
        'click',
        () => {
            move(boxEl, {x: 150}, () => {
                move(boxEl, {x: 150, y: 150}, () => {
                    move(boxEl, {y: 150}, () => {
                        move(boxEl, {x: 0, y: 0});
                    });
                });
            });
        },
        false
    );
</script>
</body>
</html>
```

<img src="https://i0.hdslb.com/bfs/album/97e97a5e20c5634615ea020b9840ef838d9c0718.gif" style="zoom:25%;" />



# 3 Promise 的含义

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了`Promise`对象。

所谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

Promise 有三个状态：pending（等待）、fulfilled 或 resolved（成功）、rejected（失败）。

Ein Promise hat drei mögliche Zustände:
1. Pending (ausstehend): Das Promise wurde erstellt, die Operation ist aber noch nicht abgeschlossen.
2. Fulfilled (erfüllt): Die Operation wurde erfolgreich abgeschlossen, und das Promise hat nun einen Wert.
3. Rejected (abgelehnt): Die Operation ist fehlgeschlagen, und das Promise hat einen Fehlerwert.

---


并且 Promise 必须接收一个回调函数，这个回调函数有两个参数，这两个参数也是两个函数，`(resolve, reject) => {}`。
- 实例化 Promise 后，默认是等待状态。
- 当执行 `resolve()` 函数时，Promise 从等待状态——>成功状态。
- 当执行 `reject()` 函数时，Promise 从等待状态——>失败状态。

注意：当 Promise 的状态一但从等待转变为某一个状态后，后续的转变就自动忽略了，比如：先调用 `resolve()` 再调用 `reject()`，那么 Promise 的最终结果是成功状态。

> 注意：这里的 resolve reject 只是一个形参，可以取任意名字，但是我们约定直接使用 resolve reject。

注意，为了行文方便，本章后面的`resolved`统一只指`fulfilled`状态，不包含`rejected`状态。

有了`Promise`对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，`Promise`对象提供统一的接口，使得控制异步操作更加容易。



---

Vorteile von Promises:
- Ermöglichen Chaining mit .then() und .catch().
- Bessere Lesbarkeit und Fehlerbehandlung im Vergleich zu Callbacks.
- Unterstützt Funktionen wie Promise.all() oder Promise.race().

Nachteile von Promises:
- Verschachtelung kann bei komplexen Operationen zu schlechter Lesbarkeit führen.
- Fehlende native Syntax-Unterstützung für strukturiertes Warten.

`Promise`也有一些缺点。
- 首先，无法取消`Promise`，一旦新建它就会立即执行，无法中途取消。
- 其次，如果不设置回调函数，`Promise`内部抛出的错误，不会反应到外部。
- 第三，当处于`pending`状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

# 4 Promise 的基本用法和沟槽函数

ES6 规定，`Promise`对象是一个构造函数，用来生成`Promise`实例。


![](image/Pasted%20image%2020241129201322.png)

- Ein **_Promise_** ist ein "Versprechen" welches in Zukunft entweder erfüllt (**_fulfilled_**) oder nicht eingehalten (**_rejected_**) wird
- Promises sind Objekte, an die beim Aufruf ihres Konstruktors eine **_Ausführungsfunktion_** (**_Executor Function_**) übergeben wird
- Ausführungsfunktion wird synchron bei Instanziierung des Promise ausgeführt, definiert aber i.d.R. asynchronen Code in Form von Callbacks, die an Funktionen höherer Ordnung, z.B. Web APIs, übergeben werden
- Ausführungsfunktion endet mit Aufruf von `**resolve**` und Übergabe eines Ergebnisobjekts oder/und mit `**reject**` und Übergabe eines Fehlerobjekts
- Das vom Konstruktor erzeugte Promise-Objekt enthält eine `**then**`-Methode, welcher als Argument eine **_Konsumfunktion_** (**_Consumer Function_**) für den Erfolgsfall und eine für den Fehlerfall übergeben wird
- Konsumfunktionen werden in eine Job Queue im Erfolgsfall bzw. Fehlerfall aufgenommen und von der Event Loop mit dem Ergebnis- bzw. Fehlerobjekt aufgerufen

## 4.1 Promise构造函数：Promise(excutor){}
下面代码创造了一个`Promise`实例。
```js
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

`Promise`构造函数接受一个函数作为参数，该函数的两个参数分别是`resolve`和`reject`。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

- `resolve`函数的作用是，将`Promise`对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
    - resolve(value);  中 的value 就是 异步操作的结果 会被传递出去
- `reject`函数的作用是，将`Promise`对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

`resolve()` 和 `reject()` 函数是可以接收参数的。比如上面的  resolve(value); 中的 value 就是 `resolve()`接受到的参数 
- `resolve()` 接收的参数会传递给 then 方法的第一个回调函数
- `reject()` 接收的参数会传递给 then 方法的第二个回调函数

注意：通常我们不仅仅会传递一个基本数据类型的值，我们还常常传递对象，比如再 reject 中传递一个错误对象：
`reject(new Error("出错了！"));`


---

Ein Promise wird normalerweise durch das Erstellen einer neuen Instanz des Promise-Objekts initialisiert, wobei eine Callback-Funktion verwendet wird, die zwei Parameter hat: resolve und reject.
resolve und reject sind Funktionen, die von JavaScript automatisch an die Funktion übergeben werden, die man beim Erstellen eines Promises mit new Promise() angibt.

1. resolve wird verwendet, um das Promise als erfolgreich zu markieren.
    1. Das übergebene Argument wird an die .then() Methode weitergegeben.
2. reject wird verwendet, um das Promise als abgelehnt zu markieren.
    1. Das übergebene Argument wird an die .catch() Methode weitergegeben.

---

```js
let myPromise = new Promise((resolve, reject) => {
    let success = true;
    if (success) {
        resolve("Erfolg!"); // wird aufgerufen, wenn die Operation erfolgreich ist
    } else {
        reject("Fehler!"); // wird aufgerufen, wenn die Operation fehlschlägt
    }
});
```


## 4.2 `then`方法分别指定`resolved`状态和`rejected`状态的回调函数


`Promise`实例生成以后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回调函数。


```js

const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});


promise.then(
    function(value) { }, // success  
    function(error) { } // failure
);

```

`then`方法可以接受两个回调函数作为参数。第一个回调函数是`Promise`对象的状态变为`resolved`时调用，第二个回调函数是`Promise`对象的状态变为`rejected`时调用。

这两个函数都是可选的，不一定要提供。它们都接受`Promise`对象传出的值作为参数。

`resolve()` 和 `reject()` 函数是可以接收参数的。比如上面的  resolve(value); 中的 value 就是 `resolve()`接受到的参数 
- `resolve()` 接收的参数会传递给 then 方法的第一个回调函数
- `reject()` 接收的参数会传递给 then 方法的第二个回调函数

注意：通常我们不仅仅会传递一个基本数据类型的值，我们还常常传递对象，比如再 reject 中传递一个错误对象：
`reject(new Error("出错了！"));`


---

Promise-Methoden: .then(), .catch() und .finally()

1
then(): Diese Methode wird aufgerufen, wenn das Promise erfüllt ist und erlaubt den Zugriff auf das Ergebnis.
```js
myPromise.then(result => {
    console.log(result); // Ausgabe: Erfolg!
});
```

2
catch(): Diese Methode fängt Fehler ab und wird aufgerufen, wenn das Promise abgelehnt wird.
```js
myPromise.catch(error => {
    console.log(error); // Ausgabe: Fehler! (wenn success = false wäre)
});
```

3
finally(): Diese Methode wird unabhängig vom Erfolg oder Misserfolg der Operation ausgeführt und wird häufig für Bereinigungsaktionen genutzt.

```js
myPromise.finally(() => {
    console.log("Promise abgeschlossen");
});
```


4
```js
let myPromise = new Promise((resolve, reject) => {
    let success = true;
    if (success) {
        resolve("Erfolg!");
    } else {
        reject("Fehler!");
    }
})
.then(result => {
    console.log(result);
})
.catch(error => {
    console.log(error);
})
.finally(() => {
    console.log("Promise abgeschlossen");
});
```

## 4.3 DER PROMISE-LIFE-CYCLE


![](image/Pasted%20image%2020241129201353.png)

Zustände des Promise-Objekts
- `**pending**`: initialer Zustand, Ausführungsfunktion noch nicht abgeschlossen
- `**fulfilled**`: Ausführungsfunktion wurde erfolgreich abgeschlossen
- `**rejected**`: Ausführungsfunktion ist gescheitert
- `**settled**`: Ausführungsfunktion mit fulfilled oder rejected beendet
- Konsumfunktion im Fehlerfalle kann alternativ auch der `**catch**`-Methode übergeben werden (anstelle als zweites Argument in `**then**`), optional
- An `**finally**` übergebene Callbacks werden unabhängig von `**fulfilled**` und `**rejected**` ausgeführt und sind keine Konsumfunktionen, das sie keine Argumente haben



## 4.4 例子 

例子 
![](image/Pasted%20image%2020241129172805.png)

```js

let p=new Promise(function(resolve, reject) {
  setTimeout(()=>resolve("Fertig! hier ist das Ergebnis"), 3000);  // 过3s 后 执行 resolve("Fertig! hier ist das Ergebnis")
}).then(
  result=>console.log(result), // 从 resolve("Fertig! hier ist das Ergebnis") 中获取 "Fertig! hier ist das Ergebnis" 作为 result 的值 
  error=>console.log(error)
).finally(()=>console.log("Bearbeitung beendet")); 



let p=new Promise(function(resolve, reject) {
  setTimeout(()=>reject(new Error("Fertig! hier ist der Fehler")), 3000);
}).then(
  result=>console.log(result),
  error=>console.log(error)
).finally(()=>console.log("Bearbeitung beendet")); 

```





---


例子1
下面是一个`Promise`对象的简单例子。

```js
function timeout(ms) {
  return new Promise( (resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(5000).then(
    (value) => { console.log(value); } // 这个回调函数是`Promise`对象的状态变为`resolved`时调用，
);

```

或者写为

```js
function timeout(ms) {
  return new Promise( (resolve, reject) => {
    setTimeout(resolve("test"), ms);
  });
}

timeout(5000).then(
    (value) => { console.log(value); } // 这个回调函数是`Promise`对象的状态变为`resolved`时调用，
);
```

上面代码中，`timeout`方法返回一个`Promise`实例，表示一段时间以后才会发生的结果。过了指定的时间（`ms`参数）以后，`Promise`实例的状态变为`resolved`，就会触发`then`方法绑定的回调函数。


----
例子2 

Promise 新建后就会立即执行。

```js
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```

上面代码中，Promise 新建后立即执行，所以首先输出的是`Promise`。然后，`then`方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以`resolved`最后输出。


---
例子3 

下面是异步加载图片的例子。

```js
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    const image = new Image();

    image.onload = function() {
      resolve(image);
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };

    image.src = url;
  });
}
```

上面代码中，使用`Promise`包装了一个图片加载的异步操作。如果加载成功，就调用`resolve`方法，否则就调用`reject`方法。



---
例子4 

如果调用`resolve`函数和`reject`函数时带有参数，那么它们的参数会被传递给回调函数。`reject`函数的参数通常是`Error`对象的实例，表示抛出的错误；`resolve`函数的参数除了正常的值以外，还可能是另一个 Promise 实例，比如像下面这样。

```js
const p1 = new Promise(function (resolve, reject) {
  // ...
});

const p2 = new Promise(function (resolve, reject) {
  // ...
  resolve(p1);
})
```

上面代码中，`p1`和`p2`都是 Promise 的实例，但是`p2`的`resolve`方法将`p1`作为参数，即一个异步操作的结果是返回另一个异步操作。

注意，这时`p1`的状态就会传递给`p2`，也就是说，`p1`的状态决定了`p2`的状态。如果`p1`的状态是`pending`，那么`p2`的回调函数就会等待`p1`的状态改变；如果`p1`的状态已经是`resolved`或者`rejected`，那么`p2`的回调函数将会立刻执行。


---

```js
const p1 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error('fail')), 3000)
})

const p2 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve(p1), 1000)
})

p2
  .then(result => console.log(result))
  .catch(error => console.log(error))
// Error: fail
```

上面代码中，`p1`是一个 Promise，3 秒之后变为`rejected`。`p2`的状态在 1 秒之后改变，`resolve`方法返回的是`p1`。由于`p2`返回的是另一个 Promise，导致`p2`自己的状态无效了，由`p1`的状态决定`p2`的状态。所以，后面的`then`语句都变成针对后者（`p1`）。又过了 2 秒，`p1`变为`rejected`，导致触发`catch`方法指定的回调函数。


---

例子5 

注意，调用`resolve`或`reject`并不会终结 Promise 的参数函数的执行。

```js
new Promise((resolve, reject) => {
  resolve(1);
  console.log(2);
}).then(r => {
  console.log(r);
});
// 2
// 1
```

上面代码中，调用`resolve(1)`以后，后面的`console.log(2)`还是会执行，并且会首先打印出来。这是因为立即 resolved 的 Promise 是在本轮事件循环的末尾执行，总是晚于本轮循环的同步任务。

一般来说，调用`resolve`或`reject`以后，Promise 的使命就完成了，后继操作应该放到`then`方法里面，而不应该直接写在`resolve`或`reject`的后面。所以，最好在它们前面加上`return`语句，这样就不会有意外。

```js
new Promise((resolve, reject) => {
  return resolve(1);
  // 后面的语句不会执行
  console.log(2);
})
```



### 4.4.1 

```js
// mit Promise-Methoden

let myPromise = new Promise( (resolve, reject) => {
    console.log("The game has started.");
    setTimeout(() => {
        if (Math.random() < 0.1) {
            resolve("You won! Congratulations!")
        } else {
            reject("You lost. Try again!")
        }
    }, 2_000)
})
.then(win => console.log(win)) // success condition
.catch(lose => console.log(lose)) // reject condition oder error
.finally(() => console.log("Thanks for playing!"))
```



```js
// mit async/await

async function playGame() {
    console.log("The game has started.");
    try {
        const result = await new Promise((resolve, reject) => {
            setTimeout(() => {
                if (Math.random() < 0.1) {
                    resolve("You won! Congratulations!");
                } else {
                    reject("You lost. Try again!");
                }
            }, 2_000);
        });
        console.log(result); // success condition
    } catch (error) {
        console.log(error); // reject condition oder error
    } finally {
        console.log("Thanks for playing!");
    }
}
playGame();
```



# 5 Chained Promises (多个 then, catch, finally )


```js
let myPromise=new Promise((resolve, reject)=> {
  setTimeout(()=> {
    resolve("Immer");
  }, 3000)
}).then(wert=>wert+" und immer")
  .then(wert=>wert+" und immer wieder")
  .then(wert=>wert+" wiederhole ich mich.")
  .then(wert=>console.log(wert))
  .then(wert=>{throw new Error("Achtung Fehler")})
  .catch(err=>console.error(err));
```


- `**then**`, `**catch**` und `**finally**` geben nach Beendigung ein neues Promise-Objekt zurück, wodurch **_verkettete Promises_** (**_Chained Promises_**) möglich werden
- Konsumfunktionen in verketteten `**then**`-Methoden werden in der vorgegebenen Reihenfolge asynchron abgearbeitet
- Wird in einer der Konsumfunktionen ein Fehler ausgelöst, wird `**then**`-Kette abgebrochen und der Fehler optional durch eine an `**catch**` übergebene Konsumfunktion behandelt


## 5.1 ##

```js
let myPromise = new Promise( (resolve, reject) => {
    console.log("The game has started.");
    setTimeout(() => {
        if (Math.random() < 0.1) {
            resolve("You won! Congratulations!")
        } else {
            reject("You lost. Try again!")
        }
    }, 2_000)
})
.then(win => console.log(win)) // success condition
.catch(lose => console.log(lose)) // reject condition oder error
.then(win => console.log(win)) // success condition
.finally(() => console.log("Thanks for playing!"))
```


Code Walkthrough:

1. **Creating the `Promise`**:
    - The `Promise` is created, and the executor function is immediately executed.
    - The message `"The game has started."` is logged to the console.
2. **Timeout Logic**:
    - After 2 seconds (`setTimeout`), the `Math.random()` generates a random number between 0 and 1:
        - If the number is less than `0.1` (10% chance), the promise is **resolved** with `"You won! Congratulations!"`.
        - Otherwise, the promise is **rejected** with `"You lost. Try again!"`.
3. **Chaining with `then`, `catch`, `finally`**:
    - The `.then()` handler is called when the promise is **resolved**:
        - It logs `"You won! Congratulations!"` to the console.
    - The `.catch()` handler is called when the promise is **rejected**:
        - It logs `"You lost. Try again!"` to the console.
4. **Second `.then()`**:
    - Regardless of the outcome (resolved or rejected), the second `.then()` runs.
    - ==Since the `catch` block doesn't return a value, the `win` parameter in this `.then()` will be `undefined`. Thus, `console.log(win)` logs `undefined` unless the promise was resolved.==
5. **`.finally()`**:
    - Runs after the promise settles (whether resolved or rejected).
    - Logs `"Thanks for playing!"` to the console.



---

Possible Outputs:
Case 1: Random number is less than `0.1` (Promise is resolved):
```js
The game has started.
You won! Congratulations!
You won! Congratulations!
Thanks for playing!

```

Case 2: Random number is greater than or equal to 0.1 (Promise is rejected):
```js
The game has started.
You lost. Try again!
undefined
Thanks for playing!
```


---

Explanation of `undefined` in the Second `.then()`:
- The second `.then()` follows the `catch()` block, which doesn't return a value. As a result:
    - If the promise is resolved, the original resolution value propagates to the second `.then()`.
    - If the promise is rejected, `catch()` intercepts the rejection but doesn't pass any value to the next `.then()`.

To avoid undefined, return a value explicitly in the catch block, like:
```js
.catch(lose => {
    console.log(lose);
    return "Better luck next time!";
})
```

Now the second .then() will log "Better luck next time!" instead of undefined after a rejection.



# 6 方法
## 6.1 Promise.prototype.then()

### 6.1.1 Promise的基本结构
```js
const p = new Promise((resolve,reject)=>{
	//成功就用resolve
	//失败就用reject
});
//调用then方法，成功就会调用前一个函数参数，失败就会调用后一个函数参数
p.then(value=>{},reason=>{});
```


then方法的返回结果：(then方法返回的是Promise对象，但对象的状态时由回调函数的执行结果决定：)

```js
const result = p.then(value=>{},reason=>{});
//then方法返回的也是Promise对象
console.log(result);
```


### 6.1.2 工作伦理
1. then 方法的两个回调函数什么时候执行
   - pending——>resolved时，执行 then 的第一个回调函数
   - pending——>rejected 时，执行 then 的第二个回调函数

2. then 方法执行后的返回值
   - then 方法执行后默认自动返回一个新的 Promise 对象

3. then 方法返回的 Promise 对象的状态改变
   - then 方法其实默认返回的是 undefined，即：`return undefined`，但是 ES6 的机制规定：当 then 返回 undefined 时，那么会将这个 undefined 包装成一个 Promise，并且这个 Promise 默认调用了 `resolve()` 方法（成功态），并且把 undefined 作为了 resolve() 的参数，相当于：

```javascript
 const p = new Promise((resolve, reject) => {
     resolve();
 });
 
 p.then(() => {
     // 默认会执行这一条
     // return undefined;
 }, () => {
 });
 
 // 实际上，return 会包装为一个 Promise 对象，同时默认执行 resolve()，并把 return 的值作为 resolve() 的参数
 /*
 return new Promise(resolve => {
     resolve(undefined);
 });
 */
 
 // -----------------------------
 // 如果我们在这个返回的 Promise 上继续调用 then 方法，并接收参数的话，可以发现 then 中成功接收到了被 Promise 包装后的参数
 const p2 = new Promise((resolve, reject) => {
     resolve();
 });
 
 p2.then(() => {
     // 默认会执行这一条
     // return undefined;
 }).then(data => {
     console.log(data);  // 打印 undefined
     // 手动 return 一个值
     return 24;
     // 相当于：return new Promise(resolve => {resolve(24);});
 }).then((data) => {
     console.log(data);	// 打印 24
 });
```

   - 如果我们要让 then 返回一个失败状态的 Promise，那么我们可以手动 return 一个 Promise 并执行 reject() 方法。

 ```javascript
 const p3 = new Promise((resolve, reject) => {
     resolve();
 });
 p3.then(() => {
     // 手动返回一个调用了 reject 的 Promise
     return new Promise((resolve, reject) => {
         reject("失败");
     })
 }).then(() => {}, errData => {
     console.log(errData);	// 失败
 });
 ```

 **总结**：
 Promise 是一个构造函数，需要 new 才能使用。
 在 new Promise() 的时候需要传递一个匿名回调函数作为 Promise() 唯一的参数，这个回调函数有两个参数 resolve reject，这两个参数也是函数，当回调函数执行第一个 resolve 函数后 Promise 便变为了成功状态，反之回调函数执行了 reject 后 Promise 便变为了失败状态，且每个 Promise 只能要么执行 resolve，要么执行 reject，不能同时执行！
 
 当 Promise 被 new 之后就会有一个 then 方法，该方法默认接收两个匿名回调函数作为参数，其中第一个回调函数是在 Promise 为成功状态时自动调用的，反之第二个回调函数是在 Promise 为失败状态时自动调用的，并且这两个回调函数是可以接收参数的，参数就来自于 resolve 或 reject 调用时传递的实参！
 
 在 then 方法执行后会默认返回 undefined（在没有指定返回值的情况下），ES6 会将其包装为一个新的成功态的 Promise，该 Promise 会自动执行 resolve 函数，该函数的参数来自于 then 方法的返回值（如果没有返回值那么默认就返回 undefined）。如果需要返回一个失败态的 Promise，那么需要在 then 中手动指定返回值：

```javascript
return new Promise((resolve, reject) => {
	reject(参数);
}
 ```

### 6.1.3 回调函数中返回不同的结果产生的不同操作

(1）如果回调函数中返回的结果是 非promise类型的属性，状态则为成功，返回值为对象的成功值
```js
const result = p.then(value => {
        console.log("成功");
        console.log(value);
        return 123;
    }, reason => { 
        console.log("失败");
        console.log(reason);
    }
);

console.log(result);
```

返回的结果为123，非promise类型，所以状态为成功，返回123  
![在这里插入图片描述](https://img-blog.csdnimg.cn/edd9a6f19f134c8e888e3d2b08e003bd.png)  

若没写return，返回undefined，也是非promise类型，所以状态为成功  
![在这里插入图片描述](https://img-blog.csdnimg.cn/1c05fce2c7a14eac99198e2af8a7bc08.png)


(2) 如果回调函数中返回的结果时 是promise对象则：

promise对象内部返回的promise状态就决定了then方法返回的promise的状态

内部返回的promise状态为成功，then方法返回Promise对象状态也为成功，返回值为成功值：
```js
 const result = p.then(value => {
            console.log("成功");
            console.log(value);
            // return 123;
            // 2、如果回调函数中返回的结果时 是promise对象则：
            return new Promise((resolve, reject) => {
                // promise对象内部返回的promise状态就决定了then方法返回的promise的状态
                // 内部返回的promise状态为成功：
                resolve('ok');
            });
        }, reason => {
            console.log("失败");
            console.log(reason);
        });
        console.log(result);
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/f1a51d233f324d1183d080f52e88505c.png)

内部返回的promise状态为失败，then方法返回Promise对象状态也为失败，返回值为失败值：


```js
 const result = p.then(value => {
            console.log("成功");
            console.log(value);
            // return 123;
            // 2、如果回调函数中返回的结果时 是promise对象则：
            return new Promise((resolve, reject) => {
                // promise对象内部返回的promise状态就决定了then方法返回的promise的状态
                // 内部返回的promise状态为失败：
                reject("no")
            });
        }, reason => {
            console.log("失败");
            console.log(reason);
        });
        console.log(result);

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/384c4251349146de94112db301f45f91.png)

就是说，then方法返回的是一个promise对象，而返回的这个promise对象的状态 由 then方法中的回调函数的返回值决定。

当返回值是非promise对象时，then方法返回的这个promise对象的状态就是成功状态，且成功值为这个返回值；
当返回值时promise对象时，then方法返回的这个promise对象的状态就由返回值中的promise对象的状态决定，返回值中的promise对象的状态为成功，则then方法返回的这个promise对象的状态就为成功，成功值也是回值中的promise对象的成功值，反之失败也是一样


(3) 回调函数的执行结果决定为抛出错误时，状态则为失败，失败值为抛出的错误
```js
const result = p.then(value => {
            console.log("成功");
            console.log(value);
            // 3、回调函数的执行结果决定为抛出错误时，状态则为失败，失败值为抛出的错误
            throw "出错了";
        }, reason => {
            console.log("失败");
            console.log(reason);

        });
        console.log(result);
————————————————
版权声明：本文为CSDN博主「东篱_Y」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_55935744/article/details/120586664
```


![在这里插入图片描述](https://img-blog.csdnimg.cn/46670bdd6a56410890dc43cbd2676200.png)

代码记录：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        const p = new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve("data");
                // reject("err");
            }, 1000)
        });

        // then方法返回的是Promise对象，但对象的状态时由回调函数的执行结果决定
        const result = p.then(value => {
            console.log("成功");
            console.log(value);
            // 1、如果回调函数中返回的结果时 非promise类型的属性，promise状态则为成功，返回值为对象的成功值
            // return 123;
            // 2、如果回调函数中返回的结果时 是promise对象则：
            // return new Promise((resolve, reject) => {
            //     // promise对象内部返回的promise状态就决定了then方法返回的promise的状态
            //     // 内部返回的promise状态为成功：
            //     // resolve('ok');
            //     // 内部返回的promise状态为失败：
            //     // reject("no")
            // });
            // 3、回调函数的执行结果决定为抛出错误时，状态则为失败，失败值为抛出的错误
            throw "出错了";
        }, reason => {
            console.log("失败");
            console.log(reason);

        });
        console.log(result);
    </script>
</body>
</html>
```



既然then方法有这样的特性，就可以链式调用
p.then(value=>{},reject=>{}).then(value=>{},reject=>{})


### 6.1.4 案例：分别间隔一秒打印省市县。

```javascript
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Promise</title>
</head>

<body>
<script>
    // 通过 Promise 的方式，解决回调地狱
    new Promise((resolve) => {
        setTimeout(() => {
            console.log("云南省");
            resolve("云南省");
        }, 1000);
    }).then(res => {
        return new Promise((resolve) => {
            setTimeout(() => {
                console.log(res + "玉溪市");
                resolve(res + "玉溪市");
            }, 1000);
        });
    }).then(res => {
        setTimeout(() => {
            console.log(res + "峨山县");
        }, 1000);
    });

    console.log("通过 Promise 的方式，实现异步");
</script>
</body>

</html>
```

![2](https://i0.hdslb.com/bfs/album/1891f1c10ba44350cb747b01463178deb806c8bf.gif)




## 6.2 Promise.prototype.catch() 
用来指定promise失败的一个回调，相当于没有第一个参数的then方法。

由之前的例子可以看出，我们在使用 Promise 的时候，大部分情况下，我们只用 resolve() 方法（成功态），所以在 Promise 回调函数中我们常常省略 reject 函数参数，在 then 中我们常常省略第二个回调函数。

但是我们还是需要处理异步中的异常，所以 ES6 中提供了我们一个 `catch()` 方法专门用来处理 Promise 的异常部分（失败态）。
- catch 专门用来处理 rejected 状态
- catch 本质上是 then 的特例

![在这里插入图片描述](https://img-blog.csdnimg.cn/8b93c36c8eeb4d8a82a5061dcfde8a79.png)
```js

then方法：

const p = new Promise((resolve, reject) => {
            setTimeout(() => {
                // 设置p对象的状态为失败，并设置失败值
                reject("err")
            }, 1000)
        })
        p.then(value => {}, reason => {
            console.error(reason);
        })

catch方法：

 const p = new Promise((resolve, reject) => {
            setTimeout(() => {
                // 设置p对象的状态为失败，并设置失败值
                reject("err")
            }, 1000)
        })
        p.catch(reason => {
            console.warn(reason);
        })

```

```javascript
new Promise((resolve, reject) => {
    reject("失败");
}).then(res => {
    console.log(res);
}).catch(err => {
    console.log(err);   // 失败
});

// -------------------------------------
// 上面的代码本质上等同于
new Promise((resolve, reject) => {
    reject("失败");
}).then(res => {
    console.log(res);
}).then(null, err => {
    console.log(err);	// 失败
});
```

> 在 Promise 中，一但出现了错误状态，那么这个错误是不会消失的，会一直向下传递，直到遇到可以处理错误的函数。

由于 catch 是 then 的特例，所以 catch 依旧返回的是一个 Promise 对象，我们可以在 catch 后继续调用 then。

```javascript
new Promise((resolve, reject) => {
    reject("失败");
}).then(res => {
    console.log(res);
}).catch(err => {
    console.log(err);   // 失败
    return "测试";
}).then(res => {
   console.log(res);	// 测试 
});
```

> 一般总是建议，Promise 对象后面要跟一个或多个 catch 方法，这样可以处理 Promise 内部发生的错误！

## 6.3 Promise.prototype.finally()

 当 Promise 状态发生变化时，不论如何变化都会执行，不变化不执行。

- finally() 不能接收参数。

- finally 也是 then 的特例。

`finally()`方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。

```js
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});
```

上面代码中，不管`promise`最后的状态，在执行完`then`或`catch`指定的回调函数以后，都会执行`finally`方法指定的回调函数。

下面是一个例子，服务器使用 Promise 处理请求，然后使用`finally`方法关掉服务器。

```js
server.listen(port)
  .then(function () {
    // ...
  })
  .finally(server.stop);
```

`finally`方法的回调函数不接受任何参数，这意味着没有办法知道，前面的 Promise 状态到底是`fulfilled`还是`rejected`。这表明，`finally`方法里面的操作，应该是与状态无关的，不依赖于 Promise 的执行结果。

上面代码中，如果不使用`finally`方法，同样的语句需要为成功和失败两种情况各写一次。有了`finally`方法，则只需要写一次。

```javascript
new Promise(resolve => {
    resolve("测试01");
}).finally(data => {
    console.log(data + " finally01");
    return new Promise((resolve, reject) => {
        reject("测试02");
    })
}).finally(data => {
    console.log(data + " finally02")
}).catch(err => {
    console.log("catch: " + err);
});

/*
undefined finally01
undefined finally02
catch: 测试02
*/

// 从以上示例可以看出：finally 可以接收正确状态或错误状态，但是不能接收参数。

// -------------------------------------
// finally 也是 then 的特例
// finally 等同于：
new Promise((resolve, reject) => {
    ...
}).then(res => {
    return res;
}, err => {
    return new Promise((resolve, reject) => {
        reject(err);
    })
})
```

`finally`：主要是用来处理一些必做操作，比如在操作数据库之后（无论成功与否）都要关闭数据库连接。

## 6.4 Promise.all()

`Promise.all()`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

```js
const p = Promise.all([p1, p2, p3]);
```

上面代码中，`Promise.all()`方法接受一个数组作为参数，`p1`、`p2`、`p3`都是 Promise 实例，如果不是，就会先调用下面讲到的`Promise.resolve`方法，将参数转为 Promise 实例，再进一步处理。另外，`Promise.all()`方法的参数可以不是数组，但必须具有 Iterator 接口，且返回的每个成员都是 Promise 实例。

`p`的状态由`p1`、`p2`、`p3`决定，分成两种情况。

（1）只有`p1`、`p2`、`p3`的状态都变成`fulfilled`，`p`的状态才会变成`fulfilled`，此时`p1`、`p2`、`p3`的返回值组成一个数组，传递给`p`的回调函数。

（2）只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，此时第一个被`reject`的实例的返回值，会传递给`p`的回调函数。

下面是一个具体的例子。

```js
// 生成一个Promise对象的数组
const promises = [2, 3, 5, 7, 11, 13].map(function (id) {
  return getJSON('/post/' + id + ".json");
});

Promise.all(promises).then(function (posts) {
  // ...
}).catch(function(reason){
  // ...
});
```

上面代码中，`promises`是包含 6 个 Promise 实例的数组，只有这 6 个实例的状态都变成`fulfilled`，或者其中有一个变为`rejected`，才会调用`Promise.all`方法后面的回调函数。

```js
/*
Promise.all() 的状态变化与所有传入的 Promise 实例对象状态有关
用途举例：在用 Ajax 从后端接口获取数据的时候，如果全部获取到了，那么才处理，否则不处理。
*/

const delay = ms => {
    return new Promise(resolve => {
        setTimeout(resolve, ms);
    });
};

// 示例一：所有状态都变为 resolved
const p1 = delay(1000).then(() => {
    console.log('p1 完成了');
    return 'p1';
});
const p2 = delay(2000).then(() => {
    console.log('p2 完成了');
    return 'p2';
});
const p = Promise.all([p1, p2]);
p.then(res => {
    console.log(res + " 成功");
}, err => {
    console.log(err + " 失败");
});

/*
p1 完成了
p2 完成了
p1,p2 成功
*/
/*
解释：
1、Promise.all() 直接执行两个 Promise 实例
2、执行 p1，输出 p1 完成了
3、检测到 resolved，Promise.all() 继续执行
4、执行 p2，输出 p2 完成了
5、检测到 resolved，由于 Promise 已经全部执行完，所以执行 then 第一个回调输出 p1,p2 成功，Promise.all() 终止。
*/

// 示例二：出现一个 rejected 状态
const p1 = delay(1000).then(() => {
    console.log('p1 完成了');
    return Promise.reject('p1');
});
const p2 = delay(2000).then(() => {
    console.log('p2 完成了');
    return 'p2';
});
const p = Promise.all([p1, p2]);
p.then(res => {
    console.log(res + " 成功");
}, err => {
    console.log(err + " 失败");
});
/*
p1 完成了
p1 失败
p2 完成了
*/
/*
解释：
1、Promise.all() 直接执行两个 Promise 实例
2、执行 p1，输出 p1 完成了
3、检测到 rejected，Promise.all() 直接变为 rejected，执行 then 第二个回调输出 p1 失败，至此 Promise.all() 已经执行完毕。
4、由于 p2 延迟了两秒执行所以在后面输出（如果 p2 延时小于 p1，那么应该先输出 p2 完成了，然后在是 p1 完成了，p1 失败）
*/
```

## 6.5 Promise.resolve()和Promise.reject()

 以上两者都是 Promise 构造函数的方法。

> 下面我们以 Promise.resolve() 举例，Promise.reject() 同理。

 ```javascript
// Promise.resolve() 可以理解为普通成功状态的一种简写形式
new Promise(resolve => resolve('foo'));
// 简写
Promise.resolve('foo');
 ```

Promise.resolve() 与 Promise.reject() 的参数问题：

1、一般参数

```javascript
Promise.resolve('foo').then(data => {
    console.log(data);
})	// foo
```

2、特殊参数：Promise 作为参数

```javascript
const p1 = new Promise(resolve => {
    setTimeout(resolve, 1000, '我执行了');
    /*
    上述延时器写法相当于：
    setTimeout(()=>{
        resolve('我执行了');
    }, 1000);
     */
});
Promise.resolve(p1).then(data => {
    console.log(data);	// 等待一秒后，输出 '我执行了'
});

/*
当 Promise.resolve() 接收的是 Promise 对象时，直接返回这个 Promise 对象，什么都不做
*/

// 所以，以上代码等同于：
p1.then(data => {
   console.log(data); // 等待一秒后，输出 '我执行了'
});

// 验证
console.log(Promise.resolve(p1) === p1);	// true

// 由于 Promise.resolve() 可以理解为普通成功状态的一种简写形式，所以：
new Promise(resolve => resolve(p1)).then(data => {
   console.log(data); // 等待一秒后，输出 '我执行了'
});
```

3、特殊参数：具有 then 方法的对象（了解即可）

```javascript
const thenable = {
    then() {
        console.log('then');
    }
};
Promise.resolve(thenable).then(
    res => console.log("res " + res),
    err => console.log("err " + err)
);

/*
then
*/

// 当接收一个含 then 方法的对象时，Promise.resolve() 会直接调用 then 方法。

// 为什么不会执行 then 中的两个回调函数呢？
console.log(Promise.resolve(thenable));
/*
Promise { <pending> }
then
*/
// 可见，当接收一个含 then 方法的对象时，默认返回一个 Promise 并且是等待状态的，没有状态的变化，那么就不可能会执行 then 的回调函数
// 如果我们要改变这个返回的 Promise 对象的状态，并让 then 的回调对应处理的话，ES6 规定了以下写法：
const thenable02 = {
    then(resolve, reject) {
        console.log('then');
        resolve('then');
    }
};
Promise.resolve(thenable02).then(
    res => console.log("res " + res),
    err => console.log("err " + err)
);
/*
then
res then
*/
```

> 与 Promise.resolve() 不同，Promise.reject() 无论接收什么类型的参数，都会原封不动的向后传递！

## 6.6 Promise.race()

`Promise.race()`方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。

```js
const p = Promise.race([p1, p2, p3]);
```

上面代码中，只要`p1`、`p2`、`p3`之中有一个实例率先改变状态，`p`的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给`p`的回调函数。

`Promise.race()`方法的参数与`Promise.all()`方法一样，如果不是 Promise 实例，就会先调用`Promise.resolve()`方法，将参数转为 Promise 实例，再进一步处理。

下面是一个例子，如果指定时间内没有获得结果，就将 Promise 的状态变为`reject`，否则变为`resolve`。

```js
const p = Promise.race([
  fetch('/resource-that-may-take-a-while'),
  new Promise(function (resolve, reject) {
    setTimeout(() => reject(new Error('request timeout')), 5000)
  })
]);

p
.then(console.log)
.catch(console.error);
```

上面代码中，如果 5 秒之内`fetch`方法无法返回结果，变量`p`的状态就会变为`rejected`，从而触发`catch`方法指定的回调函数。

## 6.7 Promise.allSettled()

有时候，我们希望等到一组异步操作都结束了，不管每一个操作是成功还是失败，再进行下一步操作。但是，现有的 Promise 方法很难实现这个要求。

`Promise.all()`方法只适合所有异步操作都成功的情况，如果有一个操作失败，就无法满足要求。

```js
const urls = [url_1, url_2, url_3];
const requests = urls.map(x => fetch(x));

try {
  await Promise.all(requests);
  console.log('所有请求都成功。');
} catch {
  console.log('至少一个请求失败，其他请求可能还没结束。');
}
```

上面示例中，`Promise.all()`可以确定所有请求都成功了，但是只要有一个请求失败，它就会报错，而不管另外的请求是否结束。

为了解决这个问题，ES2020引入了`Promise.allSettled()`方法，用来确定一组异步操作是否都结束了（不管成功或失败）。所以，它的名字叫做”Settled“，包含了”fulfilled“和”rejected“两种情况。

`Promise.allSettled()`方法接受一个数组作为参数，数组的每个成员都是一个 Promise 对象，并返回一个新的 Promise 对象。只有等到参数数组的所有 Promise 对象都发生状态变更（不管是`fulfilled`还是`rejected`），返回的 Promise 对象才会发生状态变更。

```js
const promises = [
  fetch('/api-1'),
  fetch('/api-2'),
  fetch('/api-3'),
];

await Promise.allSettled(promises);
removeLoadingIndicator();
```

上面示例中，数组`promises`包含了三个请求，只有等到这三个请求都结束了（不管请求成功还是失败），`removeLoadingIndicator()`才会执行。

该方法返回的新的 Promise 实例，一旦发生状态变更，状态总是`fulfilled`，不会变成`rejected`。状态变成`fulfilled`后，它的回调函数会接收到一个数组作为参数，该数组的每个成员对应前面数组的每个 Promise 对象。

```js
const resolved = Promise.resolve(42);
const rejected = Promise.reject(-1);

const allSettledPromise = Promise.allSettled([resolved, rejected]);

allSettledPromise.then(function (results) {
  console.log(results);
});
// [
//    { status: 'fulfilled', value: 42 },
//    { status: 'rejected', reason: -1 }
// ]
```

上面代码中，`Promise.allSettled()`的返回值`allSettledPromise`，状态只可能变成`fulfilled`。它的回调函数接收到的参数是数组`results`。该数组的每个成员都是一个对象，对应传入`Promise.allSettled()`的数组里面的两个 Promise 对象。

`results`的每个成员是一个对象，对象的格式是固定的，对应异步操作的结果。

```js
// 异步操作成功时
{status: 'fulfilled', value: value}

// 异步操作失败时
{status: 'rejected', reason: reason}
```

成员对象的`status`属性的值只可能是字符串`fulfilled`或字符串`rejected`，用来区分异步操作是成功还是失败。如果是成功（`fulfilled`），对象会有`value`属性，如果是失败（`rejected`），会有`reason`属性，对应两种状态时前面异步操作的返回值。

下面是返回值的用法例子。

```js
const promises = [ fetch('index.html'), fetch('https://does-not-exist/') ];
const results = await Promise.allSettled(promises);

// 过滤出成功的请求
const successfulPromises = results.filter(p => p.status === 'fulfilled');

// 过滤出失败的请求，并输出原因
const errors = results
  .filter(p => p.status === 'rejected')
  .map(p => p.reason);
```
# 7 Promise的应用

### 7.1.1 异步加载图片

异步加载：也称为图片的预加载。利用 js 代码提前加载图片，用户需要时可以直接从本地缓存获取，但是会增加服务器前端的压力。这样做可以提高用户的体验，因为同步加载大图片的时候，图片会一层一层的显示处理，但是经过预加载后，直接显示出整张图片。

```html
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <title>Promise 的应用</title>
    <style>
        #img {
            width: 24%;
            padding: 24px;
        }
    </style>
</head>
<body>
<!-- 一般加载图片方式 -->
<!-- <img src="https://scpic.chinaz.net/files/pic/pic9/202009/apic27858.jpg" alt=""/> -->
<img src="" alt="" id="img">

<script>
    // 异步加载图片
    // 异步加载图片函数（参数：图片路径）
    const loadImgAsync = url => {
        // Promise 实现异步
        return new Promise((resolve, reject) => {
            // 创建一个图片对象
            const img = new Image();

            // 图片成功加载触发事件
            img.onload = () => {
                resolve(img);
            };

            // 图片加载失败触发事件
            img.onerror = () => {
                reject(new Error(`Could not load image at ${url}`));
            };

            // 这个放在 onload 与 onerror 之后
            // 一但给 img.src 赋值，那么便立马开始发送请求加载图片（在后台加载，页面上不会显示）
            // 注意：这里的 src 是 img 对象的属性，与 html 中 img 的 src 无关
            img.src = url;
        });
    };

    const imgDOM = document.getElementById('img');
    loadImgAsync('https://scpic.chinaz.net/files/pic/pic9/202009/apic27858.jpg')
        .then(img => {
            // 如果加载成功，那么把后台缓存的图片显示到页面上
            imgDOM.src = img.src;
        })
        .catch(err => {
            console.log(err);
        });
</script>
</body>
</html>
```

![image-20220528144323405](https://i0.hdslb.com/bfs/album/3d95f9d84019bfe212e1abec0eb135f92636a8ef.png)

### 7.1.2 Promise封装读取文件
一般写法, 不使用Promise封装：
![在这里插入图片描述](https://img-blog.csdnimg.cn/19496369779441a99dccd408e4b713d7.png)

```js
// 1、引入fs模块
const fs = require('fs');
//2、调用方法读取文件
fs.readFile('./古诗1.md', 'utf-8', (err, data) => {
    //如果失败，则抛出错误(throw抛出一个错误)
    if (err)
        throw err;
    //没有错误则输出内容
    console.log(data);
})
```

控制台则输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/c03a853a315b40a0830c98acfbdc593c.png)


使用Promise封装：
```js
// 1、引入fs模块
const { rejects } = require('assert/strict');
const fs = require('fs');
const p = new Promise((resolve, reject) => {
    fs.readFile('./古诗1.md', 'utf-8', (err, data) => {
        if (err) reject(err);
        resolve(data);
    });
});

p.then((value) => {
    console.log(value);
}, (reason) => {
    console.log('读取失败');
})
```


输出结果同上。

### 7.1.3 多个文件读取
![在这里插入图片描述](https://img-blog.csdnimg.cn/b1395e0bb8a84a4bbfb558fd359432eb.png)

一般写法, 不用promise封装（模拟回调地狱）：
```js
const fs = require("fs");
fs.readFile('./p1.md', 'utf-8', (err1, data1) => {
    fs.readFile('./p2.md', 'utf-8', (err2, data2) => {
        fs.readFile('./p3.md', 'utf-8', (err3, data3) => {
            let result = data1 + "\n\n" + data2 + "\n\n" + data3;
            console.log(result);
        });
    });
});
```


用promise封装：
```js
const fs = require("fs");
const p = new Promise((resolve, reject) => {
    fs.readFile('./p1.md', 'utf-8', (err, data) => {
        resolve(data);
    });
});
p.then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile('./p2.md', 'utf-8', (err, data) => {
            // value 的值就是上面data的值
            resolve([value, data])
        });
    });
}, reason => {}).then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile('./p3.md', 'utf-8', (err, data) => {
            // value 的值就是上面[value, data]的值
            value.push(data);
            resolve(value)
        });
    });
}, reason => {}).then(value => {
    console.log(value.join("\n\n"));
}, reason => {})
```


### 7.1.4 Promise封装ajax请求

先写个服务器端：
```js

//引入express框架
const express = require('express');
//创建网站服务器
const app = express();

app.get('/server', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*');
    //send()
    //1.send方法内部会检测响应内容的类型
    //2.send方法会自动设置http状态码
    //3.send方法会自动设置响应的内容类型及编码
    const data = {
            name: 'zhangsan',
            age: 8
        }
        //设置定时器，3秒钟后响应给客户端
    res.send(data);
});
//监听端口
app.listen(3000);
console.log('网站服务器启动成功');

```

原生js写AJAX：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        // 四步走
        // 1、创建对象
        const xhr = new XMLHttpRequest();

        // 2、初始化 设置请求方式和url
        xhr.open("GET", "http://localhost:3000/server");

        // 3、发送
        xhr.send();

        // 4、绑定事件，处理响应结果

        xhr.onreadystatechange = function() {
            if (xhr.readyState === 4) {
                if (xhr.status >= 200 && xhr.status < 300) {
                    // 表示成功，返回响应体
                    console.log(xhr.response);
                } else {
                    //表示失败，返回状态码
                    console.log(123);
                    console.error(xhr.status);
                }
            }
        }
    </script>
</body>

</html>
```






用promise封装：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        const p = new Promise((res, rej) => {
            // 四步走
            // 1、创建对象
            const xhr = new XMLHttpRequest();

            // 2、初始化 设置请求方式和url
            xhr.open("GET", "http://localhost:3000/server");

            // 3、发送
            xhr.send();

            // 4、绑定事件，处理响应结果

            xhr.onreadystatechange = function() {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300) {
                        // 表示成功
                        res(xhr.response);
                    } else {
                        //表示失败
                        rej(xhr.status);
                    }
                }
            }
        });
        p.then((value) => {
            console.log(value);
        }, (reason) => {
            console.error(reason);
        });
    </script>
</body>

</html>


```

