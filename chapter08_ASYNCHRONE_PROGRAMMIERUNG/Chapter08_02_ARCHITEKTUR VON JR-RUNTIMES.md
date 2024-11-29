
ASYNCHRONE MECHANISMEN IM WEBBROWSER

下面的这些模块都是用来异步处理任务的模块
- Web APIs (XMLHttpRequest, Fetch API,...)   
- setTimeout, setInterval
- Promises


# 1 基础 

![](image/Pasted%20image%2020241129154822.png)


- Eine **_JavaScript Laufzeitumgebung_** (**_Runtime Environment_**) interpretiert JavaScript-Programme und führt sie aus
- Wichtige Elemente der Laufzeitumgebung sind Call Stack, Callback Queue und Event Loop
- Laufzeitumgebung im Browser interagiert mit _Web APIs_ zur asynchronen Ausführung von Programmen
- **_Call Stack_** ist ein Stapelspeicher der den Ausführungskontext von Funktionen nach dem **_Last-In-First-Out-Prinzip_** (**_LIFO_**) verwaltet    
    - 执行栈:  保存一些命令 并且执行这些命令
- **_Callback Queue_** ist eine Warteschlange, welche den zur asynchronen Ausführung bestimmten Code verwaltet
    - 任务队列:  异步任务相关回调函数添加到任务队列中
- **_Event Loop_** überprüft kontinuierlich die Einträge im Call Stack - sind keine vorhanden, übergibt sie dem Call Stack Einträge aus der Callback Queue zur Ausführung
    - **_Event Loop_**  从 Callback Queue 拿出 Einträge, 将他加入到 Call Stack 中,  用 call stack 去执行它 
- JavaScript Runtime ist **_single-threaded_**, d.h. sie verfügt nur über einen Call Stack und die Ausführung mehrerer Threads ist nicht vorgesehen (Ausnahme: Web Worker API


# 2 执行栈和任务队列

![在这里插入图片描述](https://img-blog.csdnimg.cn/f0cc815b48574ce2bb068501a9394a5e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)
1. 先执行执行栈中的同步任务
2. 异步任务(回调函数)放入任务队列中 (异步任务相关回调函数添加到任务队列中)
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行
![在这里插入图片描述](https://img-blog.csdnimg.cn/d337ebf7ba2c40c7a768fd91f6bfbf56.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)


---

event loop
![在这里插入图片描述](https://img-blog.csdnimg.cn/eaabe7880146428fb68e6e64f23db40c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)
同步任务放在执行栈中执行，异步任务由异步进程处理放到任务队列中，执行栈中的任务执行完毕会去任务队列中查看是否有异步任务执行，由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为事件循环（ event loop）。


# 3 例子分析

## 3.1 

```js
document.addEventListener(
  "click", function onClick() {
    setTimeout(function timer() {
      console.log("Du hast geklickt");
    }, 2000);
  }
);

console.log("Hallo");

setTimeout(function timeout() {
  console.log("Drücke die Maustaste!");
}, 10000);

console.log("Synchrone Ausführung beendet");
```

![](image/Pasted%20image%2020241129160805.png)

![](image/Pasted%20image%2020241129160842.png)

![](image/Pasted%20image%2020241129161410.png)

![](image/Pasted%20image%2020241129162017.png)


4 bis 10 
当 执行完 下面的模块后
```js
setTimeout(function timeout() {
  console.log("Drücke die Maustaste!");
}, 10000);
```

WebAPI 是个处理异步操作的 东西, 他会生成一个 `timeout[10000]`  在 Web API 中 

10s钟过后 , 会将 console.log("Drücke die Maustaste!") 从 Callback Queue 中拿到 Call stack 中 , Call Stack 去执行他


11 bis 16 
WebAPI listen the click operation 一旦有话,  将 之后要执行的命令 交给 Callback 

## 3.2 
此时再来看我们刚才的问题：
1

```js
console.log(1);
setTimeout(function() {
    console.log(3);
},1000);
console.log(2);

执行的结果和顺序为 1、2、3
```


2
```js
console.log(1);
setTimeout(function() {
    console.log(3);
},0);
console.log(2);

执行的结果和顺序为 1、2、3

```

3 
```js
console.log(1);
document.onclick = function() {
    console.log('click');
}
console.log(2);
setTimeout(function() {
    console.log(3)
}, 3000)

```







