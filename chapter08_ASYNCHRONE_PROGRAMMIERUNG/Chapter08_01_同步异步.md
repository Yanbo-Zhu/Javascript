

为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程
于是，JS 中出现了同步和异步。

同步: 前一个任务结束后再执行后一个任务
异步： 在做这件事的同时，你还可以去处理其他事情

# 1 同步的概念

Synchrone Programme werden durch die Laufzeitumgebung Zeile für Zeile abgearbeitet

Laufzeitumgebung wartet bis die gegenwärtige Zeile abgearbeitet ist und springt dann zur nächsten Zeile

Bei Funktionsaufruf wird der Befehlszeiger auf den Speicherbereich mit der ersten Anweisung innerhalb der Funktion gesetzt und dort die synchrone Ausführung fortgesetzt

Bei Rückkehr aus einer Funktion wird ab der nächsten Zeile nach dem ursprünglichen Funktionsaufruf fortgesetzt
Mit rein synchroner Programmierung kann nicht auf Ereignisse reagiert werden

Synchrone Programme führen oft zu Blockierungen, z.B. auf Interaktionen mit einer Webseite wird nicht reagiert, weil die Laufzeitumgebung "mit anderen Dingen beschäftigt" ist

![](image/Pasted%20image%2020241129143102.png)
# 2 异步的概念

 异步（Asynchronous, async）是与同步（Synchronous, sync）相对的概念。

 在我们学习的传统单线程编程中，程序的运行是同步的（同步不意味着所有步骤同时运行，而是指步骤在一个控制流序列中按顺序执行）。而异步的概念则是不保证同步的概念，也就是说，一个异步过程的执行将不再与原有的序列有顺序关系。

 简单来理解就是：同步按你的代码顺序执行，异步不按照代码顺序执行，异步的执行效率更高。


- Bei asynchronen Programmen werden Teile des Programms aus der synchronen Ausführung herausgenommen und auf einen bestimmten oder unbestimmten späteren Zeitpunkt verschoben
- Spätere Ausführung der asynchronen Programmteile wird durch vordefi nierter Ereignisse ausgelöst oder fi ndet statt, wenn die Laufzeitumgebung "nichts anderes zu tun hat"
- Wird eingesetzt, wenn ein zeitlich vorhersehbarer Ablauf des Programms nicht gegeben ist
- Asynchrone Programmierung führt zu reaktiven Programmen, die i.d.R. weniger blockieren
- Callbacks sind Funktionen, die der Laufzeitumgebung zur asynchronen Ausführung übergeben werden
- ==Callbacks are functions that are passed to the runtime environment for asynchronous execution.==

 以上是关于异步的概念的解释，接下来我们通俗地解释一下异步：异步就是从主线程发射一个子线程来完成任务。

 ![img](https://i0.hdslb.com/bfs/album/d1cc4d26fc4056acf3f704bddb4bfecdf3b3ddd0.png)


# 3 什么时候用异步编程

 在前端编程中（甚至后端有时也是这样），我们在处理一些简短、快速的操作时，例如计算 1 + 1 的结果，往往在主线程中就可以完成。主线程作为一个线程，不能够同时接受多方面的请求。所以，当一个事件没有结束时，界面将无法处理其他请求。

 现在有一个按钮，如果我们设置它的 onclick 事件为一个死循环，那么当这个按钮按下，整个网页将失去响应。

 为了避免这种情况的发生，我们常常用子线程来完成一些可能消耗时间足够长以至于被用户察觉的事情（或者是一些需要等待某个时机在背后自动执行的任务，比如：事件监听），比如读取一个大文件或者发出一个网络请求。因为子线程独立于主线程，所以即使出现阻塞也不会影响主线程的运行。但是子线程有一个局限：一旦发射了以后就会与主线程失去同步，我们无法确定它的结束，如果结束之后需要处理一些事情，比如处理来自服务器的信息，我们是无法将它合并到主线程中去的。

 JavaScript 是单线程语言，为了解决多线程问题，JavaScript 中的异步操作函数往往通过**回调函数**来实现异步任务的结果处理。

# 4 回调函数 (callback function)



- Callbacks sind Funktionen, die der Laufzeitumgebung zur asynchronen Ausführung übergeben werden
- ==Callbacks are functions that are passed to the runtime environment for asynchronous execution.==

在 JavaScript 中，回调函数具体的定义为：函数A 作为参数（函数引用）传递到另一个 函数B 中，并且这个 函数B 执行函数A。我们就说 函数A 叫做回调函数。如果没有名称（函数表达式），就叫做匿名回调函数。

简单理解就是：==函数a有一个参数，这个参数的值 给入的是 函数b，当函数a执行完以后执行函数b。那么这个过程就叫回调==
```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<script language="javascript" type="text/javascript">
    function a(callback)
    {
        alert("我是parent函数a！");
        alert("调用回调函数");
        callback();
    }
    function b(){
        alert("我是回调函数b");

    }
    function c(){
        alert("我是回调函数c");

    }

    function test()
    {
        a(b);
        a(c);
    }

</script>
<body>
<h1>学习js回调函数</h1>
<button onClick=test()>click me</button>
<p>应该能看到调用了两个回调函数</p>
</body>
</html>

```


## 4.1 例子 

### 4.1.1 

```javascript
function z(callback) {
  setTimeout(function() {
    console.log("Ergebnis von z()");
    callback();
  }, 3000);
};

z(()=>{
    console.log("z() ist fertig");
   });
   
```


下面 就是定义一个 function 的全部, 不过是 通过 lambda 的方式 
```
() => {
    console.log("z() ist fertig");
}
```

When `z()` is called with a callback, here's what happens:
1. The `z` function executes the synchronous `console.log("z() is starting")` immediately.
2. A `setTimeout` is triggered, starting a 1-second countdown.
3. After 1 second:
    - `"z() operation completed"` is logged.
    - The callback function is executed.

### 4.1.2 


```js
function callWebServerSync(url) {
    console.log("Calling "+url);
    var n=5000000000;
    while (n>0) n--;
    console.log(url+": 200"); 
};


callWebServerSync("http://www.tu.berlin");
callWebServerSync("http://www.tu.berlin/main.css");
callWebServerSync("http://www.tu.berlin/main.js");

```


输出是 
![](image/Pasted%20image%2020241129153855.png)



---

```js
function callWebServerAsync(url) {
    console.log("Calling "+url);   // 执行完这句后, 会等5s, 在执行 console.log(url+": 200"). 这5s 中执行什么都可以 
    setTimeout(
      ()=>console.log(url+": 200"), 5000
    );
};

callWebServerAsync("http://www.tu.berlin");
callWebServerAsync("http://www.tu.berlin/main.css");
callWebServerAsync("http://www.tu.berlin/main.js");
```


输出是 
![](image/Pasted%20image%2020241129154029.png)



## 4.2 异步任务: JS中的异步是通过回调函数实现的

异步任务有以下三种类型
普通事件，如click,resize等
资源加载，如load,error等
定时器，包括setInterval,setTimeout等


## 4.3 回调同步和回调异步

回调函数就是一个作为参数的函数，它是在我们启动一个异步任务的时候就告诉它：等你完成了这个任务之后要干什么。这样一来主线程几乎不用关心异步任务的状态了，他自己会善始善终。

注意：回调和异步不是同一个东西，许多人误认为 js 中每个回调函数都是异步处理的，实际上并不是，可以同步回调，也可以异步回调。

只不过说：**回调可以是同步也可以是异步，异步必须放在回调里执行，也就是对于一个异步任务只有回调函数里的才是异步的部分。**

 回调同步的例子：

 ```javascript
> > const test = function (func) {
> >  func();
> > }
> > 
> > test(() => {
> >  console.log('func');
> > })
 ```

回调异步的例子：

 ```javascript
> > setTimeout(()=>{
> >  console.log('one');
> > }, 3000);
> > console.log('two');
 ```



# 5 实例
## 5.1 实例1
 `setInterval()` 和 `setTimeout()` 是两个异步语句。

异步（asynchronous）：不会阻塞 CPU 继续执行其他语句，当异步完成时（包含回调函数的主函数的正常语句完成时），会执行 “回调函数”（callback）。

```html

 ```h
> <!DOCTYPE html>
> <html>
> 
> <head>
> <meta charset="utf-8">
> <title>菜鸟教程(runoob.com)</title>
> </head>
> 
> <body>
> 
> <p>回调函数等待 3 秒后执行。</p>
> <p id="demo"></p>
> <p>异步方式，不影响后续执行。</p>
> <script>
>   function print() {
>       document.getElementById("demo").innerHTML = "RUNOOB!";
>   }
>   setTimeout(print, 3000);
> </script>
> 
> </body>
> 
> </html>
 ```

![1](https://i0.hdslb.com/bfs/album/365c74378381a0e69761dfe542d2de267c1b3828.gif)
这段程序中的 setTimeout 就是一个消耗时间较长（3 秒）的过程，它的第一个参数是个回调函数，第二个参数是毫秒数，这个函数执行之后会产生一个子线程，子线程会等待 3 秒，然后执行回调函数 "print"，在命令行输出 "RUNOOB!"。

当然，JavaScript 语法十分友好，我们不必单独定义一个函数 print ，我们常常将上面的程序写成：

## 5.2 实例2

 ```html
> <!DOCTYPE html>
> <html>
> 
> <head>
> <meta charset="utf-8">
> <title>菜鸟教程(runoob.com)</title>
> </head>
> 
> <body>
> 
> <p>回调函数等待 3 秒后执行。</p>
> <p id="demo"></p>
> <p>异步方式，不影响后续执行。</p>
> <script>
>   setTimeout(function () {
>       document.getElementById("demo").innerHTML = "RUNOOB!";
>   }, 3000);
>   /* ES6 箭头函数写法
>   setTimeout(() => {
>       document.getElementById("demo").innerHTML = "RUNOOB!";
>   }, 3000);
>   */
> </script>
> 
> </body>
> 
> </html>
 ```

**注意：**既然 setTimeout 会在子线程中等待 3 秒，在 setTimeout 函数执行之后主线程并没有停止，所以：

## 5.3 实例3

 ```html
> <!DOCTYPE html>
> <html>
> 
> <head>
> <meta charset="utf-8">
> <title>菜鸟教程(runoob.com)</title>
> </head>
> 
> <body>
> 
> <p>回调函数等待 3 秒后执行。</p>
> <p id="demo1"></p>
> <p id="demo2"></p>
> <script>
>   setTimeout(function () {
>       document.getElementById("demo1").innerHTML = "RUNOOB-1!";
>   }, 3000);
>   document.getElementById("demo2").innerHTML = "RUNOOB-2!";
> </script>
> 
> </body>
> 
> </html>
 ```

这段程序的执行结果是：

 ![2](https://i0.hdslb.com/bfs/album/ad3300e4fccf3861082bcb9633584d5aad190b98.gif)

（之前常用的异步操作解决方案是：回调函数）

```javascript
document.addEventListener(
    'click',
    () => {
        console.log('这里是异步的');
    },
    false
);
console.log('这里是同步的');
```




