

# 1 Document 

Das document in z.B. const element = document.getElementById("irgendeineId"); bezieht sich auf das Document Object Model (DOM) des aktuell geladenen HTML-Dokuments in der Webseite.

Bedeutung von document:
- document ist ein globales Objekt in JavaScript, das den gesamten Inhalt des HTML-Dokuments repräsentiert.
- Es ermöglicht den Zugriff auf alle Elemente und Inhalte der Seite und stellt eine Schnittstelle bereit, um Elemente auszuwählen, zu manipulieren, Ereignisse zu verwalten und neue Inhalte hinzuzufügen.
- Im Wesentlichen ist document die Wurzel des DOM und gibt dir Zugriff auf die gesamte Struktur der Seite, wie in der HTML-Datei definiert. 
- `document.getElementById("irgendeineId")`: Hier ruft `document` die Methode `getElementById()` auf, um ein Element mit der ID `irgendeineId` im HTML-Dokument zu finden. 
-  `const element` : Das gefundene Element Wird dann in der Konstanten element gespeichert, sodass man später in deinem Code darauf zugreifen und es bearbeiten kann.


# 2 DOM操作总览
对于DOM操作，我们主要针对子元素的操作，主要有

创建
增
删
改
查
属性操作
时间操作

DOM kann für folgende Funktionen im Programmcode verwendet werden:
- Veränderung des Seiteninhaltes
- Erstellung kompletter Dokumente
- Navigation durch ein Dokument (sowohl durch Inhalt als auch durch Strukturierung)
- Löschen und Einfügen von Elementen
- Veränderung der Eigenschaften der Elemente

1创建
document.write
innerHTML
createElement

2 增
appendChild
insertBefore

3 删
removeChild

4  改
主要修改dom的元素属性，dom元素的内容、属性、表单的值等
修改元素属性：src、href、title 等
修改普通元素内容：innerHTML、innerText
修改表单元素：value、type、disabled
修改元素样式：style、className

5  查
主要获取查询dom的元素
DOM提供的API方法：getElementById、getElementsByTagName (古老用法，不推荐)
H5提供的新方法：querySelector、querySelectorAll (提倡)
利用节点操作获取元素：父(parentNode)、子(children)、兄(previousElementSibling、nextElementSibling) 提倡

6 属性操作
主要针对于自定义属性
setAttribute：设置dom的属性值
getAttribute：得到dom的属性值
removeAttribute：移除属性


# 3 获取元素 Auffinden-Methoden in document


## 3.1 方法总览

DOM在我们实际开发中主要用来操作元素。
我们如何来获取页面中的元素呢?

获取页面中的元素可以使用以下几种方式:
 - 根据 ID 获取
 - 根据标签名获取
 - 通过 HTML5 新增的方法获取
 - 特殊元素获取

>Die meisten Eigenschaften von document liefern ein Objekt vom Typ HTMLCollection
>Elemente sind beginnend mit 0 indiziert


![](image/Pasted%20image%2020241208212000.png)

| x                                                      | x                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| document.getElementById("wertDerId")                   | Diese Methode greift auf das Element im HTML-Dokument zu, welches eine id mit dem entsprechenden Wert besitzt. <br>                                                                                                                                                          |
| document.getElementsByTagName("elementBezeichner")     | Diese Methode greift auf eine Nodelist von allen Elementen zu, die als Argument übergeben werden. Z.B. alle` <p>` oder alle `<img>.`  <br>                                                                                                                                   |
| document.getElementsByClassName("wertImAttributClass") | Diese Methode greift ebenfalls auf eine Nodelist zu, nämlich alle Elemente, die das Attribut class. mit einem bestimmten in der Parameterliste spezifizierten Wert besitzen.  <br>gibt eine Sammlung (HTMLCollection) von Elementen mit einer bestimmten Klasse zurück. <br> |
| document.getElementsByName("wertImAttributName")       | Diese Methode wird in Formularen verwendet, gibt auch eine Nodelist wieder und bezieht sich auf alle Elemente, die das name. Attribut verwenden, mit dme entsprechenden Wert.                                                                                                |
| document.querySelectorAll("jederBeliebigeCSSselektor") | Auch mit dieser Methode bekommen wir eine Nodelist, nämlich alle Elemente, die mit dem in der Parameterliste spezifizierten Selektor angesprochen werden können.                                                                                                             |
| document.querySelector("jederBeliebigeCSSselektor")    | Diese Methode greift nur das erste Element welches den entsprechenden CSS-Selektor verwenden könnte.                                                                                                                                                                         |



## 3.2 使用不同方法, 其返回值的类型不同


Einzelne Elemente (object):
- getElementById()
- getElementByQuerySelector()

Listen von Elementen:
- getElementsByTagName()
- getElementsByClassName()
- getElementsByName()
- getElementsByQuerySelectorAll()


### 3.2.1 Einzelne Elemente (object)

Die id finden Sie im HTML-Dokument
```js
const inc = document.getElementById("include");
console.log(inc);
console.log(typeof inc);
console.log(inc.id);
console.log(inc.innerHTML);
console.log(inc.childNodes);
```

Für den QuerySelector 
kann man jeden gültigen CSS-Selektor einsetzen.
```js
const code = document.querySelector("article:first-of-type code");
console.log(code, typeof code);
// ginge auch einfacher, hier nur "code" :-)
```

    

### 3.2.2 Listen von Elementen
```js
 const h2 = document.getElementsByTagName("h2");
console.log(h2);

const heading = document.getElementsByClassName("heading");
console.log(heading[0].innerHTML);

const allP = document.querySelectorAll("p");
console.log(allP);

const allRadio = document.getElementsByName("comprehension");
console.log(allRadio);

for(let i=0; i<allRadio.length; i++){
    console.log(allRadio[i].checked);
}
```
   



## 3.3 获取特殊元素 document.XX
1 获取body元素
返回body元素对象: document.body;

2 获取html元素
返回html元素对象: document.documentElement;

3 获取forms元素
const forms = document.forms;
const form = document.forms[0];




## 3.4 根据ID获取 getElementByld()

findet ein Element anhand seiner ID.
返回 一个 element 
使用 getElementByld() 方法可以获取带ID的元素对象 doucument.getElementByld('id名')
    
```js
const element = document.getElementById("irgedneineId")
```

---


使用 console.dir() 可以打印我们获取的元素对象，更好的查看对象里面的属性和方法。

示例
```html
<div id="time">2019-9-9</div>
<script>
    // 1.因为我们文档页面从上往下加载，所以得先有标签，所以script写在标签下面
    // 2.get 获得 element 元素 by 通过 驼峰命名法
    // 3.参数 id是大小写敏感的字符串
    // 4.返回的是一个元素对象
    var timer = document.getElementById('time');
    console.log(timer);
    // 5. console.dir 打印我们的元素对象，更好的查看里面的属性和方法
    console.dir(timer);
</script>
```


## 3.5 根据标签名获取  getElementByTagName()

tag 指的是 html 中的 `<div>` 或者 `<h1>` 等 

返回一个 array, gibt alle Elemente eines bestimmten Tags zurück.
还可以根据标签名获取某个元素（父元素）内部所有指定标签名的子元素,获取的时候不包括父元素自己

`element.getElementsByTagName('标签名')`
`const elements = document.getElementsByTagName("div");`

根据标签名获取，使用 getElementByTagName() 方法可以返回带有指定标签名的对象的集合

- 因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
- 得到元素对象是动态的
- 返回的是获取过来元素对象的集合，以伪数组的形式存储
- 如果获取不到元素，则返回为空的伪数组(因为获取不到对象)


1
ol.getElementsByTagName('li');

注意：父元素必须是单个对象(必须指明是哪一个元素对象)，获取的时候不包括父元素自己

```html
<script>
	//element.getElementsByTagName('标签名'); 父元素必须是指定的单个元素
    var ol = document.getElementById('ol');
    console.log(ol.getElementsByTagName('li'));
</script>
```


2 
document.getElementsByTagName('标签名');

```html

<ul>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
    <li>知否知否，应是等你好久</li>
</ul>
<script>
    // 1.返回的是获取过来元素对象的集合 以伪数组的形式存储
    var lis = document.getElementsByTagName('li');
    console.log(lis);
    console.log(lis[0]);
    // 2.依次打印,遍历
    for (var i = 0; i < lis.length; i++) {
        console.log(lis[i]);
    }
    // 3.如果页面中只有 1 个 li，返回的还是伪数组的形式
    // 4.如果页面中没有这个元素，返回的是空伪数组
</script>

```


## 3.6 根据类名获取 getElementsByClassName()

根据类名返回元素对象合集
gibt eine Sammlung (HTMLCollection) von Elementen mit einer bestimmten Klasse zurück.

document.getElementsByClassName('类名')
ol.getElementsByClassName('类名')
const elements = document.getElementsByClassName("irgendeineKlasse");

## 3.7 根据AttributName获取  getElementsByName()
document.getElementsByName("wertImAttributName")



## 3.8 document.querySelector(selector):
https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector

> 这里的 selector 指的不光是 css-selector, 还以用 html 的tag, 等等

注意这里不是 css selector 
根据指定选择器返回第一个元素对象. 返回一个 erste Element .  findet das erste Element, das einem CSS-Selektor entspricht.

document.querySelector('选择器');
```js
const element = document.querySelector(".irgendeineKlasse");
```

// 切记里面的选择器需要加符号 
// 类选择器.box 
// id选择器 `#nav`
var firstBox = document.querySelector('.box');

```js
querySelector('*')

querySelector('input')

querySelector('input[name="pwd"]')
querySelector('input[value="pwd"]')
querySelector('input[type="reset"]')
querySelector('input[type="reset"] input[value="pwd"]') // 这样做是会报错, 是无效的

querySelector('[name="pwd"]')


//Here, the first <input> element with the name "login" (<input name="login"/>) located inside a <div> whose class is "user-panel main" (<div class="user-panel main">) in the document is returned:
const el = document.querySelector("div.user-panel.main input[name='login']");

```

## 3.9 document.querySelectorAll(selector)

gibt alle Elemente zurück, die einem Selektor entsprechen.

> 这里的 selector 指的不光是 css-selector, 还以用 html 的tag, 等等

返回 nodelist
根据指定选择器返回所有元素对象
```js
document.querySelectorAll('选择器');
const elements = document.querySelectorAll(".irgendeineKlasse");
```

Auch mit dieser Methode bekommen wir eine Nodelist, nämlich alle Elemente, die mit dem in der Parameterliste spezifizierten Selektor angesprochen werden können.

注意：
querySelector 和 querySelectorAll 里面的选择器需要加符号,比如: document.querySelector('#nav');

```js
<script>
    // 1. getElementsByClassName 根据类名获得某些元素集合
    var boxs = document.getElementsByClassName('box');
    console.log(boxs);
    // 2. querySelector 返回指定选择器的第一个元素对象  切记 里面的选择器需要加符号 .box  #nav
    var firstBox = document.querySelector('.box');
    console.log(firstBox);
    var nav = document.querySelector('#nav');
    console.log(nav);
    var li = document.querySelector('li');
    console.log(li);
    // 3. querySelectorAll()返回指定选择器的所有元素对象集合
    var allBox = document.querySelectorAll('.box');
    console.log(allBox);
    var lis = document.querySelectorAll('li');
    console.log(lis);


   const p = document.querySelector("p");
    console.log(p);

    const allRadios = Array.from(document.querySelectorAll("[type=radio]"));
</script>
```

# 4 Auffind-Eigenschaften in document


HTML Collections
- collection

```js
const form = document.forms[0];
console.log(form);
```

|                           |                                                                                                                               |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Eigenschaften in document | Beschreibung                                                                                                                  |
| document.anchors          | Liefert eine Liste aller Anchor-Elemente (gekennzeichnet durch <a>-Tags).                                                     |
| document.body             | Liefert das body-Element des Dokumentes.                                                                                      |
| document.doctype          | Liefert den Wert von <!DOCTYPE> des Dokuments.                                                                                |
| document.documentElement  | Liefert das html-Element                                                                                                      |
| document.forms            | Liefert eine Liste aller Formulare (gekennzeichnet durch <form>-Tags) des Dokuments.                                          |
| document.images           | Liefert eine Liste aller Bilder (gekennzeichnet durch <img>-Tag) des Dokuments.                                               |
| document.links            | Liefert eine Liste mit allen Verweisen die in dem Dokument enthalten sind (gekennzeichnet durch <a>, <area> und andere Tags). |
|                           |                                                                                                                               |

# 5 Auffind-Methoden/Eigenschaften in element

![](image/Pasted%20image%2020241208212126.png)

|                                |                                                                            |
| ------------------------------ | -------------------------------------------------------------------------- |
| Eigenschaften/Methoden         | Beschreibung                                                               |
| element.attributes             | Liefert eine Liste mit allen Attributen eines Elements.                    |
| element.childNodes             | Liefert eine Liste mit allen Kindelementen eines Elements.                 |
| element.firstChild             | Liefert das erste Kind eines Elements.                                     |
| element.getAttribute()         | Liefert den Wert des spezifizierten Attributs.                             |
| element.getElementsByTagName() | Liefert eine Liste mit allen Elementen mit dem spezifizierten Tag-Namen.   |
| element.hasAttribute()         | Liefert true wenn ein Element das spezifizierte Attribut hat, sonst false. |
| element.hasAttributes()        | Liefert true wenn ein Element (beliebige) Attribute hat, sonst false.      |
| element.hasChildNodes()        | Liefert true falls das Element Kindelemente hat, sonst false.              |
| element.lastChild              | Liefert das letzte Kindelement eines Elements.                             |
| element.nextSibling            | Liefert das Geschwister welches dem Element unmittelbar folgt.             |
| element.ownerDocument          | Liefert das Wurzel-Element des Elements (üblicherweise document).          |
| element.parentNode             | Liefert den Elternknoten des Elements.                                     |
| element.previousSibling        | Liefert das Geschwister welches dem Element unmittelbar vorangeht.         |


# 6 Methoden und Eigenschaften zum Verändern von Elementen

|                           |                                                                                                     |
| ------------------------- | --------------------------------------------------------------------------------------------------- |
| Eigenschaften/Methoden    | Beschreibung                                                                                        |
| document.write            | Schreibt Inhalt in ein HTML-Dokument. Achtung: Bestehender Inhalt wird überschrieben.               |
| element.innerHTML         | Ändert den Inhalt eines HTML-Elements.                                                              |
| element.attribute         | Ändert den Wert eines HTML-Attributs.                                                               |
| element.setAttribute()    | Ändert ebenfalls den Wert eines HTML-Attributs.                                                     |
| element.style.property    | Ändert den CSS-Style eines HTML-Elements.                                                           |
| element.appendChild()     | Fügt einen neuen Kindknoten an letzter Stelle der Liste der Kindknoten zu einem Element hinzu.      |
| element.insertBefore()    | Fügt einen neuen Kindknoten vor dem spezifizierten Kindknoten ein.                                  |
| element.removeAttribute() | Entfernt ein Attribut aus dem spezifizierten Element.                                               |
| element.removeChild()     | Entfernt den spezifizierten Kindknoten.                                                             |
| element.replaceChild()    | Ersetzt den spezifizierten Kindknoten durch einen neuen Kindknoten.                                 |
| element.textContent       | Setzt oder liefert den textuellen Inhalt des Elements und aller direkten und indirekten Nachfolger. |

# 7 改变元素 

JavaScript 的 DOM 操作可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容 、属性等。注意以下都是属性. 

## 7.1 总结

![在这里插入图片描述](https://img-blog.csdnimg.cn/f6835ead437948e3804c4432ceb812ad.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)




## 7.2 改变元素内容
https://stackoverflow.com/questions/3955229/remove-all-child-elements-of-a-dom-node-in-javascript


1 element.innerHTML
起始位置到终止位置的全部内容，包括HTML标签，同时保留空格和换行
erlaubt das Einfügen von HTML-Inhalten in ein Element.
`element.innerHTML = "<p>Neuer Inhalt</p>";`

- **功能**: 获取或设置 HTML 格式的内容。
- **特点**:
    - 会解析 HTML 标签。
    - 支持嵌入的 HTML 代码。
- 用法
    - `document.getElementById('example').innerHTML = '<b>Bold Text</b>';`  如果元素内容是 `<b>Bold Text</b>`，`innerHTML` 将返回：`<b>Bold Text</b>`。
    - **优点**: 能动态插入 HTML 代码，适合需要嵌入复杂结构时使用。
    - **缺点**: 容易引发 **XSS (跨站脚本攻击)**，如果内容来源不可信，请避免使用。


```html
<body>
    <div></div>
    <p>
        我是文字
        <span>123</span>
    </p>

    <script>
        // innerText 和 innerHTML的区别 
        // 1. innerText 不识别html标签,去除空格和换行
        var div = document.querySelector('div');
        div.innerText = '<strong>今天是：</strong> 2019';
        // 2. innerHTML 识别html标签 保留空格和换行的
        div.innerHTML = '<strong>今天是：</strong> 2019';
        // 这两个属性是可读写的  可以获取元素里面的内容
        var p = document.querySelector('p');
        console.log(p.innerText);
        console.log(p.innerHTML);
    </script>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/f3394f40561e45c299c09d7bbecdb513.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)



2  element.innerText
从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉。
==ändert nur den sichtbaren Textinhalt eines Elements== und berücksichtigt dabei das CSS-Rendering. Nicht sichtbare Inhalte (z. B. aufgrund von display: none) werden ignoriert.  就是说 element.innerText  根本找不到  Nicht sichtbare Inhalte, 自然也就无法改变它的 值了  
```
element.innerText = "Neuer Inhalt";
```

- **功能**: 获取或设置元素中**可见的文本内容**。
- **特点**:
    - 不解析 HTML 标签，只返回用户在页面上看到的文本。
    - 会忽略隐藏的内容（如通过 `display: none` 隐藏的部分）。
    - 会受 CSS 的影响，比如 `text-transform`。
- 实例
    - `document.getElementById('example').innerText = 'Plain Text';`  如果元素内容是 `<b>Bold Text</b>`，`innerText` 将返回：`Bold Text`。
- **优点**:
    - 操作简单，直接返回可见内容。
- **缺点**:
    - 访问效率较低，因为它会触发浏览器的**回流（reflow）**，计算当前的可见内容。




3  element.textContent

ändert den Textinhalt, ohne HTML-Tags zu interpretieren.
`element.textContent = "Neuer Inhalt";`


```js
doFoo.onclick = () => {
  const myNode = document.getElementById("foo");
  myNode.textContent = '';
}

```

- **优点**:
    - 操作简单，直接返回可见内容。
- **缺点**:
    - 访问效率较低，因为它会触发浏览器的**回流（reflow）**，计算当前的可见内容。
- 示例 
    - `document.getElementById('example').textContent = 'Plain Text';`
- **优点**:
    - 性能更高，因为它不会触发回流。
    - 更安全，用于防止 XSS 攻击。
- **缺点**:
    - 不会保留 HTML 格式，所有标签会被当作普通文本。


4 innerHTML 和 innerText, textContent 三者的比较 

| 特性             | `innerHTML`  | `innerText`  | `textContent` |
| -------------- | ------------ | ------------ | ------------- |
| **包含 HTML 标签** | ✅ 解析 HTML    | ❌ 不解析        | ❌ 不解析         |
| **包含隐藏内容**     | ✅ 包含         | ❌ 不包含        | ✅ 包含          |
| **性能**         | 较低（解析 HTML）  | 较低（触发回流）     | 高（只读写文本内容）    |
| **安全性**        | 容易受 XSS 攻击   | 较安全          | 非常安全          |
| **典型应用场景**     | 动态插入或修改 HTML | 获取或设置可见的文本内容 | 获取或设置所有文本内容   |

### 7.2.1 **使用建议**

- **`innerHTML`**: 需要动态操作 HTML 时使用，但要避免不可信内容。
- **`innerText`**: 操作用户可见文本时使用。
- **`textContent`**: 获取纯文本内容时优先使用，性能更好且更安全。

4 element.replaceChildren(...arrayOfNewChildren);

In 2022+, use the replaceChildren() API!
Replacing all children can now be done with the (cross-browser supported) replaceChildren API:
    `container.replaceChildren(...arrayOfNewChildren);`

This will do both:
- remove all existing children, and
- append all of the given new children, in one operation.

You can also use this same API to just remove existing children, without replacing them:
    `container.replaceChildren();`

This is fully supported in Chrome/Edge 86+, Firefox 78+, and Safari 14+. It is fully specified behavior. This is likely to be faster than any other proposed method here, since the removal of old children and addition of new children is done without requiring innerHTML, and in one step instead of multiple.

## 7.3 改变元素属性

```js
// img.属性
img.src = "xxx";

input.value = "xxx";
input.type = "xxx";
input.checked = "xxx";
input.selected = true / false;
input.disabled = true / false;
```



## 7.4 Elemente hinzufügen und entfernen

- `document.createElement(tagName)`: erstellt ein neues Element.
    - `document.createElement("div");`
- `parentElement.appendChild(childElement)`: fügt ein Kind-Element am Ende des Elternelements ein.
    - `parentElement.appendChild(neuesElement);`
- `parentElement.insertBefore(newElement, referenceElement)`: fügt ein neues Element vor einem bestehenden Element ein.
    - `parentElement.insertBefore(neuesElement, referenzElement);`
- `element.remove():` entfernt ein Element aus dem DOM.
    - `element.remove();`
- `parentElement.removeChild(childElement)`: entfernt ein Kind-Element.
    - `parentElement.removeChild(childElement);`
    - `myList.removeChild(myList.lastElementChild);`







# 8 Klassen und Style bearbeiten: element.className

我们可以通过 JS 修改元素的大小、颜色、位置等样式。

1 行内样式操作
```
// element.style
div.style.backgroundColor = 'pink';
div.style.width = '250px';
```

2 类名样式操作
// element.className

注意：
- JS里面的样式采取驼峰命名法，比如 fontSize ，backgroundColor
- JS 修改 style 样式操作 ，产生的是行内样式，CSS权重比较高
- 如果样式修改较多，可以采取操作类名方式更改元素样式
- class 因为是个保留字，因此使用className来操作元素类名属性
- className 会直接更改元素的类名，会覆盖原先的类名

```html
<body>
    <div class="first">文本</div>
    <script>
        // 1. 使用 element.style 获得修改元素样式  如果样式比较少 或者 功能简单的情况下使用
        var test = document.querySelector('div');
        test.onclick = function() {
            // this.style.backgroundColor = 'purple';
            // this.style.color = '#fff';
            // this.style.fontSize = '25px';
            // this.style.marginTop = '100px';
            // 让我们当前元素的类名改为了 change

            // 2. 我们可以通过 修改元素的className更改元素的样式 适合于样式较多或者功能复杂的情况
            // 3. 如果想要保留原先的类名，我们可以这么做 多类名选择器
            // this.className = 'change';
            this.className = 'first change';
        }
    </script>
</body>
```

```js
    function changePic(mood) {
        if (mood === "g") {
            pic.parentElement.className = "happy";
            pic.src = "pics/sonne.png";
            pic.alt = ":-)";
        }
        else {
            pic.parentElement.className = "sad";
            pic.src = "pics/sonneSad.jpg";
            pic.alt = ":-(";
        }
    }
```


## 8.1 element.classList:

给 element 编辑他的 css中的class

The Element.classList is a read-only property that returns a live DOMTokenList collection of the class attributes of the element. This can then be used to manipulate the class list.
```
element.classList.add(className): fügt eine Klasse hinzu.

element.classList.remove(className): entfernt eine Klasse.

element.classList.toggle(className): fügt eine Klasse hinzu, wenn sie fehlt, oder entfernt sie, wenn sie vorhanden ist.


element.style.property: ermöglicht das direkte Bearbeiten von CSS-Eigenschaften.
element.style.color = "red";
element.style.fontSize = "20px";
```




1
```js

const div = document.createElement("div");
div.className = "foo";

// our starting state: <div class="foo"></div>
console.log(div.outerHTML);

// use the classList API to remove and add classes
div.classList.remove("foo");
div.classList.add("anotherclass");

// <div class="anotherclass"></div>
console.log(div.outerHTML);

// if visible is set remove it, otherwise add it
div.classList.toggle("visible");

// add/remove visible, depending on test conditional, i less than 10
div.classList.toggle("visible", i < 10);

console.log(div.classList.contains("foo"));

// add or remove multiple classes
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// add or remove multiple classes using spread syntax
const cls = ["foo", "bar"];
div.classList.add(...cls);
div.classList.remove(...cls);

// replace class "foo" with class "bar"
div.classList.replace("foo", "bar");

```



## 8.2 排他思想
如果有同一组元素，我们相要某一个元素实现某种样式，需要用到循环的排他思想算法：

1. 所有元素全部清除样式（干掉其他人）
2. 给当前元素设置样式 （留下我自己）
3. 注意顺序不能颠倒，首先干掉其他人，再设置自己

```html
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // 1. 获取所有按钮元素
        var btns = document.getElementsByTagName('button');
        // btns得到的是伪数组  里面的每一个元素 btns[i]
        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function() {
                // (1) 我们先把所有的按钮背景颜色去掉  干掉所有人
                for (var i = 0; i < btns.length; i++) {
                    btns[i].style.backgroundColor = '';
                }
                // (2) 然后才让当前的元素背景颜色为pink 留下我自己
                this.style.backgroundColor = 'pink';

            }
        }
        //2. 首先先排除其他人，然后才设置自己的样式 这种排除其他人的思想我们成为排他思想
    </script>
</body>

```


![在这里插入图片描述](https://img-blog.csdnimg.cn/c4ab0beac7444b208441727a380b437e.gif#pic_center)




# 9 属性操作
## 9.1 属性操作
### 9.1.1 获取属性值 element.getAttribute();
1 获取内置属性值(元素本身自带的属性)
element.属性;
form_YZH.id

2 获取自定义的属性
element.getAttribute('属性');

form_YZH.getAttribute('id');

`element.getAttribute(attribute): holt den aktuellen Wert eines Attributs.`
`element.getAttribute("href");`
### 9.1.2 设置属性值 element.setAttribute();
设置内置属性值
element.属性 = '值';

主要设置自定义的属性
element.setAttribute('属性','值');

element.setAttribute(attribute, value): setzt ein Attribut mit einem neuen Wert.
`element.setAttribute("src", "bild.jpg");`


```js
let form = document.forms[0];
form.setAttribute("novalidate",true);
// 之前 <form> xxx </form>
// 之后 <form novalidate> xxx </form>



let form = document.forms[0];
form.setAttribute("id","yzh");
// 之前 <form> xxx </form>
// 之后 <form id="yzh"> xxx </form>
```

### 9.1.3 移除属性 element.removeAttribute();
element.removeAttribute('属性');
`element.removeAttribute(attribute): entfernt ein Attribut.`
`element.removeAttribute("src");`

### 9.1.4 例子
```html 
<body>
    <div id="demo" index="1" class="nav"></div>
    <script>
        var div = document.querySelector('div');
        // 1. 获取元素的属性值
        // (1) element.属性
        console.log(div.id);
        //(2) element.getAttribute('属性')  get得到获取 attribute 属性的意思 我们程序员自己添加的属性我们称为自定义属性 index
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));
        // 2. 设置元素属性值
        // (1) element.属性= '值'
        div.id = 'test';
        div.className = 'navs';
        // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // class 特殊  这里面写的就是class 不是className
        // 3 移除属性 removeAttribute(属性)    
        div.removeAttribute('index');
    </script>
</body>
```


## 9.2 自定义属性 (H5中新增)
自定义属性目的：
- 保存并保存数据，有些数据可以保存到页面中而不用保存到数据库中
- 有些自定义属性很容易引起歧义，不容易判断到底是内置属性还是自定义的，所以H5有了规定

### 9.2.1 设置自定义属性
H5规定自定义属性 data-开头作为属性名并赋值

```html
<div data-index = "1"></>

// 或者使用JavaScript设置
div.setAttribute('data-index',1);
```

### 9.2.2 获取自定义属性
- 兼容性获取 element.getAttribute('data-index')
- H5新增的：element.dataset.index 或element.dataset['index'] IE11才开始支持

```html
<body>
    <div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));
        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
</body>
```
