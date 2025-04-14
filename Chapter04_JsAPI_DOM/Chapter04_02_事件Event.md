
# 1 事件基础

Ein Event-Handler in JavaScript ist eine Funktion, die auf ein bestimmtes Ereignis (z. B. Klick, Mausbewegung oder Tastendruck) reagiert. Sie wird einem HTML-Element zugewiesen und aktiviert, wenn das Ereignis eintritt. Beispielsweise kann ein Button ein click-Event auslösen, das durch den zugehörigen Event-Handler verarbeitet wird. Event-Handler werden häufig mit Methoden wie addEventListener oder direkt als Attribut im HTML (onclick, onmouseover) definiert.

![](image/Pasted%20image%2020241214160833.png)

## 1.1 事件概述 Ereignis/Events
JavaScript 使我们有能力创建动态页面，而事件是可以被 JavaScript 侦测到的行为。

简单理解： 触发— 响应机制。

网页中的每个元素都可以产生某些可以触发 JavaScript 的事件，例如，我们可以在用户点击某按钮时产生一个事件，然后去执行某些操作。


- Interaktive Webseiten mit Hilfe von **_Ereignissen_** (**_Events_**)
- Beispiel: Wechsel von Bildern beim Überfahren mit der Maus
- Ereignisse werden durch die Laufzeitumgebung erkannt oder können durch das Programm ausgelöst werden
- **_Event Handler_** oder **_Event Listener_** sind Callbacks, die ausgeführt werden wenn ein bestimmtes Ereignis auf einem Element oder Objekt ausgelöst wurde


## 1.2 事件三要素
事件源(谁)
事件类型(什么事件)
事件处理程序(做啥)

```html
<script>
    // 点击一个按钮，弹出对话框
    // 1. 事件是有三部分组成  事件源  事件类型  事件处理程序   我们也称为事件三要素
    //(1) 事件源 事件被触发的对象   谁  按钮
    var btn = document.getElementById('btn');
    //(2) 事件类型  如何触发 什么事件 比如鼠标点击(onclick) 还是鼠标经过 还是键盘按下
    //(3) 事件处理程序  通过一个函数赋值的方式 完成
    btn.onclick = function() {
        alert('点秋香');
    }
</script>
```


## 1.3 执行事件的步骤 Ablauf 
获取事件源
注册事件(绑定事件)
添加事件处理程序(采取函数赋值形式)
```js
<script>
    // 执行事件步骤
    // 点击div 控制台输出 我被选中了
    // 1. 获取事件源
    var div = document.querySelector('div');
    // 2.绑定事件 注册事件
    // div.onclick 
    // 3.添加事件处理程序 
    div.onclick = function() {
        console.log('我被选中了');
    }
</script>
```

1. Registrierung des Event Listener bei der Laufzeitumgebung für Ereignisse auf bestimmten Elementen bzw. Objekten
2. Auftreten des Ereignisses, zum Beispiel Betätigung eines Buttons mit der Maus
3. Erkennung des Ereignisses durch die Laufzeitumgebung
4. Benachrichtigung des Event Listener
5. Durchführung ereignisbezogener Aktionen



# 2 DOM事件流 / Event Propagation Reihenfolge
- 事件流描述的是从页面中接收事件的顺序
- 事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

![在这里插入图片描述](https://img-blog.csdnimg.cn/063297f2336f43dfb246930ae877a9ad.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

事件冒泡： IE 最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点的过程。
事件捕获： 网景最早提出，由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程。
加深理解： 我们向水里面扔一块石头，首先它会有一个下降的过程，这个过程就可以理解为从最顶层向事件发生的最具体元素（目标点）的捕获过程；之后会产生泡泡，会在最低点（ 最具体元素）之后漂浮到水面上，这个过程相当于事件冒泡。

![在这里插入图片描述](https://img-blog.csdnimg.cn/51f0146f0e334813b35d9b7075382a33.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

## 2.1 捕获阶段/ capture phase
document -> html -> body -> father -> son
两个盒子嵌套，一个父盒子一个子盒子，我们的需求是当点击父盒子时弹出 father ，当点击子盒子时弹出 son
```html
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // dom 事件流 三个阶段
        // 1. JS 代码中只能执行捕获或者冒泡其中的一个阶段。
        // 2. onclick 和 attachEvent（ie） 只能得到冒泡阶段。
        // 3. 捕获阶段 如果addEventListener 第三个参数是 true 那么则处于捕获阶段  document -> html -> body -> father -> son
        var son = document.querySelector('.son');
        son.addEventListener('click', function() {
             alert('son');
        }, true);
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, true);
    </script>
</body>
```


但是因为DOM流的影响，我们点击子盒子，会先弹出 father，之后再弹出 son
![在这里插入图片描述](https://img-blog.csdnimg.cn/65d6a7c8038f414fbf03c3ac4d2ce293.gif#pic_center)

这是因为捕获阶段由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收
- document -> html -> body -> father -> son
- 先看 document 的事件，没有；再看 html 的事件，没有；再看 body 的事件，没有；再看 father 的事件，有就先执行；再看 son 的事件，再执行。

## 2.2 冒泡阶段/ Propagation phase 
son -> father ->body -> html -> document

我们点击子盒子，会弹出 son、father、document
这是因为冒泡阶段开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点
son -> father ->body -> html -> document
```html
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
		// 4. 冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 那么则处于冒泡阶段  son -> father ->body -> html -> document
        var son = document.querySelector('.son');
        son.addEventListener('click', function() {
            alert('son');
        }, false);
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
</body>
```


![在这里插入图片描述](https://img-blog.csdnimg.cn/9ab4190f50d14c7aa879789476a394e9.gif#pic_center)



## 2.3 小结
- JS 代码中只能执行捕获或者冒泡其中的一个阶段
- onclick 和 attachEvent只能得到冒泡阶段
- addEventListener(type,listener[,useCapture])第三个参数
    - 如果是 true，表示在事件捕获阶段调用事件处理程序；
    - 如果是 false (不写默认就是false),表示在事件冒泡阶段调用事件处理程序
- 实际开发中我们很少使用事件捕获，我们更关注事件冒泡。
- 有些事件是没有冒泡的，比如 onblur、onfocus、onmouseenter、onmouseleave


# 3 事件对象 Ereignis/Ergebnis

```js
eventTarget.onclick = function(event) {
   // 这个 event 就是事件对象，我们还喜欢的写成 e 或者 evt 
} 
eventTarget.addEventListener('click', function(event) {
   // 这个 event 就是事件对象，我们还喜欢的写成 e 或者 evt  
})
```


官方解释：event 对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态

简单理解：
事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面
这个对象就是事件对象 event，它有很多属性和方法，比如“
- 谁绑定了这个事件
- 鼠标触发事件的话，会得到鼠标的相关信息，如鼠标位置
- 键盘触发事件的话，会得到键盘的相关信息，如按了哪个键
这个 event 是个形参，系统帮我们设定为事件对象，不需要传递实参过去
当我们注册事件时， event 对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）

```html
<body>
    <div>123</div>
    <script>
        // 事件对象
        var div = document.querySelector('div');
        div.onclick = function(e) {
                // console.log(e);
                // console.log(window.event);
                // e = e || window.event;
                console.log(e);


            }
        // 1. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看
        // 2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
        // 3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
        // 4. 这个事件对象我们可以自己命名 比如 event 、 evt、 e
        // 5. 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;
    </script>
</body>
```

## 3.1 事件对象的兼容性方案
事件对象本身的获取存在兼容问题：
标准浏览器中是浏览器给方法传递的参数，只需要定义形参 e 就可以获取到。
在 IE6~8 中，浏览器不会给方法传递参数，如果需要的话，需要到 window.event 中获取查找
解决：
`e = e || window.event;`

```html
<body>
    <div>123</div>
    <script>
        // 事件对象
        var div = document.querySelector('div');
        div.onclick = function(e) {
                // e = e || window.event;
                console.log(e);
				// 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;

            }
</body>
```




## 3.2 `event`-Object

event-Object: Methoden und Eigenschaften zur Abfrage von Daten, die das Event näher beschreiben
Eigenschaften des event-Objekts

| Eigenschaft                                      | Beschreibung                                                                   |
| ------------------------------------------------ | ------------------------------------------------------------------------------ |
| **`event.currentTarget`**                        | Liefert das Element welches das Ereignis ausgelöst hat                         |
| `**event.timeStamp**`                            | Liefert den Zeitstempel im ms zu dem das Ereignis auftrat                      |
| `**event.clientX**` und  <br>`**event.clientY**` | Koordinaten des Mauszeigers zum Zeitpunkt eines aufgetretenen Maus-Ereignisses |
| `**event.key**`                                  | Liefert Wert der Taste die bei einem Tastatur-Ereignis ausgelöst wurde         |
|                                                  |                                                                                |

## 3.3 事件对象的常见属性和方法
| 事件对象属性方法            | 说明                             |
| ------------------- | ------------------------------ |
| e.target            | 返回触发事件的对象 标准                   |
| e.srcElement        | 返回触发事件的对象 非标准 ie6-8使用          |
| e.type              | 返回事件的类型 比如click mouseover 不带on |
| e.cancelBubble      | 该属性阻止冒泡，非标准，ie6-8使用            |
| e.returnValue       | 该属性阻止默认行为 非标准，ie6-8使用          |
| e.preventDefault()  | 该方法阻止默认行为 标准 比如不让链接跳转          |
| e.stopPropagation() | 阻止冒泡 标准                        |

- click : Wird ausgelöst, wenn ein Element angeklickt wird.
- mouseover : Wird ausgelöst, wenn die Maus über ein Element bewegt wird.
- mouseout : Wird ausgelöst, wenn die Maus das Element verlässt.
- keydown : Wird ausgelöst, wenn eine Taste auf der Tastatur gedrückt wird.
- keyup : Wird ausgelöst, wenn eine gedrückte Taste wieder losgelassen wird.
- submit : Wird ausgelöst, wenn ein Formular abgeschickt wird.
- load : Wird ausgelöst, wenn ein Bild Oder eine Seite vollständig geladen ist.
- scroll : Wird ausgelöst, wenn der Benutzer scrollt.


---

Fenstereignisse

| Ereignis...          | ... wird ausgelöst ...                                                     |
| -------------------- | -------------------------------------------------------------------------- |
| **`onafterprint`**   | nachdem das Dokument ausgedruckt wurde                                     |
| `**onbeforeprint**`  | bevor das Dokument ausgedruckt wird                                        |
| `**onbeforeunload**` | bevor das Dokument verlassen wird                                          |
| `**onerror**`        | wenn ein Fehler auftritt                                                   |
| `**onhaschange**`    | wenn das Dokument verändert wurde                                          |
| `**onload**`         | wenn die Webseite "fertig" geladen ist                                     |
| `**onmessage**`      | wenn eine Nachricht ausgelöst wurde                                        |
| `**onoffline**`      | wenn die Internetverbindung unterbrochen wurde                             |
| `**ononline**`       | wenn die Internetverbindung hergestellt wurde                              |
| `**onpagehide**`     | wenn das Fenster welches das Dokument anzeigt versteckt wird               |
| `**onpageshow**`     | wenn das Fenster welches das Dokument anzeigt sichtbar wird                |
| `**onpopstate**`     | wenn sich die Historie des Fensters ändert                                 |
| `**onredo**`         | wenn das Dokument einen Vorgang "Nochmals tun" ausführt                    |
| `**onresize**`       | wenn die Größe des Browserfensters verändert wird                          |
| `**onstorage**`      | wenn eine gespeicherte Webseite aktualisiert wird                          |
| `**onundo**`         | wenn das Dokument einen Vorgang "Rückgängig machen" ausführt               |
| `**onunload**`       | wenn das Dokument verlassen wurde oder das Browserfenster geschlossen wird |
|                      |                                                                            |

---

Mausereignisse

| Ereignis...        | ... wird ausgelöst ...                                   |
| ------------------ | -------------------------------------------------------- |
| **`onclick`**      | bei einem Mausklick auf das Element                      |
| `**ondbclick**`    | bei einem Maus-Doppelklick auf das Element               |
| `**ondrag**`       | wenn das Element mit der Maus gezogen wird               |
| `**ondragend**`    | beim Beenden des Drag-Vorgangs                           |
| `**ondragenter**`  | wenn eine Element auf ein Zielelement gezogen wurde      |
| `**ondragleave**`  | wenn ein Element das Zielelement verlässt                |
| `**ondragstart**`  | beim Beginn eines Drag-Vorgangs                          |
| `**ondrop**`       | wenn das gezogene Element fallen gelassen wird           |
| `**onmousedown**`  | wenn die Maustaste auf einem Element gedrückt wird       |
| `**onmousemove**`  | wenn der Mauszeiger sich über ein Element bewegt         |
| `**onmouseout**`   | wenn der Mauszeiger sich aus einem Element heraus bewegt |
| `**onmousover**`   | wenn sich der Mauszeiger über einem Element bewegt       |
| `**onmouseup**`    | wenn die Maustaste losgelassen wird                      |
| `**onmousewheel**` | wenn das Mausrad betätigt wird                           |
| `**onscroll**`     | wenn der Scrollbalken eines Elements bewegt wird         |

---

Tastaturereignisse

| Ereignis...      | ... wird ausgelöst ...              |
| ---------------- | ----------------------------------- |
| **`onkeydown`**  | der Nutzer eine Taste gedrückt hält |
| `**onkeypress**` | wenn der Nutzer eine Taste drückt   |
| `**onkeyup**`    | wenn der Nutzer eine Taste loslässt |

---

Formularereignisse

| Ereignis...         | ... wird ausgelöst ...                                                           |
| ------------------- | -------------------------------------------------------------------------------- |
| **`onblur`**        | in dem Moment wenn eine Element den Fokus verliert                               |
| `**onchange**`      | in dem Moment wenn sich der Wert eines Elementes ändert                          |
| `**oncontextmenu**` | wenn eine Kontextmenü ausgelöst wird (nicht unterstützt in den meisten Browsern) |
| `**onfocus**`       | wenn eine Element den Fokus erhält                                               |
| `**onformchange**`  | wenn sich ein Formular verändert                                                 |
| `**onforminput**`   | wenn das Formular mit Nutzerinhalten gefüllt wird                                |
| `**oninput**`       | wenn ein Element mit Nutzerinhalten gefüllt wird                                 |
| `**oninvalid**`     | wenn ein Element ungültig ist                                                    |
| `**onselect**`      | nachdem Text in einem Element ausgewählt wurde                                   |
| `**onsubmit**`      | ein Formular abgeschickt wird                                                    |

---

Medienereignisse

| Ereignis...            | ... wird ausgelöst ...                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **`onabort`**          | wenn das Laden von Medieninhalten abgebrochen wird                                                                             |
| `**oncanplay**`        | wenn eine Datei fertig zum Abspielen ist (d.h. der Buffer bis zu einer bestimmten Größe geladen wurde)                         |
| `**oncanplaytrough**`  | wenn eine Datei komplett im Buffer geladen ist und ohne Unterbrechungen bis zum Ende abgespielt werden kann                    |
| `**ondurationchange**` | wenn sich die Laufzeit verändert                                                                                               |
| `**onemptied**`        | wenn etwas unvorhergesehenes passiert ist und die Datei nicht abspielbereit ist (zum Beispiel Abbruch der Internetverbindung). |
| `**onended**`          | wenn der Abspielvorgang das Ende der Datei erreicht hat                                                                        |
| `**onerror**`          | wenn eine Fehler beim Laden einer Mediendatei oder eines Medienstreams ausgetreten ist.                                        |
| `**onloadeddata**`     | wenn das gezogene Element fallen gelassen wird                                                                                 |
| `**onloadedmetadata**` | wenn Metadaten (Abspieldauer, Format, etc.) geladen wurden                                                                     |
| `**onloadstart**`      | in dem Moment wenn eine Datei beginnt zu laden                                                                                 |
| `**onpause**`          | wenn der Nutzer oder ein Programm die Abspielung anhält                                                                        |
| `**onplay**`           | wenn der Medieninhalt bereit zum Abspielen ist                                                                                 |
| `**onplaying**`        | wenn mit dem Abspielen gerade begonnen wurde                                                                                   |
| `**onprogress**`       | wenn der Browser die Medieninhalte lädt                                                                                        |

---

Medienereignisse

| Ereignis...              | ... wird ausgelöst ...                                                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| **`onratechange`**       | jedesmal wenn die Abspielrate verändert wird                                                                                          |
| `**onreadystatechange**` | wenn sich der "Ready State" einer Übertragung verändert                                                                               |
| `**onseeked**`           | wenn das Seeking-Attribut auf false gesetzt wurde                                                                                     |
| `**onseeking**`          | wenn das Seeking-Attribut auf true gesetzt wurde                                                                                      |
| `**onstalled**`          | wenn der Browser den Inhalt nicht laden kann                                                                                          |
| `**onsuspend**`          | wenn das Laden von Inhalten vorzeitig abgebrochen wurde                                                                               |
| `**ontimeupdate**`       | wenn sich die Abspielposition verändert hat                                                                                           |
| `**onvolumechanged**`    | wenn sich der Lautstärkepegel geändert hat                                                                                            |
| `**onwaiting**`          | wenn die Medienabspielung angehalten wurde, aber fortgesetzt werden soll (zum Beispiel bei Unterbrechung durch Leerlaufen des Buffer) |















## 3.4 e.target

```js
1
let submit = document.querySelector("[type=submit]");
submit.addEventListener("click",
    function (e) {
        e.preventDefault();
    },
    false);




2
let form = document.forms[0];

form.addEventListener("blur",
    function (e) {
        console.log(e.target);
        let error = e.target.validity;
        console.log(error);
        console.log(error.valid);

        if (error) {
            //Fehlermeldung schicken und Feld übergeben
            console.log(hasError(e.target));
        }
        if (error.valid) // 当全部的 feld 检验都正确了 
            deleteMessage();  // 这是一个自定义的function 
    },
    // propagation umkehren
    true);
```

### 3.4.1 e.target 和 this 的区别
this 是事件绑定的元素， 这个函数的调用者（绑定这个事件的元素）
e.target 是事件触发的元素。


this是事件绑定的元素，这个函数的调用者(绑定这个事件的元素)
e.target是事件触发的元素

```html
<body>
    <div>123</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        // 常见事件对象的属性和方法
        // 1. e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）
        // 区别 ： e.target 点击了那个元素，就返回那个元素 this 那个元素绑定了这个点击事件，那么就返回谁
        var div = document.querySelector('div');
        div.addEventListener('click', function(e) {
            console.log(e.target);
            console.log(this);

        })
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
                // 我们给ul 绑定了事件  那么this 就指向ul  
                console.log(this);
                console.log(e.currentTarget);

                // e.target 指向我们点击的那个对象 谁触发了这个事件 我们点击的是li e.target 指向的就是li
                console.log(e.target);

            })
            // 了解兼容性
            // div.onclick = function(e) {
            //     e = e || window.event;
            //     var target = e.target || e.srcElement;
            //     console.log(target);

        // }
        // 2. 了解 跟 this 有个非常相似的属性 currentTarget  ie678不认识
    </script>
</body>

```


# 4 常见的鼠标事件
|鼠标事件	|触发条件|
|--|---|
|onclick	|鼠标点击左键触发|
|onmouseover	|鼠标经过触发|
|onmouseout	|鼠标离开触发|
|onfocus	|获得鼠标焦点触发|
|onblur	|失去鼠标焦点触发|
|onmousemove	|鼠标移动触发|
|onmouseup	|鼠标弹起触发|
|onmousedown	|鼠标按下触发|

新的写法

|鼠标事件	|触发条件|
|--|--- |
|click	|鼠标点击左键触发|
|mouseover	|鼠标经过触发|
|mouseout	|鼠标离开触发|
|focus	|获得鼠标焦点触发|
|blur	|失去鼠标焦点(就是 鼠标离开这个 feld 了) 的时候 触发|
|mousemove	|鼠标移动触发|
|mouseup	|鼠标弹起触发|
|mousedown	|鼠标按下触发|
|change|it doesn't fire unnecessarily when the user clicks an already-selected radio.|
| formdata | The formdata event fires after the entry list representing the form's data is constructed. This happens when the form is submitted, but can also be triggered by the invocation of a FormData()  constructor. |

## 4.1 禁止鼠标右键与鼠标选中
contextmenu主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单
selectstart 禁止鼠标选中

```html
<body>
    <h1>我是一段不愿意分享的文字</h1>
    <script>
        // 1. contextmenu 我们可以禁用右键菜单
        document.addEventListener('contextmenu', function(e) {
                e.preventDefault(); // 阻止默认行为
            })
            // 2. 禁止选中文字 selectstart
        document.addEventListener('selectstart', function(e) {
            e.preventDefault();

        })
    </script>
</body>

```


## 4.2 鼠标事件对象
event对象代表事件的状态，跟事件相关的一系列信息的集合
现阶段我们主要是用鼠标事件对象 MouseEvent 和键盘事件对象 KeyboardEvent。

|鼠标事件对象	|说明|
|---|---|
|e.clientX	|返回鼠标相对于浏览器窗口可视区的X坐标|
|e.clientY	|返回鼠标相对于浏览器窗口可视区的Y坐标|
|e.pageX（重点）|	返回鼠标相对于文档页面的X坐标 IE9+ 支持|
|e.pageY（重点）|	返回鼠标相对于文档页面的Y坐标 IE9+ 支持|
|e.screenX	|返回鼠标相对于电脑屏幕的X坐标|
|e.screenY	|返回鼠标相对于电脑屏幕的Y坐标|

```html
<body>
    <script>
        // 鼠标事件对象 MouseEvent
        document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.clientX);
            console.log(e.clientY);
            console.log('---------------------');

            // 2. page 鼠标在页面文档的x和y坐标
            console.log(e.pageX);
            console.log(e.pageY);
            console.log('---------------------');

            // 3. screen 鼠标在电脑屏幕的x和y坐标
            console.log(e.screenX);
            console.log(e.screenY);

        })
    </script>
</body>
```


# 5 常用的键盘事件
|键盘事件	触发条件|
|----|----|
|keyup	|某个键盘按键被松开时触发|
|keydown	|某个键盘按键被按下时触发|
|keypress	|某个键盘按键被按下时触发，但是它不识别功能键，比如 ctrl shift 箭头等|


如果使用addEventListener 不需要加 on
onkeypress 和前面2个的区别是，它不识别功能键，比如左右箭头，shift 等
三个事件的执行顺序是： keydown – keypress — keyup

```html
<body>
    <script>
        // 常用的键盘事件
        //1. keyup 按键弹起的时候触发 
        // document.onkeyup = function() {
        //         console.log('我弹起了');

        //     }
        document.addEventListener('keyup', function() {
            console.log('我弹起了');
        })

        //3. keypress 按键按下的时候触发  不能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keypress', function() {
                console.log('我按下了press');
            })
            //2. keydown 按键按下的时候触发  能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keydown', function() {
                console.log('我按下了down');
            })
            // 4. 三个事件的执行顺序  keydown -- keypress -- keyup
    </script>
</body>
```



## 5.1 键盘对象属性
|键盘事件对象 属性|	说明|
|--|--|
|keyCode	|返回该键值的ASCII值. 已经废弃. event.keyCode === 1|
|key	|现在使用这个 event.key === 'Enter'|

keydown和 keyup 不区分字母大小写，keypress 区分字母大小写。
在我们实际开发中，我们更多的使用keydown和keyup， 它能识别所有的键（包括功能键）
Keypress 不识别功能键，但是keyCode属性能区分大小写，返回不同的ASCII值

```html
<body>
    <script>
        // 键盘事件对象中的keyCode属性可以得到相应键的ASCII码值
        // 1. 我们的keyup 和keydown事件不区分字母大小写  a 和 A 得到的都是65
        // 2. 我们的keypress 事件 区分字母大小写  a  97 和 A 得到的是65
        document.addEventListener('keyup', function(e) {
            console.log('up:' + e.keyCode);
            // 我们可以利用keycode返回的ASCII码值来判断用户按下了那个键
            if (e.keyCode === 65) {
                alert('您按下的a键');
            } else {
                alert('您没有按下a键')
            }

        })
        document.addEventListener('keypress', function(e) {
            console.log('press:' + e.keyCode);
        })
    </script>
</body>

```


# 6 注册事件(绑定事件)
https://vfhwebp.eduloop.de/loop/Aufbau_eine_js-scripts

给元素添加事件，称为注册事件或者绑定事件。

注册事件有两种方式：传统方式和方法监听注册方式

|传统注册方式|	方法监听注册方式|
|---|--|
|利用 on 开头的事件 onclick	|w3c 标准推荐方式|
| `<button onclick = "alert("hi")"></button>` | addEventListener() 它是一个方法|
|btn.onclick = function() {}	|IE9 之前的 IE 不支持此方法，可使用 attachEvent() 代替|
|特点：注册事件的唯一性|	特点：同一个元素同一个事件可以注册多个监听器|
|同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数	|按注册顺序依次执行|
## 6.1 Event Listener

不用 Event Listener doe muss die ganze  Zeit überprüft, ob etwas passiert ist. 

Ein Event Listener ist eine Funktion in JavaScript, die verwendet wird, um auf bestimmte Ereignisse (Events) zu reagieren, die im DOM auftreten. Der Event Listener „lauscht“ auf das Auftreten eines bestimmten Ereignisses und führt dann eine bestimmte Aktion aus, wenn das Ereignis eintritt, ==ohne dass der Code die ganze Zeit überprüft, ob etwas passiert ist.== Stattdessen wird der Event Listener nur dann aktiv, wenn das definierte Ereignis auftritt.


Die addEventListener-Methode ist die gebräuchlichste Art, Event Listener zu einem Element hinzuzufügen, da sie mehrere Listener für das gleiche Ereignis unterstützt und die Handhabung von Events flexibel und sauber gestaltet.

### 6.1.1 Vorteile der Verwendung von addEventListener

1  Mehrere Listener

Man kann mehrere Event-Listener für dasselbe Ereignis und dasselbe Element hinzufügen, was mit dem direkten Attribut wie onclick oder onmouseover nicht möglich ist.

Wenn man mehrere onclick-Handler direkt über die Eigenschaft onclick zuweit, überschreibt der letzte Handler die vorherigen. Es kann also nur ein Handler gleichzeitig aktiv sein:

```js
const button = document.getElementById("myButton");

// Erster Handler
button.onclick = function() {
    console.log("Erster Klick-Handler");
};

// Zweiter Handler überschreibt den ersten
button.onclick = function() {
    console.log("Zweiter Klick-Handler");
};
```

---


2 Entfernen von Listenern
Mit removeEventListener kann man einen bestimmten Event Listener auch wieder entfernen.

Beispiel mit benannter Funktion:
```js
const button = document.getElementById("myButton");

// Handler-Funktion definieren
function handlerFunktion() {
    console.log("Button wurde geklickt!");
}

// Event-Listener hinzufügen
button.addEventListener("click", handlerFunktion);

// Event-Listener entfernen
button.removeEventListener("click", handlerFunktion);
```
In diesem Fall wird der click-Event-Handler erfolgreich entfernt, da die gleiche handlerFunktion verwendet wurde.



Beispiel mit anonymer Funktion (nicht entfernbar):
```js
const button = document.getElementById("myButton");

// Anonyme Funktion als Event-Handler
button.addEventListener("click", function() {
    console.log("Button wurde geklickt!");
});

// Versuch, den Event-Listener zu entfernen (funktioniert nicht!)
button.removeEventListener("click", function() {
    console.log("Button wurde geklickt!");
});
```

==Hier funktioniert das Entfernen nicht==, da die anonyme Funktion, die in addEventListener verwendet wurde, nicht dieselbe ist wie die in removeEventListener.
- Wenn man eine Funktion zuweist, wird ihre Referenz (Adresse im Speicher) gespeichert.
- Beim Entfernen eines Event-Listeners sucht removeEventListener nach genau dieser Referenz. Wenn die Referenz nicht übereinstimmt, findet der Browser den Event-Handler nicht und kann ihn daher nicht entfernen.




## 6.2 传统方式 : Direkt im HTML-Code:


- Einrichten des Event Listener durch Ereignis-Attribut des jeweiligen Elements
- Bei einem Ereignis auf dem Element wird hinterlegte Funktion aufgerufen
- Vermischung von JavaScript und HTML
- Nur auf HTML-Elemente anwendbar
- Jeweils nur ein Event Listener pro Ereignistyp und Element


```html
<button onclick="alert('Button wurde geklickt!')">Klick mich</button>
```


```html
<div style="background-color: yellow; width: 200px; height: 200px;" 
		 onmouseover="this.style.backgroundColor = 'blue';" 
		 onmouseout="this.style.backgroundColor = 'yellow'">
</div>
```

```html 
<!-- vorheriges HTML -->
<button onclick="changeColor()">
  Farbe ändern
</button>

<script>
  function changeColor() {
    //Funktionslogik
  }
</script>
```

## 6.3 传统方式: Über JavaScript im Skriptbereich oder einer separaten Datei:


- Einrichten des Event Listener durch eine Ereignis-Eigenschaft im Objekt, welches das Element repräsentiert
- Jeweils nur ein Event Listener pro Ereignistyp und Element - ==bei Registrierung mehrerer Event Listener werden vorherige überschrieben==


```js
<script>
	const myBtn = document.getElementById("meinButton");
	myBtn.onclick = function() {
	  alert("Button wurde geklickt!");
	};
</script>

<script>
	const myDiv = document.getElementById("exampleDiv");
	myDiv.onmouseover = function() {
    myDiv.style.backgroundColor = 'blue';
	};
	myDiv.onmouseout = function() {
    myDiv.style.backgroundColor = 'yellow';
	};
</script>



--------------------

var element=document.getElementById("eineID");
element.onmouseover=function() {/*Funktionslogik*/};

var element=document.getElementById("eineID");
element.onmouseover=changeColor;
function changeColor() {
  //Funktionslogik
}


```


```html
<!-- vorheriges HTML -->
<button onclick="changeColor(event)">
  Farbe ändern
</button>

<script>
  function changeColor(evt) {
    //Funktionslogik
  }
</script>
```


```js
var element=document.getElementById("eineID");
element.onmouseover=function(evt) {/*Funktionslogik*/};
```


```js
let element=document.getElementById("but01");
element.addEventListener("click", changeColor);
element.addEventListener("click", changeText);
  
function changeColor(evt) {
  //Funktionslogik
};
  
function changeText(evt) {
  //Funktionslogik
}
```



## 6.4 addEventListener事件监听方式

https://www.runoob.com/jsref/met-document-addeventlistener.html
https://www.cnblogs.com/embrace-ly/p/10570052.html

eventTarget.addEventListener()方法将指定的监听器注册到 eventTarget（目标对象）上
当该对象触发指定的事件时，就会执行事件处理函数

Die Methode addEventListener lauscht auf ein bestimmtes Event und ruft bei Eintritt des events eine Funktion auf. 

- Verknüpfung zwischen Element und Event Listener mittels der Methode `**addEventListener()**` auf dem jeweiligen Element
- Erster Parameter bezeichnet die Art des Events (ohne den Präfix "`**on**`")
    - Erster Parameter des Event Listener referenziert ein `**event**`-Objekt, das beim Aufruf des Listener durch die Laufzeitumgebung übergeben wird
- Zweiter Parameter enthält die Referenz des Event Listener
    - Übergabeparameter muss nicht notwendigerweise im Funktionskopf deklariert werden
- Erster Parameter des Event Listener ist eine Referenz auf ein Objekt vom Typ `**Event**`, welches weitere Informationen über das Event liefert
- Beispiel: `**currentTarget**` von Event bezeichnet das Element auf das sich das Ereignis bezieht (siehe nächste Folie)

syntax
```js
eventTarget.addEventListener(typeOfevent,eventFunction,[useCapture])
addEventListener("event",Funktionsreferenz,capture)
addEventListener("event", anonyme Funktion als Wrapper für Funktionsaufrufe, captures)
```


该方法接收三个参数：
- typeOfevent: 事件类型字符串，比如click,mouseover,注意这里不要带on
- eventFunction：事件处理函数，事件发生时，会调用该监听函数
- useCapture：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习
    - 如果是 true，表示在事件捕获阶段调用事件处理程序；  就是从 最祖先的 element 到 目前的element
    - 如果是 false (不写默认就是false),表示在事件冒泡阶段调用事件处理程序, 就是 目前的element 上升到 祖先的element 

```html
<body>
    <button>传统注册事件</button>
    <button>方法监听注册事件</button>
    <button>ie9 attachEvent</button>
    <script>
        var btns = document.querySelectorAll('button');
        // 1. 传统方式注册事件
        btns[0].onclick = function() {
            alert('hi');
        }
        btns[0].onclick = function() {
                alert('hao a u');
            }
            // 2. 事件监听注册事件 addEventListener 
            // (1) 里面的事件类型是字符串 所以加引号 而且不带on
            // (2) 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
        btns[1].addEventListener('click', function() {
            alert(22);
        })
        btns[1].addEventListener('click', function() {
                alert(33);
            })
            // 3. attachEvent ie9以前的版本支持
        btns[2].attachEvent('onclick', function() {
            alert(11);
        })
    </script>
</body>

```



```js
<!-- vorheriges HTML -->
<button id="but01">
  Farbe ändern
</button>
<!-- weiteres HTML -->

<script>
  let element=document.getElementById("but01");
  element.addEventListener("click", changeColor);
  element.addEventListener("click", changeText);
  
  function changeColor() {
    //Funktionslogik
  };
  
  function changeText() {
    //Funktionslogik
  }
</script>
```


### 6.4.1 添加多个事件

您可以在文档中添加许多事件，添加的事件不会覆盖已存在的事件。
document.addEventListener("click", myFunction);
document.addEventListener("click", someOtherFunction);

您可以在文档中添加不同类型的事件: 
document.addEventListener("mouseover", myFunction);
document.addEventListener("click", someOtherFunction);
document.addEventListener("mouseout", someOtherFunction);

### 6.4.2 使用 函数引用, 函数调用 , 匿名函数的 区别

```js
eventTarget.addEventListener(typeOfevent,eventFunction,[useCapture])
addEventListener("event",Funktionsreferenz,capture)
addEventListener("event", anonyme Funktion als Wrapper für Funktionsaufrufe, captures)
```

```js
p.addEventLoistener("click", myFunction)  //Referenz
p.addEventLoistener("click", myFunction()) //Aufruf und sofortige einmalige Abarbeitung
p .addEventListener("click",
   function(event){  // anonyme Funktion als Wrapper für Funktionsaufrufe
    add(p1,p2);  
    e.preventDefault();            
    e.stopPropagation(); // stop 停止  Propagation 传播
        
})

```

Das Problem mit der Referenzierung ist, daß so keine Argumente an die Funktion übergeben werden können
Man behilft sich mit einer Wrapper-Funktion, die anonym ist, weil sie sofort aufgerufen wird und deshalb keinen Namen benötigt. Über die anonyme Funktion können wir auch gleich auf das event zugreifen, sofern wir der Funktion einen Parameter geben.

使用 函数引用, 或者 匿名函数 是对的 

- 使用 函数引用, : showallElements: 
    - 当 click 这个p 标签 的时候, 才会运行 showallElements funktion. 而且之后点击 p 标签， showallElements 这个funtion, 也会被运行。 而且可以运行多次 
    - 因为  showallElements 代表的是 该函数的 储存地址, 而不是函数结果 
    - Das Problem mit der Referenzierung ist, daß so keine Argumente an die Funktion übergeben werden können
- 使用 匿名函数 function(event){ add(p1,p2); e.preventDefault();}      (anonyme Funktion als Wrapper für Funktionsaufrufe)
    - Man behilft sich mit einer Wrapper-Funktion, die anonym ist, weil sie sofort aufgerufen wird und deshalb keinen Namen benötigt. 
    - Über die anonyme Funktion können wir auch gleich auf das event zugreifen, sofern wir der Funktion einen Parameter geben.
- 使用 函数调用:  showallElements (): 
    - Aufruf und sofortige einmalige Abarbeitung
    - 页面一旦加载,  showallElements funktion 就被运行, 不管你有没有点击 p 标签 , 而且之后点击 p 标签， showallElements 这个funtion, 也不会在被运行了。 一次都不会被运行， 怎么click 都没有用. 
    - 因为  showallElements () 代表的是函数结果 

用 引用函数 或者 匿名函数 (action 发生后 才会执行 funktion)
```js
    // Mit click auf p soll die folgende Funktion ausgeführt werden.
    function showAllElements(){
        for(let i=0; i<document.body.childNodes.length; i++){
            console.log(document.body.childNodes[i]);
        }
    }
    // Funktionsreferenz, damit die Funktion auf click aufgerufen werden kann.
    p.addEventListener("click",showAllElements);
```


```js
 document.getElementById("btn").addEventListener("click",
   function(){
     add(p1,p2);
   })
// 若直接传add(p1,p2),不需要点击，直接显示运算结果。

```

### 6.4.3 useCapture
为什么是 propagation: Das event wird hochgereicht und man bezeichnet das als propagation. 
- useCapture：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习
    - 如果是 false (不写默认就是false), 表示在事件冒泡阶段 (propagation phase) 调用事件处理程序, 就是 目前的element 上升到 祖先的element     (von Kind zu Vorfahren weitergegeben.  )
    - 如果是 true，表示在事件捕获阶段调用事件处理程序；  就是从 最祖先的 element 到 目前的element. (von Vorfahren zu Nachfahren.)

useCapture= false, 就是先在element本身处理 这个event, 然后再往上升 , 这个 funktion 再在 vorfahren 中 被 abgearbeitet  (  Immer wenn eine Funktion auf ein event hin abgearbeitet wird, dann werden auch die Funktionen auf dasselbe event in allen Vorfahren abgearbeitet. )
Das event wird hochgereicht und man bezeichnet das als propagation. 
Gesteuert wird das über den dritten Parameter in der Methode addEventListener(). 
- Dabei ist false der default und die events werden von Kind zu Vorfahren weitergegeben. 
- Mit dem Wert true kehrt sich die Reihenfolge um, von Vorfahren zu Nachfahren.

Über das event aus der anonymen Funktion können wir mit der Methode stopPropagation() dieses Verhalten unterbinden.

### 6.4.4 mit this

```js
<script>
	const myDiv = document.getElementById("exampleDiv");
	myDiv.addEventListener("mouseover", function() {
		// "this" funktioniert auch und verweist auf das Element
		this.style.backgroundColor = "blue";
	});
	// mit Lambda-Funktionen funktioniert "this" nicht
	myDiv.addEventListener("mouseout", function() {
		this.style.backgroundColor = "yellow";
	});
</script>
```


## 6.5 attachEvent事件监听方式(兼容)
- eventTarget.attachEvent()方法将指定的监听器注册到 eventTarget（目标对象） 上
- 当该对象触发指定的事件时，指定的回调函数就会被执行

eventTarget.attachEvent(eventNameWithOn,callback)
该方法接收两个参数：
eventNameWithOn：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on
callback： 事件处理函数，当目标触发事件时回调函数被调用
ie9以前的版本支持

## 6.6 注册事件兼容性解决方案
兼容性处理的原则：首先照顾大多数浏览器，再处理特殊浏览器
```js
 function addEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 addEventListener 方法
      if (element.addEventListener) {
        element.addEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.attachEvent) {
        element.attachEvent('on' + eventName, fn);
      } else {
        // 相当于 element.onclick = fn;
        element['on' + eventName] = fn;
 } 

```



# 7 Eventhandler的例子 with addEventListener

HTML Online Editor: [https://www.w3schools.com/html/tryit.asp?filename=tryhtml_editor](https://www.w3schools.com/html/tryit.asp?filename=tryhtml_editor)

直接用这个 来 显示 效果 

## 7.1 
```js

<script>
	const myBtn = document.getElementById("meinButton");
	myBtn.addEventListener("click", function() {
	  alert("Button wurde geklickt!");
	});
</script>

<script>
	const myDiv = document.getElementById("exampleDiv");
	myDiv.addEventListener("mouseover", function() {
		myDiv.style.backgroundColor = "blue";
	});
	myDiv.addEventListener("mouseout", () => {
		myDiv.style.backgroundColor = "yellow";
	});
</script>

```

## 7.2 点击图片 来更换图片的颜色
```js
// Ändern von Attributen
const pic = document.querySelector("img");
// console.log(pic);
function changeImage(){
    // console.log(pic.alt, pic.src);
    if(pic.alt === "Die Sonne :-)"){
        pic.src = "pics/sonneSad.jpg"
        pic.alt = "Die Sonne :-(";
    }
    else{
        pic.src = "pics/sonne.png";
        pic.alt = "Die Sonne :-)";
    }
}
// changeImage();

pic.addEventListener("click",changeImage,false);
//    addEventListener("event",Funktionsreferenz, Propagation)

// styles manipulieren über die class
const changeStyle = () => pic.classList.toggle("invert");
pic.addEventListener("mouseover", changeStyle, false);
```

## 7.3 点击 reset 按钮以后, 页面要reload

不然默认默认状态下, 点击 reset 按钮以后, 
- 页面不会reload, 
    - 导入 一些通过 js script 填入的元素 依然存在  
- 但是会 把表单中的输入都清零, reset 成空
```js

// Formular auswerten mit submit
const submit = document.querySelector("[type = submit]");
// console.log(submit);
submit.addEventListener("click",
    e => {
        e.preventDefault();
        changePic(moodCheck());
        console.log(form.lastElementChild.nodeName);

        
        if (form.lastElementChild.nodeName !== "P") // Elemente sind immer UPPERCASE, 所以这里用P, 不用小写的p
            feedback(firstName.value);
        else {
            form.lastElementChild.remove();
            feedback(firstName.value);
        }
    });



const reset = document.querySelector("[type=reset]");
// console.log(reset);
reset.addEventListener("click", e => { location.reload() });
```

## 7.4 鼠标event: formdata
https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/formdata_event

The formdata event fires after the entry list representing the form's data is constructed. This happens when the form is submitted, but can also be triggered by the invocation of a FormData() constructor.

This event is not cancelable and does not bubble.

```js
	submit.addEventListener("click", (e) => {
		e.preventDefault();
		new FormData(form);  // 点下 submit 这个按钮, 会根据 form 这个变量中内容,产生一个新的 FormData类型 的 对象. form 在上面被 定义的:  let form = document.forms[0];
	}, false);

	// Vor dem Absenden wäre es sinnvoll nochmals auf die validity aller Felder zu prüfen.
	form.addEventListener( "formdata", (e) => {
		// formdata 这个event 的意思是, 如果 form 中有 formdata 类型的 对象 被产生的话,就执行后面定义的 function 

		console.log("formdata fired");


		console.log(e.formData);  // 如果只是打印e.formData, 则根据显示的结果 e.formData中没有任何表单上 user 自己输入的信息

		let data = e.formData;
		//console.log(data.entries()); // 如果只是打印data.entries(), 显示的结果是, data.entries()中没有任何表单上 user 自己输入的信息

		console.log("-----------------");
		for (let value of data.entries()) {
			console.log(value);  // 打印的结果是, 这种形式 是可以显示 表单上 user 自己输入的信息
		}

	}, false );
```


## 7.5 Radio Button
https://stackoverflow.com/questions/58606047/how-to-use-on-addeventlistener-on-radio-button-in-plain-javascript
best practice in this scenario would be to listen to the "change" event rather than "click", then it doesn't fire unnecessarily when the user clicks an already-selected radio.

```css
<label>
  <input name="contract_duration" type="radio" value="6-Months"/>
  <span>6-Months</span>
</label>

<label>
  <input name="contract_duration" type="radio" value="1-Year"/>
  <span>1-Year</span>
</label>

<label>
  <input name="contract_duration" type="radio" value="2-Years"/>
  <span>2-Years</span>
</label>
```


```js
if (document.querySelector('input[name="contract_duration"]')) {
  document.querySelectorAll('input[name="contract_duration"]').forEach((elem) => {
    elem.addEventListener("change", function(event) {
      var item = event.target.value;
      console.log(item);
    });
  });
}

let contact = document.querySelectorAll('input[name="contract_duration"]');
                                  // or '.your_radio_class_name'

for (let i = 0; i < contact.length; i++) {
  contact[i].addEventListener("change", function() {
    let val = this.value; // this == the clicked radio,
    console.log(val);
  });
}
```

## 7.6 klicken button and a new message shows up 

```js
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Button Beispiel</title>
</head>
<body>

  <!-- Der Button wird hier durch JavaScript hinzugefügt -->

  <script>
    const newBtn = document.createElement("button"); // neuen Button erstellen
    newBtn.textContent = "Klicke mich";
    
    document.body.appendChild(newBtn); // Button zum Body hinzufügen

    // Event-Listener hinzufügen
    newBtn.addEventListener("click", () => {
	     alert("Button wurde geklickt!");
    });
  </script>
  
</body>
</html>
```

![](image/Pasted%20image%2020241211210540.png)

## 7.7 Inhalt verändern

![](image/Pasted%20image%2020241211210649.png)

```js
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beispiel für innerHTML</title>
</head>
<body>

	<div id="content">
		Dies ist der ursprüngliche Inhalt.
	</div>
	<button onclick="changeContent()">Inhalt ändern</button>
	
	<script>
		function changeContent() {
			const element = document.getElementById("content");
      element.innerHTML = "<p>Neuer Inhalt: Dieser Text wurde dynamisch hinzugefügt und befindet sich in einem &lt;p&gt;-Tag.</p>";
    }
  </script>
  
</body>
</html>
```


## 7.8 klicken button and add new element 

![](image/Pasted%20image%2020241211210733.png)

```js
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beispiel für createTextNode</title>
</head>
<body>

	<div>
		<p id="content">Dies ist der ursprüngliche Inhalt.</p>
	</div>
	<button onclick="increment()">Inhalt ändern</button>
	
	<script>
		let counter = 0;
		function increment() {
			counter++;
			if (counter == 1) {
				changeContent();
			} else {
				addListItems();
			}
		}

    const element = document.getElementById("content"); 
    function changeContent() {
	    element.innerText = "Der Inhalt wurde geändert."
	  }

    const uList = document.createElement('ul');
    const myDiv = document.getElementsByTagName("div")[0];
    myDiv.appendChild(uList);
		
		function addListItems() {
			const listItem = document.createElement('li');
			const textNode = document.createTextNode(`Hallo ${counter - 1}!`)
            
      listItem.appendChild(textNode);
      uList.appendChild(listItem);
    }
  </script>
  
</body>
</html>
```


## 7.9 

![](image/Pasted%20image%2020241211210855.png)

```js
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beispiel für getElementsByClassName</title>
    <style>
        .box {
            width: 100px;
            height: 100px;
            background-color: lightgray;
            margin: 10px;
            display: inline-block;
        }
    </style>
</head>
<body>

    <div class="box">Box 1</div>
    <div class="box">Box 2</div>
    <div class="box">Box 3</div>
    <button>Farbe ändern</button>

    <script>
    const myButton = document.getElementsByTagName("button")[0];
    myButton.addEventListener("click", () => {
	    const boxes = document.getElementsByClassName("box");
	    let i = 1; // Zähler
	    
	    // Schleife über die HTMLCollection, um jedes Element zu ändern    
	    for (let box of boxes) {
		    box.style.backgroundColor = "lightblue"; // Farbe ändern
		    box.textContent = `Box ${i} geändert`; // Text ändern
		    i++;
		  }});
    </script>

</body>
</html>
```


## 7.10 mouseover , mouseout, mouseclick

![](image/Pasted%20image%2020241211210921.png)


```js
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beispiel für Event Listener</title>
</head>
<body>
	<div id="yellowDiv" style="background-color: yellow; width: 200px; height: 200px;"></div>
	<br>
 	<p id="message">The div is yellow!</p>
 	
 	<script>
        const yellowDiv = document.getElementById("yellowDiv");
        const message = document.getElementById("message");
        const copiedText = message.innerHTML;
        const copiedColor = yellowDiv.style.backgroundColor;
      
        // div-Listener für Mauszeiger
        yellowDiv.addEventListener("mouseover", () => yellowDiv.style.backgroundColor = "red")
        yellowDiv.addEventListener("mouseover", () => message.innerText = "The div is red!")
        //div.addEventListener("mouseover", () => { div.style.backgroundColor = "red"; message.innerText = "Das div ist rot!";

        // div-Listener für Mauszeiger weg vom div
        function yellowDivAgain() {
            yellowDiv.style.backgroundColor = copiedColor;
            message.innerHTML = copiedText;
        }
        yellowDiv.addEventListener("mouseout", yellowDivAgain);
        
        
        // div-Listener für Klick
        yellowDiv.addEventListener("click", function() {
            yellowDiv.style.backgroundColor = "blue";
            message.textContent = "The div is " + yellowDiv.style.backgroundColor + "!"
        });
        
 </script>

</body>
</html>
```


## 7.11 Button 随机移动

![](image/Pasted%20image%2020241211211102.png)


```js
<!DOCTYPE html>
<html>
<head>
	<title>Einfach ein dummes Beispiel für ein dummes Spielchen</title>
</head>
<body>

	<h1 id="h1">Reveal the secret!<h1>
	<button style="position: absolute;">Click me!</button>

	<script>
	
		const button = document.getElementsByTagName("button")[0];
		const h1 = document.getElementById("h1");
		
	  let counter = 0;

		function doSomeAction() {
		  counter++;
    
	    if (counter == 100) {
		    button.removeEventListener("mouseover", doSomeAction);
	      h1.textContent = "It is time. You have deserved it!"
	    }
        
			let random1 = Math.random() * window.innerHeight;
	    let random2 = Math.random() * window.innerWidth;
	    button.style.top = `${random1}px`;
	    button.style.left = `${random2}px`;
		}
    
		button.addEventListener("mouseover", doSomeAction);
	  button.addEventListener("click", () => alert("Webtech is a bad ass subject and Szymon is the best tutor!!"));  
</script>

</body>
</html>
```


## 7.12 load video 

![](image/Pasted%20image%2020241211211139.png)

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Einfach ein Beispiel für mehrere Sachen zusammengefasst (und bisschen Selbstdarstellung)</title>
	</head>
	<body style="font-family: Arial, Helvetica, sans-serif;">

		<button id="myBtn">Load the video</button>
		
		<div style="display: none;">
			<br>
			<img id="eng" src="https://www.countryflags.com/wp-content/uploads/united-kingdom-flag-png-xl.png" alt="ENG">
			<img id="deu" src="https://www.countryflags.com/wp-content/uploads/germany-flag-png-xl.png" alt="GER">
			<img id="pol" src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/12/Flag_of_Poland.svg/2560px-Flag_of_Poland.svg.png" alt="POL">
			<img id="esp" src="https://cdn.countryflags.com/thumbs/spain/flag-400.png" alt="ESP">
			<img id="ndl" src="https://www.countryflags.com/wp-content/uploads/netherlands-flag-png-xl.png" alt="NDL">
			<img id="ukr" src="https://cdn.countryflags.com/thumbs/ukraine/flag-400.png" alt="UKR">
		</div>
		
		<div style="width: 560px; color: darkblue;">
			<h1 id="heading"></h1>
			<p id="description"></p>
		</div>
	</body>

	<script>
		
		const myBtn = document.getElementById("myBtn");
		const langDiv = document.getElementsByTagName("div")[0];

		const video = document.createElement("iframe");
		video.setAttribute("src", "https://www.youtube.com/embed/6f9ctfWDNGY");
		video.setAttribute("width", "560");
		video.setAttribute("height", "315");

		myBtn.addEventListener("click", () => {
	    document.body.insertBefore(video, langDiv);
	    myBtn.remove();
    	langDiv.removeAttribute("style");
		});

		const heading = document.getElementById("heading");
		const description = document.getElementById("description");
		const images = document.getElementsByTagName("img");
		
		for (let image of images) {
	    image.setAttribute("width", "30");
      image.setAttribute("height", "20");
      image.setAttribute("style", "border: 1px solid black");
    }

		for (let i = 0; i < images.length; i++) {
	    images[i].addEventListener("click", function() {
	      for (let image of images) {
	        image.setAttribute("height", "20");
          image.setAttribute("width", "30");
        }
        heading.innerText = languages[i].title;
	      description.innerText = languages[i].description;
        this.setAttribute("height", "40");
        this.setAttribute("width", "60");
        console.log(languages[i]);
    	});
		}
    
    const languages = [
    	{ language: "ENG", title: "Description:", description: "In this video, Szymon talks about his adventures with learning foreign languages. Weirdo. He has been living in Germany for 10 years and his German still sucks. So, what level must his other languages be at?" },
    	{ language: "DEU", title: "Beschreibung:", description: "In diesem Video erzählt Szymon von seinen Abenteuern beim Lernen von Fremdsprachen. Ein komischer Typ. Er lebt seit 10 Jahren in Deutschland und sein Deutsch ist immer noch Scheiße. Auf welchem Niveau müssen dann seine anderen Sprachen sein?" },
    	{ language: "POL", title: "Opis:", description: "W tym filmie Szymon opowiada o swoich przygodach z nauką języków obcych. Dziwny typ. Od 10 lat mieszka w Niemczech i nadal mówi słabo po niemiecku. Na jakim poziomie musi być w takim razie reszta jego języków?"},
    	{ language: "ESP", title: "Descripción:", description: "En este video, Szymon habla sobre sus aventuras aprendiendo idiomas extranjeros. Un tipo extraño. Lleva 10 años viviendo en Alemania y todavía habla mal alemán. ¿Entonces, en qué nivel estarán sus otros idiomas?" },
    	{ language: "NDL", title: "Beschrijving:", description: "In deze video vertelt Szymon over zijn avonturen met het leren van vreemde talen. Een rare kerel. Hij woont al 10 jaar in Duitsland en spreekt nog steeds slecht Duits. Op welk niveau zouden zijn andere talen dan zijn?" },
    	{ language: "UKR", title: "Oпис:", description: "У цьому відео Шимон розповідає про свої пригоди з вивченням іноземних мов. Дивний тип. Він живе в Німеччині вже 10 років, але досі погано говорить німецькою. То на якому рівні тоді мають бути його інші мови?" }
		];
		
	</script>

</html>
```


# 8 删除事件(解绑事件)

## 8.1 removeEventListener删除事件方式
eventTarget.removeEventListener(type,listener[,useCapture]);

该方法接收三个参数：
type:事件类型字符串，比如click,mouseover,注意这里不要带on
listener：事件处理函数，事件发生时，会调用该监听函数
useCapture：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习

```js
// 向文档添加事件句柄
document.addEventListener("mousemove", myFunction);

// 移除文档的事件句柄
document.removeEventListener("mousemove", myFunction);
```

---

2 Entfernen von Listenern
Mit removeEventListener kann man einen bestimmten Event Listener auch wieder entfernen.

2.1
Beispiel mit benannter Funktion:
```js
const button = document.getElementById("myButton");

// Handler-Funktion definieren
function handlerFunktion() {
    console.log("Button wurde geklickt!");
}

// Event-Listener hinzufügen
button.addEventListener("click", handlerFunktion);

// Event-Listener entfernen
button.removeEventListener("click", handlerFunktion);
```
In diesem Fall wird der click-Event-Handler erfolgreich entfernt, da die gleiche handlerFunktion verwendet wurde.


2.2 
Beispiel mit anonymer Funktion (nicht entfernbar):
```js
const button = document.getElementById("myButton");

// Anonyme Funktion als Event-Handler
button.addEventListener("click", function() {
    console.log("Button wurde geklickt!");
});

// Versuch, den Event-Listener zu entfernen (funktioniert nicht!)
button.removeEventListener("click", function() {
    console.log("Button wurde geklickt!");
});
```

==Hier funktioniert das Entfernen nicht==, da die anonyme Funktion, die in addEventListener verwendet wurde, nicht dieselbe ist wie die in removeEventListener.
- Wenn man eine Funktion zuweist, wird ihre Referenz (Adresse im Speicher) gespeichert.
- Beim Entfernen eines Event-Listeners sucht removeEventListener nach genau dieser Referenz. Wenn die Referenz nicht übereinstimmt, findet der Browser den Event-Handler nicht und kann ihn daher nicht entfernen.



## 8.2 detachEvent删除事件方式(兼容)
eventTarget.detachEvent(eventNameWithOn,callback);

该方法接收两个参数：
eventNameWithOn：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on
callback： 事件处理函数，当目标触发事件时回调函数被调用
ie9以前的版本支持

## 8.3 传统事件删除方式
eventTarget.onclick = null;

事件删除示例：
```html
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs = document.querySelectorAll('div');
        divs[0].onclick = function() {
            alert(11);
            // 1. 传统方式删除事件
            divs[0].onclick = null;
        }
        // 2.removeEventListener 删除事件
        divs[1].addEventListener('click',fn);   //里面的fn不需要调用加小括号

        function fn(){
            alert(22);
            divs[1].removeEventListener('click',fn);
        }
        // 3.IE9 中的删除事件方式
        divs[2].attachEvent('onclick',fn1);
        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick',fn1);
        }
    </script>

</body>
```


## 8.4 删除事件兼容性解决方案
```js
 function removeEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 removeEventListener 方法
      if (element.removeEventListener) {
        element.removeEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.detachEvent) {
        element.detachEvent('on' + eventName, fn);
      } else {
        element['on' + eventName] = null;
 } 
```


# 9 事件对象阻止默认行为 e.preventDefault()
```html
<body>
    <div>123</div>
    <a href="http://www.baidu.com">百度</a>
    <form action="http://www.baidu.com">
        <input type="submit" value="提交" name="sub">
    </form>
    <script>
        // 常见事件对象的属性和方法
        // 1. 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);

        function fn(e) {
            console.log(e.type);

        }
        // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function(e) {
                e.preventDefault(); //  dom 标准写法
            })
            // 3. 传统的注册方式
        a.onclick = function(e) {
            // 普通浏览器 e.preventDefault();  方法
            // e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            // e.returnValue;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            return false;
            alert(11);
        }
    </script>
</body>

```

## 9.1 阻止submit 这个 button 的默认行为

Defautl behavior von Submit: Page neue laden. page neue laden 导致  feld in Form leer machen

Formular sendet die entgegen genommenen Daten an die im action-Attribut spezifizierte Adresse und leert alle Formularfelder. Das ist nicht immer wünschenswert. 
Hat der Anwender z.B. einige Felder ausgefüllt, aber einige nicht richtig, dann muß er nach dem Absenden alle Felder wieder neu ausfüllen. Das ist nicht benutzerfreundlich.

Den Default können wir unterbinden, genauso wie wir den capture-Parameter im addEventListener() unterbunden haben, über das event mit der Methode preventDefault().

```js
{

"use strict";
let submit = document.querySelector(["type=submit"]);
const doSomeThing = (el) => {
 //do something like checking a form
}
submit.addEventListener("click",function(e){
                                  donSomeThing();
                                  e.preventDefault();},false);
}
```


```js
    const submit = document.querySelector("[type=submit]");
    // console.log(submit);

    const test = () => console.log("test");

    //Defautl behavior von Submit: Page neue laden und feld leer machen

    // ohne Unterdrücken des default
    // submit.addEventListener("click",test,false);


    // mit Unterdrücken des default
    submit.addEventListener("click",
        function (e) {
            test();
            console.log(e);  // e 是 event 类型的变量
            e.preventDefault();   //  重点是这句话
        },
        false);
```


```html
<form>
    <fieldset>
        <legend>Kenntnisse</legend>
        <div>
            <label	for="knowhow">Dein Knowhow</label>
            <input	id="knowhow"
                    list="lang"
                    required>
            <datalist	id="lang">
                <option value="JavaScript">
                <option value="CSS">
                <option value="HTML">
            </datalist>
        </div>
    </fieldset>
    <fieldset>
        <legend>Wie ist Deine Stimmung?</legend>
        <div>
            <label	for="good">Super!</label>
            <input	type="radio"
                    id="good"
                    value="g"
                    name="mood"
                    checked>
        </div>
        <div>
            <label	for="bad">Geht so.</label>
            <input	type="radio"
                    id="bad"
                    value="b"
                    name="mood">
        </div>
    </fieldset>
    <div>
        <input type="reset">
        <input type="submit">
    </div>
</form>
```


# 10 阻止事件冒泡 e.stopPropagation()
事件冒泡：开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点
事件冒泡本身的特性，会带来的坏处，也会带来的好处，需要我们灵活掌握。

https://www.jianshu.com/p/919b9e5adb55
https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation

propagation reicht ein event hoch, an alle Vorfahren, die dasselbe event nutzen

The stopPropagation() method of the Event interface prevents further propagation of the current event in the capturing and bubbling phases. It does not, however, prevent any default behaviors from occurring; for instance, clicks on links are still processed. 

根据DOM事件流机制，在元素上触发的大多数事件都会冒泡传递到该元素的所有祖辈元素上，如果这些祖辈元素上也绑定了相应的事件处理函数，就会触发执行这些函数。

使用stopPropagation()函数可以阻止当前事件向祖辈元素的冒泡传递，也就是说该事件不会触发执行当前元素的任何祖辈元素的任何事件处理函数。

该函数只阻止事件向祖辈元素的传播，不会阻止该元素自身绑定的其他事件处理函数的函数。event.stopImmediatePropagation()不仅会阻止事件向祖辈元素的传播，还会阻止该元素绑定的其他(尚未执行的)事件处理函数的执行。

## 10.1 写法

标准写法
e.stopPropagation();

非标准写法： IE6-8 利用对象事件 cancelBubble属性
e.cancelBubble = true;


```html
<body>
    <div class="father">
        <div class="son">son儿子</div>
    </div>
    <script>
        // 常见事件对象的属性和方法
        // 阻止冒泡  dom 推荐的标准 stopPropagation() 
        var son = document.querySelector('.son');
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // stop 停止  Propagation 传播
            e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false);

        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
</body>

```


1 阻止事件冒泡的兼容性解决方案
```js
if(e && e.stopPropagation){
      e.stopPropagation();
  }else{
      window.event.cancelBubble = true;
  }
```



## 10.2 例子

```js
(function init() {
    "use strict";

    const allElements = document.querySelectorAll("*");
    // console.log(allElements);

    const showAll = el => console.log(el);

    for (let i = 0; i < allElements.length; i++) {
        allElements[i].addEventListener("click",
            function (e) {
                showAll(allElements[i]);
                //e.stopPropagation()
            },
            false);
    }

    // propagation reicht ein event hoch, an alle Vorfahren,
    // die dasselbe event nutzen.
    // false und true beeinflussen die Reihenfolge
    // zum Aussetzen: stopPropagation
})();
```

不加上 e.stopPropagation(): 
当前点击的元素的 每个祖先 元素 都会执行一遍 showAll(allElements[i]);
![](image/Chapter04_事件高级_addEventListener_Propagation_01.png)

加上 e.stopPropagation(): 
只有 当前点击的元素的 直接父亲 元素 会执行一遍 showAll(allElements[i]);
![](image/Chapter04_事件高级_addEventListener_Propagation_02.png)


# 11 事件委托
事件委托也称为事件代理，在 jQuery 里面称为事件委派
事件委托的原理: 不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点

```html
<body>
    <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
            // 点了谁，就让谁的style里面的backgroundColor颜色变为pink
        })
    </script>
</body>

```

以上案例：给 ul 注册点击事件，然后利用事件对象的 target 来找到当前点击的 li，因为点击 li，事件会冒泡到 ul 上， ul 有注册事件，就会触发事件监听器。


