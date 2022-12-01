数组(Array)是指一组数据的集合，其中的每个数据被称作元素，在数组中可以存放任意类型的元素。数组是一种将一组数据存储在单个变量名下的优雅方式。

//普通变量一次只能存储一个值
var num = 10;
//数组一次可以存储多个值
var arr =[1,2,3,4,5];



# 1 创建数组
JavaScript 中创建数组有两种方式：
利用 new 创建数组
利用数组字面量创建数组

①利用 new 创建数组
var 数组名 = new Array();
var arr = new Array(); //创建一个新的空数组

注意 Array()，A要大写

②利用数组字面量创建数组
// 1.利用数组字面量方式创建空的数组 
var 数组名 =[];
// 2.使用数组字面量方式创建带初始值的数组
var 数组名 =['小白','小黑','小黄','瑞奇'];
// 3.数组中可以存放任意类型的数据，例如字符串，数字，布尔值等
var arrStus =['小白'，12,true,28.9];

- 数组的字面量是方括号 
- 声明数组并赋值称为数组的初始化
- 这种字面量方式也是我们以后最多使用的方式

# 2 数组的索引（下标）
索引 (下标) ：用来访问数组元素的序号（数组下标从 0 开始）

//定义数组
var arrStus = [1,2,3];
//获取数组中的第2个元素
alert(arrStus[1]);

# 3 遍历数组
我们可以通过 for 循环索引遍历数组中的每一项

// 数组索引访问数组中的元素
var arr = ['red','green', 'blue'];
console.log(arr[0]) // red
console.log(arr[1]) // green
console.log(arr[2]) // blue

// for循环遍历数组
var arr = ['red','green', 'blue'];
for (var i = 0; i < arr.length; i++){
    console.log(arrStus[i]);
}


# 4 数组的长度
使用“数组名.length”可以访问数组元素的数量（数组长度）

var arrStus = [1,2,3];
alert(arrStus.length);  // 3


注意：
此处数组的长度是数组元素的个数 ，不要和数组的索引号混淆
当我们数组里面的元素个数发生了变化，这个 length 属性跟着一起变化

# 5 数组中新增元素
①通过修改 length 长度新增数组元素
可以通过修改 length 长度来实现数组扩容的目的

length 属性是可读写的

var arr = ['red', 'green', 'blue', 'pink'];
arr.length = 7;
console.log(arr);
console.log(arr[4]);
console.log(arr[5]);
console.log(arr[6]);

其中索引号是 4，5，6 的空间没有给值，就是声明变量未给值，默认值就是 undefined

②通过修改数组索引新增数组元素
可以通过修改数组索引的方式追加数组元素

不能直接给数组名赋值，否则会覆盖掉以前的数据

这种方式也是我们最常用的一种方式

var arr = ['red', 'green', 'blue', 'pink'];
arr[4] = 'hotpink';
console.log(arr);


## 5.1 例子1
1.新建一个数组，里面存放10个整数（ 1~10）， 要求使用循环追加的方式输出： [1,2,3,4,5,6,7,8,9,10]

①使用循环来追加数组。
②声明一个空数组 arr。
③循环中的计数器 i 可以作为数组元素存入。
由于数组的索引号是从0开始的， 因此计数器从 0 开始更合适，存入的数组元素要+1。

```js
var arr = [];
for (var i = 0; i < 10; i++){
    arr[i] = i + 1;
}
console.log(arr);
```


## 5.2 例子2
2.将数组 [2, 0, 6, 1, 77, 0, 52, 0, 25, 7] 中大于等于 10 的元素选出来，放入新数组

①声明一个新的数组用于存放新数据。
②遍历原来的数组，找出大于等于 10 的元素。
③依次追加给新数组 newArr。


实现代码1：
```js
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
// 定义一个变量 用来计算 新数组的索引号
var j = 0;
for (var i = 0; i < arr.length; i++) {
    if (arr[i] >= 10) {
        // 给新数组
        newArr[j] = arr[i];
        // 索引号 不断自加
        j++;
    }
}
console.log(newArr);
```

实现代码2：
```js
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
for (var i = 0; i < arr.length; i++) {
    if (arr[i] >= 10) {
        // 给新数组
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```



# 6 删除指定数组元素


将数组[2, 0, 6, 1, 77, 0, 52, 0, 25, 7]中的 0 去掉后，形成一个不包含 0 的新数组。

1
```js
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
for(var i = 0; i <arr.length; i++){
    if(arr[i] != 0){
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```


2 
//老师代码
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];   // 空数组的默认的长度为 0 
// 定义一个变量 i 用来计算新数组的索引号

```js
for (var i = 0; i < arr.length; i++) {
    // 找出大于 10 的数
    if (arr[i] != 0) {
        // 给新数组
        // 每次存入一个值，newArr长度都会 +1  
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```



# 7 翻转数组
将数组 [‘red’, ‘green’, ‘blue’, ‘pink’, ‘purple’] 的内容反过来存放

// 把旧数组索引号的第4个取过来(arr.length - 1),给新数组索引号第0个元素(newArr.length)

```js
var arr = ['red','green','blue','pink','purple'];
var newArr = [];
for (var i = arr.length -1; i>=0; i--){
    newArr[newArr.length] = arr[i];
}
console.log(newArr);
```


# 8 数组排序
冒泡排序

将数组 [5, 4, 3, 2, 1]中的元素按照从小到大的顺序排序，输出： 1，2，3，4，5

```js
var arr = [5,4,3,2,1];
for (var i = 0; i < arr.length-1; i++){ //外层循环管趟数，5个数共交换4躺
    for (var j = 0; j <= arr.length - i - 1; j++){
        //里层循环管每一趟交换的次数
        //前一个和后面一个数组元素相比较
        if(arr[j] > arr[j+1]){
            var temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }  
    }
}
console.log(arr);
```




# 9 案例

1.请将 [“关羽”,“张飞”,“马超”,“赵云”,“黄忠”,“刘备”,“姜维”]; 数组里的元素依次打印到控制台

var arr = ["关羽","张飞","马超","赵云","黄忠","刘备","姜维"]; 
// 遍历  从第一个到最后一个
for(var i = 0; i < arr.length; i++ )  { 
   console.log( arr[i] );
} 


2.求数组 [2,6,1,7, 4] 里面所有元素的和以及平均值

①声明一个求和变量 sum。
①遍历这个数组，把里面每个数组元素加到 sum 里面。
①用求和变量 sum 除以数组的长度就可以得到数组的平均值。
```js
var arr = [2, 6, 1, 7, 4];
var sum = 0;
var average = 0;
for (var i = 0; i < arr.length; i++) {
    sum += arr[i];
}
average = sum / i; //此时i为5
//      average = sum / arr.length;
console.log('和为' + sum);
console.log('平均值为' + average);
```


3.求数组[2,6,1,77,52,25,7]中的最大值

①声明一个保存最大元素的变量 max。
②默认最大值可以取数组中的第一个元素。
③遍历这个数组，把里面每个数组元素和 max 相比较。
④如果这个数组元素大于max 就把这个数组元素存到 max 里面，否则继续下一轮比较。
⑤最后输出这个 max。

方法1
```js
 var arr = [2, 6, 1, 77, 52, 25, 7];
        var max = arr[0];
        var temp;
        for (var i = 0; i < arr.length; i++) {
            if (max < arr[i]) {
                temp = max;
                max = arr[i];
                arr[i] = temp;
            }
        }
        console.log('最大值为' + max);

```


方法二：
```js
var arrNum = [2,6,1,77,52,25,7];
var maxNum = arrNum[0]; // 用来保存最大元素,默认最大值是数组中的第一个元素
// 从0 开始循环数组里的每个元素
for(var i = 0;i< arrNum.length; i++){
    // 如果数组里当前循环的元素大于 maxNum，则保存这个元素和下标
    if(arrNum[i] > maxNum){
        maxNum = arrNum[i]; // 保存数值到变量 maxNum
    }
}
```


4.将数组 [‘red’, ‘green’, ‘blue’, ‘pink’] 里面的元素转换为字符串

思路：就是把里面的元素相加就好了，但是注意保证是字符相加

①需要一个新变量 str 用于存放转换完的字符串。
②遍历原来的数组，分别把里面数据取出来，加到字符串变量 str 里面。
```js
var arr = ['red','green','blue','pink'];
var str ='';
for(var i = 0; i < arr.length; i++){
    str += arr[i];
}
console.log(str);
// redgreenbluepink

```


5.将数组 [‘red’, ‘green’, ‘blue’, ‘pink’] 转换为字符串，并且用 | 或其他符号分割

①需要一个新变量用于存放转换完的字符串 str。
①遍历原来的数组，分别把里面数据取出来，加到字符串里面。
①同时在后面多加一个分隔符。

```js
var arr = ['red', 'green', 'blue', 'pink'];
var str = '';
var separator = '|';
for (var i = 0; i < arr.length; i++) {
   str += arr[i] + separator;
}
console.log(str);
// red|green|blue|pink

```
