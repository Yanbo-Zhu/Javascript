ES5 给我们新增了一些方法，可以很方便的操作数组或者字符串

数组方法
字符串方法
对象方法

# 1 数组方法
迭代(遍历)方法：foreach() ，map()，filter()，some() ，every() ;

## 1.1 forEach()
array.forEach(function(currentValue,index,arr))

currentValue : 数组当前项的值
index: 数组当前项的索引
arr: 数组对象本身

```html
<body>
    <script>
        // forEach 迭代(遍历) 数组
        var arr = [1, 2, 3];
        var sum = 0;
        arr.forEach(function(value, index, array) {
            console.log('每个数组元素' + value);
            console.log('每个数组元素的索引号' + index);
            console.log('数组本身' + array);
            sum += value;
        })
        console.log(sum);
    </script>
</body>
```


## 1.2 filter()筛选数组
array.filter(function(currentValue,index,arr))
filter()方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组
注意它直接返回一个新数组
-   currentValue : 数组当前项的值
-   index ：数组当前项的索引
-   arr : 数组对象本身

```html
<body>
    <script>
        // filter 筛选数组
        var arr = [12, 66, 4, 88, 3, 7];
        var newArr = arr.filter(function(value, index) {
            // return value >= 20;
            return value % 2 === 0;
        });
        console.log(newArr);
    </script>
</body>

```


## 1.3 some()
some()方法用于检测数组中的元素是否满足指定条件（查找数组中是否有满足条件的元素）
注意它返回的是布尔值，如果查找到这个元素，就返回true，如果查找不到就返回false
如果找到第一个满足条件的元素，则终止循环，不再继续查找
-   currentValue : 数组当前项的值
-   index ：数组当前项的索引
-   arr : 数组对象本身


```html
<body>
    <script>
        // some 查找数组中是否有满足条件的元素 
        var arr1 = ['red', 'pink', 'blue'];
        var flag1 = arr1.some(function(value) {
            return value == 'pink';
        });
        console.log(flag1);
        // 1. filter 也是查找满足条件的元素 返回的是一个数组 而且是把所有满足条件的元素返回回来
        // 2. some 也是查找满足条件的元素是否存在  返回的是一个布尔值 如果查找到第一个满足条件的元素就终止循环
    </script>
</body>
```


# 2 字符串方法

## 2.1 trim()
​ str.trim()
trim()方法会从一个字符串的两端删除空白字符
trim()方法并不影响原字符串本身，它返回的是一个新的字符串

```html
<body>
    <input type="text"> <button>点击</button>
    <div></div>
    <script>
        // trim 方法去除字符串两侧空格
        var str = '   an  dy   ';
        console.log(str);
        var str1 = str.trim();
        console.log(str1);
        var input = document.querySelector('input');
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        btn.onclick = function() {
            var str = input.value.trim();
            if (str === '') {
                alert('请输入内容');
            } else {
                console.log(str);
                console.log(str.length);
                div.innerHTML = str;
            }
        }
    </script>
</body>
```



# 3 对象方法
## 3.1 Object.keys()
Object.keys()用于获取对象自身所有的属性
效果类似for...in
返回一个由属性名组成的数组

```html
<body>
    <script>
        // 用于获取对象自身所有的属性
        var obj = {
            id: 1,
            pname: '小米',
            price: 1999,
            num: 2000
        };
        var arr = Object.keys(obj);
        console.log(arr);
        arr.forEach(function(value) {
            console.log(value);
            // id
            // pname
            // price
            // num
        })
    </script>
</body>
```


## 3.2 Object.defineProperty()
Object.defineProperty()定义对象中新属性或修改原有的属性(了解)
Object.defineProperty(obj, prop, descriptor)

obj : 目标对象
prop : 需定义或修改的属性的名字
descriptor : 目标属性所拥有的特性


第三个参数 descriptor 说明：以对象形式{ }书写
value：设置属性的值，默认为undefined
writeable: 值是否可以重写 true | false 默认为false
enumerable: 目标属性是否可以被枚举 true | false 默认为false
configurable: 目标属性是否可以被删除或是否可以再次修改特性 true | false 默认为false


```html
<body>
    <script>
        // Object.defineProperty() 定义新属性或修改原有的属性
        var obj = {
            id: 1,
            pname: '小米',
            price: 1999
        };
        // 1. 以前的对象添加和修改属性的方式
        // obj.num = 1000;
        // obj.price = 99;
        // console.log(obj);
        // 2. Object.defineProperty() 定义新属性或修改原有的属性
        Object.defineProperty(obj, 'num', {
            value: 1000,
            enumerable: true
        });
        console.log(obj);
        Object.defineProperty(obj, 'price', {
            value: 9.9
        });
        console.log(obj);
        Object.defineProperty(obj, 'id', {
            // 如果值为false 不允许修改这个属性值 默认值也是false
            writable: false,
        });
        obj.id = 2;
        console.log(obj);
        Object.defineProperty(obj, 'address', {
            value: '中国山东蓝翔技校xx单元',
            // 如果只为false 不允许修改这个属性值 默认值也是false
            writable: false,
            // enumerable 如果值为false 则不允许遍历, 默认的值是 false
            enumerable: false,
            // configurable 如果为false 则不允许删除这个属性 不允许在修改第三个参数里面的特性 默认为false
            configurable: false
        });
        console.log(obj);
        console.log(Object.keys(obj));
        delete obj.address;
        console.log(obj);
        delete obj.pname;
        console.log(obj);
        Object.defineProperty(obj, 'address', {
            value: '中国山东蓝翔技校xx单元',
            // 如果值为false 不允许修改这个属性值 默认值也是false
            writable: true,
            // enumerable 如果值为false 则不允许遍历, 默认的值是 false
            enumerable: true,
            // configurable 如果为false 则不允许删除这个属性 默认为false
            configurable: true
        });
        console.log(obj.address);
    </script>
</body>
```


