# 1 初识JavaScirpt

## 1.1 JavaScript是什么
-   JavaScript 是世界上最流行的语言之一，是一种运行在客户端的脚本语言 （Script 是脚本的意思）
-   脚本语言：不需要编译，运行过程中由 js 解释器( js 引擎）逐行来进行解释并执行
-   现在也可以基于 Node.js 技术进行服务器端编程
-  JavaScript内嵌于HTML网页中，通过浏览器内置JavaScript引擎直接编译，把一个原本只用来显示的页面，转变成支持用户交互的页面程序。

## 1.2 JavaScript 的作用
主要用于开发交互式的Web页面，使网页的互动性更强，用户体验更好。

表单动态校验（密码强度检测） （ JS 产生最初的目的 ）
网页特效
服务端开发(Node.js)
桌面程序(Electron)
App(Cordova)
控制硬件-物联网(Ruff)
游戏开发(cocos2d-js)


## 1.3 HTML/CSS/JS 的关系
1. HTML/CSS 标记语言–描述类语言
    1. HTML 决定网页结构和内容( 决定看到什么 )，相当于人的身体
    2. CSS 决定网页呈现给用户的模样( 决定好不好看 )，相当于给人穿衣服、化妆
2. JS 脚本语言–编程类语言
    1. 实现业务逻辑和页面控制( 决定功能 )，相当于人的各种动作

## 1.4 浏览器执行JS简介

浏览器分成两部分：渲染引擎和 JS 引擎
- 渲染引擎：用来解析HTML与CSS，俗称内核，比如 chrome 浏览器的 blink ，老版本的 webkit
- JS 引擎：也称为 JS 解释器。 用来读取网页中的JavaScript代码，对其处理后运行，比如 chrome 浏览器的 V8

浏览器本身并不会执行JS代码，而是通过内置 JavaScript 引擎(解释器) 来执行 JS 代码 。JS 引擎执行代码时逐行解释每一句源码（转换为机器语言），然后由计算机去执行，所以 JavaScript 语言归为脚本语言，会逐行解释执行。

![在这里插入图片描述](https://img-blog.csdnimg.cn/6626246651a048ab94cff1c8afe62fc2.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)


## 1.5 JS组成
JavaScript 包括 ECMAScript、DOM、BOM

![](image/Chapter01_JS基础_JS组成_001.png)

1 ECMAScript
ECMAScript 是由ECMA 国际（ 原欧洲计算机制造商协会）进行标准化的一门编程语言，这种语言在万维网上应用广泛，它往往被称为 JavaScript 或 JScript，但实际上后两者是 ECMAScript 语言的实现和扩展。
ECMAScript：ECMAScript 规定了JS的编程语法和基础核心知识，是所有浏览器厂商共同遵守的一套JS语法工业标准。
![](image/Chapter01_JS基础_JS组成_002.png)

2 DOM文档对象模型
文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标记语言的标准编程接口。通过 DOM 提供的接口可以对页面上的各种元素进行操作（大小、位置、颜色等）。

3 BOM浏览器对象模型
BOM (Browser Object Model，简称BOM) 是指浏览器对象模型，它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框、控制浏览器跳转、获取分辨率等。

# 2 JavaScript的特点
1 脚本语言
脚本（script）简单来说就是一条条的文本命令，按照程序流程执行

常见的脚本语言： JavaScript、VBScript、Perl、PHP、Python等。
非脚本语言： C、C++、Java、C#等。

脚本和非脚本语言的区别
- 脚本语言依赖于解释器，只在被调用时自动进行解释或编译。
- 非脚本语言一般需要编译、链接，生成独立的可执行文件后才能运行。


2 可跨平台
几乎适用于所有的浏览器，包括手机等各类移动设备。
特点：JavaScript语言不依赖操作系统，仅需要浏览器的支持。

3 支持面向对象
面向对象是软件开发中的一种重要的编程思想，其优点非常多。


# 3 JS初体验
JS 有3中书写位置，分别为行内、内嵌和外部

## 3.1 行内式JS
由于现代网页开发提倡结构、样式、行为的分离，即分离HTML、CSS、 JavaScript三部分的代码，避免直接写在HTML标签的属性中，从而更有利于维 护。因此在实际开发中不推荐使用行内式。

`<input type="button" value="点我试试" onclink="javascript:alert('Hello World')" />`

1.  可以将单行或少量JS代码写在HTML标签的事件属性中(以on开头的属性)，如： onclink
2.  注意单双引号的使用：在HTML中我们推荐使用**双引号**，JS中我们推荐使用**单引号**
3.  可读性差，在 HTML 中编入 JS 大量代码时，不方便阅读
4. 引号易错，引号多层嵌套匹配时，非常容易弄混
5.  特殊情况下使用

## 3.2 内嵌式JS
```javascript
<script>
     alert('Hello World!');
</script>
```


可以将多行JS代码写到`<script>`标签中
内嵌 JS 是学习时常用的方式


## 3.3 外部JS
`<script src="my.js"></script>`

利于HTML页面代码结构化，把单独JS代码独立到HTML页面之外，既美观，又方便
引用外部JS文件的script标签中间不可以写代码
适合于JS代码量比较大的情况


## 断点调试
浏览器中按 F12–> sources -->找到需要调试的文件–>在程序的某一行设置断点(在行数点一下)
刷新浏览器
Watch: 监视，通过watch可以监视变量的值的变化，非常的常用
F11: 程序单步执行，让程序一行一行的执行，这个时候，观察watch中变量的值的变化
