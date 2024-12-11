


# 1 节点操作

获取元素通常使用两种方式：

|1.利用DOM提供的方法获取元素	|2.利用节点层级关系获取元素|
|--|--|
|document.getElementById()	|利用父子兄节点关系获取元素|
|document.getElementsByTagName()	|逻辑性强，但是兼容性较差|
|document.querySelector 等	||
|逻辑性不强，繁琐	||

这两种方式都可以获取元素节点，我们后面都会使用，但是节点操作更简单


## 1.1 节点概述 Struktur des Dokumentes
网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM 中，节点使用 node 来表示。
Es gibt Vorfahren, Nachfahren, Eltern, Kinder und Geschwister.
HTML DOM 树中的所有节点均可通过 JavaScript 进行访问，所有 HTML 元素（节点）均可被修改，也可以创建或删除。

![在这里插入图片描述](https://img-blog.csdnimg.cn/f176c025b5ff43468d53ed4d49259812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

一般的，节点至少拥有三个基本属性. 节点至少拥有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）这三个基本属性。  


Es gibt verschiedene Arten von Knoten. Die wichtigsten hierbei sind:
- Der Dokumentknoten stellt die gesamte Struktur dar
- Der Wurzelknoten ist der Beginn des Dokumentes
- Ein Dokumentfragmentknoten zeigt nur einen Teil der Baumstruktur
- Ein Elementknoten ist ein Element aus HTML oder XML
- Ein Attributknoten entspricht einem Attribut aus der HTML- oder XML-Sprache
- Ein Textknoten stellt lediglich den Textinhalt eines Elementes bzw. eines Attributes dar

例子
[![6 5 dombaum uebung.gif](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/2/26/6_5_dombaum_uebung.gif)](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/2/26/6_5_dombaum_uebung.gif)
Der in der Übung gezeigte Wurzelknoten html besitzt als Kinder(child nodes) die Elementknoten head und body, ist also ein Elternteil(parent nodes) von ihnen. \
head und body werden Geschwister(siblings) genannt. 
Vom Wurzelknoten ausgehend kann man jeden anderen Knoten erreichen. 
Desweiteren ist html ein Vorfahrenelement von h1 und title ein Nachfahrenelement von html.


### 1.1.1 nodeType
同一个 Element 内还有 Elementknoten, Attributknoten und Textknoten.
- 元素节点：nodeType 为1
- 属性节点：nodeType 为2
- 文本节点：nodeType 为3(文本节点包括文字、空格、换行等)

我们在实际开发中，节点操作主要操作的是元素节点
利用 DOM 树可以把节点划分为不同的层级关系，常见的是父子兄层级关系。

### 1.1.2 nodeName
nodeName 必须要用大写
```js
if (form.lastElementChild.nodeName !== "P") // Elemente sind immer UPPERCASE, 所以这里用P, 不用小写的p. 小写的p 匹配不到

let message = document.createElement("p");// createElement 中 可以用小写的 
```

## 1.2 节点总览

|Eigenschaft	|Erläuterung|
|--|--|
|nodeName	|HTML-Element eines Knotens wird als Zeichenkette ausgegeben ( "body")|
|nodeType	|Tag = 1, Attribut = 2, Text = 3|
|childNodes|返回当前节点的所有子节点。|
|firstChild|	erstes Element im childNodes-Array, erster Kindsknoten, childNodes[0]|
|lastChild	|letztes Element im childNodes-Array, letzter Kindsknoten, childNodes[n] |
|nextSibling	|das nächste Kind des Elternknotens|
|previousSibling	|das vorherige Kind des Elternknotens|
|parentNode	|der Elternknoten|
|childElementCount|返回子元素（不包括文本节点和注释）的个数|
|children|返回当前节点的所有元素子节点。 为 childNodes 的元素版本|
|firstElementChild|	Das erste Kindsknotenelement. 指向第一个子元素；firstChild的元素版。|
|lastElementChild	|Das letzte Kindsknotenelement. 指向最后    一个子元素；lastChild的元素版。|
|previousElementSibling|	Das vorherige Kindselement des Elternknoten bzw. das vorherige Geschwisterknotenelement.指向前一个同辈元素；previousSibling的元素版。 |
|nextElementSibling	|Das nächste Kindselement des Elternknoten bzw. das nächste Geschwisterknotenelement.指向最后一个同辈元素；nextSibling的元素版。 |

### 1.2.1 firstChild派系 和 firstElementChild派系 比较
firstChild一派返回全部元素，包括空格以及元素等，而firstElementChild这一派比较高冷，它看不起文本和注释这点“小钱”. 
- 共同点
    - 它们的共同点都是获取父节点下第一个节点对象。
- 不同点
    - 对于文本元素，firstElementChild不能返回，而firstChild则可以. firstChild可以获取文本元素而firstElemenChild不能 . 
    - 所以如果父元素下的子元素不存在其他element元素，而是文本元素或注释，firstElementChild则会报错。
    - 但是firstElementChild只会获取元素节点对象，从名称就可以看出来，firstChild则可以获取文本节点对象（当然也可以获取元素节点对象）. 比如空格和换行都被当做文本节点。
    - 区别在于 firstChild 返回第一个子节点作为元素节点，包含文本节点或注释节点（取决于哪个是第一个），而 firstElementChild 返回第一个子节点作为元素节点（忽略文本和注释节点）。

例子
1 firstChild返回的除了元素节点，还可能是文本节点或注释节点。
```
<div id="div1">
  <h1>hello</h1>
</div>

let div1 = document.getElementById('div1');
console.log(div1.childNodes);
console.log(div1.firstChild);

```
结果如图所示：此次的返回结果除了包含h1标签之外，还有两个文本节点。他们是div和h1之间的回车和空格。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210219111843306.png)

2 `firstElementChild` 属性返回当前节点的第一个**元素**子节点（注意是只返回元素子节点，不包括文本结点和注释结点）。如果没有任何元素子节点，则返回 null。
```
<div id="div1">
  <h1>hello</h1>
</div>

let div1 = document.getElementById('div1');
console.log(div1.children);
console.log(div1.firstElementChild);
```
结果如图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210219112439323.png)  
`lastElementChild` 属性返回当前节点的最后一个**元素**子节点，如果不存在任何元素子节点，则返回null。


## 1.3 父级节点  (node.parentNode 或者 node.parentElement)
node.parentNode 或者  node.parentElement

1 parentNode
- parentNode属性可以返回某节点的父结点，注意是最近的一个父结点
- 如果指定的节点没有父结点则返回null
```html
<body>
    <!-- 节点的优点 -->
    <div>我是div</div>
    <span>我是span</span>
    <ul>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
    </ul>
    <div class="demo">
        <div class="box">
            <span class="erweima">×</span>
        </div>
    </div>

    <script>
        // 1. 父节点 parentNode
        var erweima = document.querySelector('.erweima');
        // var box = document.querySelector('.box');
        // 得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null
        console.log(erweima.parentNode);
    </script>
</body>
```


2 parentElement
```js
const pic = document.querySelector("img");

console.log(pic.parentElement);
function sky(mood) {
    if (mood === "happy") pic.parentElement.className = "happy";
    else pic.parentElement.className = "sad";
}
    
```


## 1.4 子结点
parentNode.childNodes(标准)
- parentNode.childNodes 返回包含指定节点的子节点的集合，该集合为即时更新的集合
- 返回值包含了所有的子结点，包括元素节点，文本节点等
- 如果只想要获得里面的元素节点，则需要专门处理。所以我们一般不提倡使用childNodes

parentNode.children(非标准)
- parentNode.children 是一个只读属性，返回所有的子元素节点
- 它只返回子元素节点，其余节点不返回 （这个是我们重点掌握的）
- 虽然 children 是一个非标准，但是得到了各个浏览器的支持，因此我们可以放心使用

```html
<body>
    <ul>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
    </ul>
    <ol>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
    </ol>
    <script>
        // DOM 提供的方法（API）获取
        var ul = document.querySelector('ul');
        var lis = ul.querySelectorAll('li');
        // 1. 子节点  childNodes 所有的子节点 包含 元素节点 文本节点等等
        console.log(ul.childNodes);
        console.log(ul.childNodes[0].nodeType);
        console.log(ul.childNodes[1].nodeType);
        // 2. children 获取所有的子元素节点 也是我们实际开发常用的
        console.log(ul.children);
    </script>
</body>
```


### 1.4.1 parentNode.firstChild
parentNode.firstChild

firstChild 返回第一个子节点，找不到则返回null
同样，也是包含所有的节点

### 1.4.2 parentNode.lastChild
parentNode.lastChild

lastChild 返回最后一个子节点，找不到则返回null
同样，也是包含所有的节点

```js
<body>
    <ol>
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>我是li5</li>
    </ol>
    <script>
        var ol = document.querySelector('ol');
        // 1. firstChild 第一个子节点 不管是文本节点还是元素节点
        console.log(ol.firstChild);
        console.log(ol.lastChild);
        // 2. firstElementChild 返回第一个子元素节点 ie9才支持
        console.log(ol.firstElementChild);
        console.log(ol.lastElementChild);
        // 3. 实际开发的写法  既没有兼容性问题又返回第一个子元素
        console.log(ol.children[0]);			//第一个子元素节点
        console.log(ol.children[ol.children.length - 1]);//最后一个子元素节点
    </script>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/dde9c5a059d34c8da3641043a4ecb7df.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)


### 1.4.3 parentNode.firstElementChild
parentNode.firstElementChild

- firstElementChild 返回第一个子节点，找不到则返回null
- 有兼容性问题，IE9以上才支持


### 1.4.4 parentNode.lastElementChild
parentNode.lastElementChild
- lastElementChild 返回最后一个子节点，找不到则返回null
- 有兼容性问题，IE9以上才支持

### 1.4.5 解决方案
实际开发中，firstChild 和 lastChild 包含其他节点，操作不方便，而 firstElementChild 和 lastElementChild 又有兼容性问题，那么我们如何获取第一个子元素节点或最后一个子元素节点呢？

解决方案
- 如果想要第一个子元素节点，可以使用 parentNode.chilren[0]
- 如果想要最后一个子元素节点，可以使用

// 数组元素个数减1 就是最后一个元素的索引号
parentNode.chilren[parentNode.chilren.length - 1]


示例：
```html
<body>
    <ol>
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
    </ol>
    <script>
        var ol = document.querySelector('ol');
        // 1.firstChild 获取第一个子结点的，包含文本结点和元素结点
        console.log(ol.firstChild);
        // 返回的是文本结点 #text(第一个换行结点)
        
        console.log(ol.lastChild);
        // 返回的是文本结点 #text(最后一个换行结点)
        // 2. firstElementChild 返回第一个子元素结点
        console.log(ol.firstElementChild);
        // <li>我是li1</li>
        
        // 第2个方法有兼容性问题，需要IE9以上才支持
        // 3.实际开发中，既没有兼容性问题，又返回第一个子元素
        console.log(ol.children[0]);
        // <li>我是li1</li>
        console.log(ol.children[3]);
        // <li>我是li4</li>
        // 当里面li个数不唯一时候，需要取到最后一个结点时这么写
        console.log(ol.children[ol.children.length - 1]);
    </script>
</body>
```


## 1.5 兄弟节点
Mit firstElementChild, lastElementChild, previousElementSibling und nextElementSibling können Sie auf Elemente der jeweiligen Knoten zugreifen. Gibt es keine Elemente an der Stelle wird der Wert Null zurückgegeben.

如果找不到的话, 就返回 Null 

### 1.5.1 node.nextSibling
node.nextSibling

- nextSibling 返回当前元素的下一个兄弟元素节点，找不到则返回null
- 同样，也是包含所有的节点

### 1.5.2 node.previousSibling
node.previousSibling

previousSibling 返回当前元素上一个兄弟元素节点，找不到则返回null

同样，也是包含所有的节点

### 1.5.3 node.nextElementSibling
node.nextElementSibling

nextElementSibling 返回当前元素下一个兄弟元素节点，找不到则返回null
有兼容性问题，IE9才支持

### 1.5.4 node.previousElementSibling
node.previousElementSibling

previousElementSibling 返回当前元素上一个兄弟元素节点，找不到则返回null
有兼容性问题，IE9才支持

```html

<body>
    <div>我是div</div>
    <span>我是span</span>
    <script>
        var div = document.querySelector('div');
        // 1.nextSibling 下一个兄弟节点 包含元素节点或者 文本节点等等
        console.log(div.nextSibling);		// #text
        console.log(div.previousSibling);	// #text
        // 2. nextElementSibling 得到下一个兄弟元素节点
        console.log(div.nextElementSibling);	//<span>我是span</span>
        console.log(div.previousElementSibling);//null
    </script>
</body>
```


如何解决兼容性问题 ？

答：自己封装一个兼容性的函数
```js
function getNextElementSibling(element) {
    var el = element;
    while(el = el.nextSibling) {
        if(el.nodeType === 1){
            return el;
        }
    }
    return null;
}
```


## 1.6 节点操作 

### 1.6.1 总览 

|Methode	|Syntax	|Erläuterung|
|---|---|---|
|appendChild	|[Elternknoten].appendChild( [Kindknoten]);	|hängt den Kindknoten an den Elternknoten an|
|hasChildNodes|	[Knotenname].hasChildNodes();	|gibt einen booleschen Wert aus, der aussagt ob Kinder vorhanden sind oder nicht|
|createElement|	document.createElement( [HTML-Element]);	|erzeugt einen Knoten, der aus dem HTML-Element besteht|
|removeNode|	[Knotenname].removeNode( [alles?]);	|der Knoten wird aus dem Baum entfernt, steht in Klammern der Wert true, werden auch alle Kindknoten entfernt|
|cloneNode|	[Knotenname].cloneNode( [alles?]);	|erzeugt ein Duplikat des angegebenen Knotens, ist der Wert in Klammern true, werden auch alle Kindknoten dupliziert|
|replaceNode|	[Alter Knoten].replaceNode( [Neuer Knoten]);	|der alte Knoten wird durch den neuen ersetzt|
|setAttribute|	[Knotenname].setAttribute( [Attributname], [Attributwert]);	|der Knoten erhält ein zusätzliches Attribut|
|insertBefore|	[Elternknoten].insertBefore( [neuer Kindknoten], [folgender Kindknoten]);	|es wird ein neuer Kindknoten in den Elternknoten eingefüg|

### 1.6.2 创建节点 

#### 1.6.2.1 document.createElement('tagName');
document.createElement('tagName');
document.createElement() 方法创建由 tagName 指定的HTML 元素
因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点


```js

const div = document.createElement("div");
div.className = "foo";

// our starting state: <div class="foo"></div>
console.log(div.outerHTML);

```


#### 1.6.2.2 document.createTextNode
document.createTextNode("Danke " + user);
没有创造任何新的节点, 没有创造 名字为 "text" 的节点

```js
function feedback(user) {
    // Element erzeugen
    let message = document.createElement("p");
    
    // neues Element mit content und/oder Attributen bestücken
    let text = document.createTextNode("Danke " + user);
}


function showMessage(field, explanation) {
    // Falls messages vorhanden sind, werden diese vorher gelöscht
    deleteMessage();
    let message = document.createElement("p");
    let text = field.parentElement.firstElementChild.innerHTML + " " + explanation + "!";
    console.log(text);
    message.appendChild(document.createTextNode(text));  // 原来为 <p></p>, 添加完了以后变为 <p>Danke, yanbo</p>
    form.appendChild(message);
};

```


`document.createTextNode` prevents text from being rendered as html. 
https://stackoverflow.com/questions/13041388/javascript-trying-to-add-linebreak-inside-create-text-node-method
所以 使用 下面这样 都是 无效的, 无法在 html 中显示出 为换行
```js

1
<script>
/*jslint browser:true */
var i;
var out = document.getElementById("output");
var args = ["aaa", "bbb", "ccc", "ddd", 1, 2, 4 + 4];
function displayArgs() {
    "use strict";
    for (i = 0; i < args.length; i++) {
        out.appendChild(document.createTextNode(args[i] + "<br>"));
    }
}

displayArgs(args);
</script>

========
2
alertInformation += (" The required Filed \"" + element.name + "\": wasn't inputed or doesn't match pattern" + '<br/>')  // 无效的
alertInformation += (" The required Filed \"" + element.name + "\": wasn't inputed or doesn't match pattern" + "\n") // 无效的


// Element erzeugen
let message = document.createElement("p");

// neues Element mit content und/oder Attributen bestücken
let text = document.createTextNode(alertInformation);

// content in neues Element einfügen
message.appendChild(text);

// vollständiges Element in das Dokument einfügen
form.appendChild(message);

```

使用 `myDiv.innerHTML = 'blah!<br/>';` 是有效的
```js
var myDiv = document.createElement("div");
myDiv.id = 'myDiv';
myDiv.innerHTML = 'blah!<br/>';
document.body.appendChild(myDiv);
```

### 1.6.3 [Knotenname].hasChildNodes();	

### 1.6.4 替代节点 [Alter Knoten].replaceNode( [Neuer Knoten]);

### 1.6.5 添加节点 node.appendChild(child), node.insertBefore(child,指定元素)
node.appendChild(child)
    node.appendChild() 方法将一个节点添加到指定父节点的子节点列表末尾。类似于 CSS 里面的 after 伪元素。

node.insertBefore(child,指定元素)
    node.insertBefore() 方法将一个节点添加到父节点的指定子节点前面。类似于 CSS 里面的 before 伪元素。

```js
<body>
    <ul>
        <li>123</li>
    </ul>
    <script>
        // 1. 创建节点元素节点
        var li = document.createElement('li');
        // 2. 添加节点 node.appendChild(child)  node 父级  child 是子级 后面追加元素  类似于数组中的push
        // 先获取父亲ul
        var ul = document.querySelector('ul');
        ul.appendChild(li);
        // 3. 添加节点 node.insertBefore(child, 指定元素);
        var lili = document.createElement('li');
        ul.insertBefore(lili, ul.children[0]);
        // 4. 我们想要页面添加一个新的元素分两步: 1. 创建元素 2. 添加元素
    </script>
</body>
```

```js
const form = document.forms[0];
function feedback(user) {
    // Element erzeugen
    let message = document.createElement("p");
    // neues Element mit content und/oder Attributen bestücken
    let text = document.createTextNode("Danke " + user);
    // content in neues Element einfügen
    message.appendChild(text);
    // vollständiges Element in das Dokument einfügen
    form.appendChild(message);
}
```

### 1.6.6 删除节点 node.removeChild(child)
node.removeChild(child)

node.removeChild()方法从 DOM 中删除 node节点下的一个子节点，返回删除的节点

### 1.6.7 复制节点(克隆节点) node.cloneNode()
node.cloneNode()

node.cloneNode()方法返回调用该方法的节点的一个副本。 也称为克隆节点/拷贝节点
如果括号参数为空或者为 false ，则是浅拷贝，即只克隆复制节点本身，不克隆里面的子节点
如果括号参数为 true ，则是深度拷贝，会复制节点本身以及里面所有的子节点

```html
<body>
    <ul>
        <li>1111</li>
        <li>2</li>
        <li>3</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        // 1. node.cloneNode(); 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容
        // 2. node.cloneNode(true); 括号为true 深拷贝 复制标签复制里面的内容
        var lili = ul.children[0].cloneNode(true);
        ul.appendChild(lili);
    </script>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/78d882e140344b47b288cbf90fd79a50.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

### 1.6.8 面试题
三种动态创建元素的区别

- doucument.write()
- element.innerHTML
- document.createElement()

区别：
- document.write() 是直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘
- element.innerHTML 
    - 是将内容写入某个 DOM 节点，不会导致页面全部重绘
    - 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂
    - 总结：不同浏览器下， innerHTML 效率要比 createElement 高
- document.createElement()创建多个元素效率稍低一点点，但是结构更清晰

```html
<body>
    <div class="innner"></div>
    <div class="create"></div>
    <script>
        // 2. innerHTML 创建元素
        var inner = document.querySelector('.inner');
        // 2.1 innerHTML 用拼接字符串方法
        for (var i = 0; i <= 100; i++) {
            inner.innerHTML += '<a href="#">百度</a>';
        }
        // 2.2 innerHTML 用数组形式拼接
        var arr = [];
        for (var i = 0; i <= 100; i++) {
            arr.push('<a href="#">百度</a>');
        }
        inner.innerHTML = arr.join('');

        // 3.document.createElement() 创建元素
        var create = document.querySelector('.create');
        var a = document.createElement('a');
        create.appendChild(a);
    </script>
</body>
```


2

```html
<figure>
    <img src="pics/sonne.png" alt="Die Sonne :-)">
    <figcaption>Deine Laune zählt!</figcaption>
</figure>
```

```css
.invert{
	filter: invert();  // 改变 度 
}
```

```js
    // Ändern von Attributen
    const pic = document.querySelector("img");
    // console.log(pic);
    
// styles manipulieren über die class
    const changeStyle = () => pic.classList.toggle("invert");  // if invert is already set to pic , 就 remove it (invert), otherwise add it
    pic.addEventListener("mouseover", changeStyle, false);   // 鼠标划过图片上方的说, 就会启动 changestyle 这个 funktion 
```





