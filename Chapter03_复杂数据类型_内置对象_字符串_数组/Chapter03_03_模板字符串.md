

# 1 CSS3 模板字符串 (使用反引号） `xx`

### 1.1.1 认识模板字符串
1、声明（反引号）
let str = 我也是字符串;

- 普通字符串：

```javascript
'字符串'
"字符串"
```

- 模板字符串：

```javascript
`字符串`


```

### 1.1.2 模板字符串与一般字符串的区别

- 对于普通用法**没有区别**

```javascript
const name1 = 'zjr';
const name2 = `zjr`;
console.log(name1, name2, name1 === name2);
// zjr zjr true
```

- 字符串拼接的**巨大区别**

```javascript
const person = {
    name: 'zjr',
    age: 18,
    sex: '男'
};

const info =
    '我的名字是：' + person.name +
    '，性别是：' + person.sex +
    '，今年：' + person.age + '岁';

console.log(info);

// 我的名字是：zjr，性别是：男，今年：18岁
```

```javascript
const person = {
    name: `zjr`,
    age: 18,
    sex: `男`
};

const info = `我的名字是：${person.name}，性别是：${person.sex}，今年：${person.age}岁`;

console.log(info);

// 我的名字是：zjr，性别是：male，今年：18岁
```

> 模板字符串最大的优势：方便注入！

### 1.1.3 模板字符串的特点

#### 1.1.3.1 输出多行字符串

```javascript
// 一般字符串
const info = '第一行\n第二行';
console.log(info);
/*
第一行
第二行
*/


// 模板字符串
const info = `第一行
第二行`;	// 注意不能有缩进
console.log(info);
/*
第一行
第二行
*/
```

> 模板字符串中，所有的空格、换行或缩进都会被保存在输出中


#### 1.1.3.2 内容中可以直接出现换行符
```js
let str =`<ul>
			<li>sdgsdg</li>
			<li>sdgsdg</li>
			<li>sdgsdg</li>
			<li>sdgsdg</li>
		  </ul>`

let resilt = {
    name: 'zhangsan',
    age: 20,
    sex：'男'
}
let html = ` <div>
    <span>${result.name}</span>
    <span>${result.name}</span>
    <span>${result.name}</span>
</div> `;

```

#### 1.1.3.3 输出 `` ` 和 `\` 等特殊字符

```javascript
const info = `\``;	// ```
const info = `\\`;	// `\`
const info = `""`;	// `""`
const info = `''`;	// `''`
```


#### 1.1.3.4 模板字符串的注入

```javascript
const username = 'alex';
const person = {
    age: 18,
    sex: `male`
};
const getSex = function (sex) {
    return sex === `male` ? '男' : '女';
};

const info = `${username},${person.age + 2},${getSex(person.sex)}`;
console.log(info);

// alex,20,男
```

> 模板字符串的 `${}` 注入可以兼容几乎所有的值！
>
> 模板字符串、字符串、数值、布尔值、表达式、函数……（只要结果是个 “值” 即可）

##### 1.1.3.4.1 模板字符串中可以解析变量。
```js
let name = '张三';
let sayHello = `hello,my name is ${name}`; // hello,my name is zhangsan 

```

变量拼接
```js
let lovest ='dfsd';
let out = `${lovest}dgdgdgs`;
//out就为dfsddgdgdgs
```

##### 1.1.3.4.2 在模板字符串可以调用函数。

```js
const aryHello = function () {
    return '哈哈哈哈 追不到我吧 我就是这么强大';
};
let greet = `${sayHello()} 哈哈哈哈`;
console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈 
```


### 1.1.4 模板字符串的应用

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <title>模板字符串的应用</title>
    <style>
        body {
            padding: 50px 0 0 300px;
            font-size: 22px;
        }

        ul {
            padding: 0;
        }

        p {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
<p>学生信息表</p>
<ul id="list">
    <li style="list-style: none;">信息加载中……</li>
</ul>

<script>
    // 数据（此处只是模拟数据，后期是通过 Ajax 从后台获取）
    const students = [
        {
            username: 'Alex',
            age: 18,
            sex: 'male'
        },
        {
            username: 'ZhangSan',
            age: 28,
            sex: 'male'
        },
        {
            username: 'LiSi',
            age: 20,
            sex: 'female'
        }
    ];

    const list = document.getElementById('list');

    let html = '';

    for (let i = 0; i < students.length; i++) {
        html += `<li>我的名字是：${students[i].username},${students[i].sex},${students[i].age}</li>`;
    }

    list.innerHTML = html;
</script>
</body>
</html>
```

<img src="https://i0.hdslb.com/bfs/album/55bc9aaadc9819646ff0adc3ab841d8d9247fd03.png" alt="image-20220315130229559" style="zoom:50%;" />

