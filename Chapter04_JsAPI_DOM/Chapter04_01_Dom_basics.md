# 1 什么是DOM
文档对象模型（Document Object Model，简称 DOM），是 W3C 组织推荐的处理可扩展标记语言（HTML或者XML）的标准编程接口
W3C 已经定义了一系列的 DOM 接口，通过这些 DOM 接口可以改变网页的内容、结构和样式。
![在这里插入图片描述](https://img-blog.csdnimg.cn/fc42557d25be4683881c2f0f231bc778.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

DOM 把以下内容都看做是对象
文档：一个页面就是一个文档，DOM中使用doucument来表示
元素：页面中的所有标签都是元素，DOM中使用 element 表示
节点：网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示


Ein HTML-Dokument ist hierarchisch, wie eine Baumstruktur, aus vielen Knoten aufgebaut. 
Der oberste oder Wurzelknoten ist das Dokument selbst, das document.
Mit js kann man auf das DOM zugreifen, es auslesen, Knoten löschen, ändern oder hinzufügen.


# 2 DOM主要操作
对于DOM操作，我们主要针对子元素的操作，主要有

创建
增
删
改
查
属性操作
时间操作

## 2.1 创建
document.write
innerHTML
createElement

## 2.2 增
appendChild
insertBefore

## 2.3 删
removeChild

## 2.4 改
主要修改dom的元素属性，dom元素的内容、属性、表单的值等
修改元素属性：src、href、title 等
修改普通元素内容：innerHTML、innerText
修改表单元素：value、type、disabled
修改元素样式：style、className

## 2.5 查
主要获取查询dom的元素
DOM提供的API方法：getElementById、getElementsByTagName (古老用法，不推荐)
H5提供的新方法：querySelector、querySelectorAll (提倡)
利用节点操作获取元素：父(parentNode)、子(children)、兄(previousElementSibling、nextElementSibling) 提倡

## 2.6 属性操作
主要针对于自定义属性
setAttribute：设置dom的属性值
getAttribute：得到dom的属性值
removeAttribute：移除属性


# 3 获取元素

## 3.1 如何获取页面元素
DOM在我们实际开发中主要用来操作元素。
我们如何来获取页面中的元素呢?

获取页面中的元素可以使用以下几种方式:
 - 根据 ID 获取
 - 根据标签名获取
 - 通过 HTML5 新增的方法获取
 - 特殊元素获取

## 3.2 使用不同method, 其返回值的类型


Einzelne Elemente (object):
- getElementById()
- getElementByQuerySelector()

Listen von Elementen:
- getElementsByTagName()
- getElementsByClassName()
- getElementsByName()
- getElementsByQuerySelectorAll()

HTML Collections
- collection

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
   

### 3.2.3 HTML Collections
```js
const form = document.forms[0];
console.log(form);
```


## 3.3 根据ID获取 getElementByld()
使用 getElementByld() 方法可以获取带ID的元素对象
    doucument.getElementByld('id名')

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


## 3.4 根据标签名获取  getElementByTagName()
还可以根据标签名获取某个元素（父元素）内部所有指定标签名的子元素,获取的时候不包括父元素自己
    element.getElementsByTagName('标签名')

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

## 3.5 通过H5新增方法获取

### 3.5.1 根据类名获取 getElementsByClassName
根据类名返回元素对象合集
document.getElementsByClassName('类名')
ol.getElementsByClassName('类名')


### 3.5.2 querySelector
https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector
根据指定选择器返回第一个元素对象

document.querySelector('选择器');

// 切记里面的选择器需要加符号 
// 类选择器.box 
// id选择器 #nav
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

### 3.5.3 querySelectorAll
根据指定选择器返回所有元素对象
    document.querySelectorAll('选择器');

注意：
querySelector 和 querySelectorAll 里面的选择器需要加符号,比如: document.querySelector('#nav');

### 3.5.4 例子
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


## 3.6 获取特殊元素 document.XX
1 获取body元素
返回body元素对象: document.body;

2 获取html元素
返回html元素对象: document.documentElement;

3 获取forms元素
const forms = document.forms;
const form = document.forms[0];


# 4 改变元素

JavaScript 的 DOM 操作可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容 、属性等。注意以下都是属性

## 4.1 改变元素内容
https://stackoverflow.com/questions/3955229/remove-all-child-elements-of-a-dom-node-in-javascript

1  element.innerText
从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉。

2 element.innerHTML

起始位置到终止位置的全部内容，包括HTML标签，同时保留空格和换行

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


3  element.textContent

```js
doFoo.onclick = () => {
  const myNode = document.getElementById("foo");
  myNode.textContent = '';
}

```


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

## 4.2 改变元素属性

```html
// img.属性
img.src = "xxx";

input.value = "xxx";
input.type = "xxx";
input.checked = "xxx";
input.selected = true / false;
input.disabled = true / false;
```

## 4.3 改变样式属性 element.className
我们可以通过 JS 修改元素的大小、颜色、位置等样式。

1 行内样式操作
// element.style
div.style.backgroundColor = 'pink';
div.style.width = '250px';

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


### 4.3.1 element.classList: 给 element 强加上一个css中的class

The Element.classList is a read-only property that returns a live DOMTokenList collection of the class attributes of the element. This can then be used to manipulate the class list.

返回 这个 element  被加上了那些 class (class 定义在 css 中 )

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





## 4.4 总结

![在这里插入图片描述](https://img-blog.csdnimg.cn/f6835ead437948e3804c4432ceb812ad.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

## 4.5 排他思想
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

## 4.6 自定义属性
### 4.6.1 获取属性值 element.getAttribute();
1 获取内置属性值(元素本身自带的属性)
element.属性;
form_YZH.id

2 获取自定义的属性
element.getAttribute('属性');

form_YZH.getAttribute('id');

### 4.6.2 设置属性值 element.setAttribute();
设置内置属性值
element.属性 = '值';

主要设置自定义的属性
element.setAttribute('属性','值');


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

### 4.6.3 移除属性 element.removeAttribute();
element.removeAttribute('属性');

### 4.6.4 例子
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


## 4.7 H5中新增的 自定义属性
自定义属性目的：
- 保存并保存数据，有些数据可以保存到页面中而不用保存到数据库中
- 有些自定义属性很容易引起歧义，不容易判断到底是内置属性还是自定义的，所以H5有了规定

### 4.7.1 H5 新增的 设置自定义属性的方法
H5规定自定义属性 data-开头作为属性名并赋值

```html
<div data-index = "1"></>

// 或者使用JavaScript设置
div.setAttribute('data-index',1);
```

### 4.7.2 H5 新增的 获取H5自定义属性的方法
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

# 5 节点操作

获取元素通常使用两种方式：

|1.利用DOM提供的方法获取元素	|2.利用节点层级关系获取元素|
|--|--|
|document.getElementById()	|利用父子兄节点关系获取元素|
|document.getElementsByTagName()	|逻辑性强，但是兼容性较差|
|document.querySelector 等	||
|逻辑性不强，繁琐	||

这两种方式都可以获取元素节点，我们后面都会使用，但是节点操作更简单
一般的，节点至少拥有三个基本属性

## 5.1 节点概述
网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM 中，节点使用 node 来表示。

HTML DOM 树中的所有节点均可通过 JavaScript 进行访问，所有 HTML 元素（节点）均可被修改，也可以创建或删除。

![在这里插入图片描述](https://img-blog.csdnimg.cn/f176c025b5ff43468d53ed4d49259812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

一般的，节点至少拥有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）这三个基本属性。


### 5.1.1 nodeType
- 元素节点：nodeType 为1
- 属性节点：nodeType 为2
- 文本节点：nodeType 为3(文本节点包括文字、空格、换行等)

我们在实际开发中，节点操作主要操作的是元素节点
利用 DOM 树可以把节点划分为不同的层级关系，常见的是父子兄层级关系。

### 5.1.2 nodeName
nodeName 必须要用大写
```js
if (form.lastElementChild.nodeName !== "P") // Elemente sind immer UPPERCASE, 所以这里用P, 不用小写的p. 小写的p 匹配不到

let message = document.createElement("p");// createElement 中 可以用小写的 
```


## 5.2 父级节点
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


## 5.3 子结点
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


### 5.3.1 第一个子结点 parentNode.firstChild
parentNode.firstChild

firstChild 返回第一个子节点，找不到则返回null
同样，也是包含所有的节点

### 5.3.2 最后一个子结点 parentNode.lastChild
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


### 5.3.3 第一个子结点 parentNode.firstElementChild
parentNode.firstElementChild

- firstElementChild 返回第一个子节点，找不到则返回null
- 有兼容性问题，IE9以上才支持


### 5.3.4 最后一个子结点parentNode.lastElementChild
parentNode.lastElementChild
- lastElementChild 返回最后一个子节点，找不到则返回null
- 有兼容性问题，IE9以上才支持

### 5.3.5 解决方案
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


## 5.4 兄弟节点
### 5.4.1 下一个兄弟节点 node.nextSibling
node.nextSibling

- nextSibling 返回当前元素的下一个兄弟元素节点，找不到则返回null
- 同样，也是包含所有的节点

### 5.4.2 上一个兄弟节点 node.previousSibling
node.previousSibling

previousSibling 返回当前元素上一个兄弟元素节点，找不到则返回null

同样，也是包含所有的节点

### 5.4.3 下一个兄弟节点 node.nextElementSibling
node.nextElementSibling

nextElementSibling 返回当前元素下一个兄弟元素节点，找不到则返回null
有兼容性问题，IE9才支持

### 5.4.4 上一个兄弟节点 node.previousElementSibling
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


## 5.5 节点操作 

### 5.5.1 创建节点 

#### 5.5.1.1 document.createElement('tagName');
document.createElement('tagName');
document.createElement() 方法创建由 tagName 指定的HTML 元素
因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点


```js

const div = document.createElement("div");
div.className = "foo";

// our starting state: <div class="foo"></div>
console.log(div.outerHTML);

```


#### 5.5.1.2 document.createTextNode
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

### 5.5.2 添加节点 node.appendChild(child), node.insertBefore(child,指定元素)
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

### 5.5.3 删除节点 node.removeChild(child)
node.removeChild(child)

node.removeChild()方法从 DOM 中删除 node节点下的一个子节点，返回删除的节点

### 5.5.4 复制节点(克隆节点) node.cloneNode()
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

### 5.5.5 面试题
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


