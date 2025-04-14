
javascript, array 的 built-in function 

In JavaScript gibt es eine Reihe von beliebten Higher-Order Functions (HOFs), die auf Arrays und Objekte angewendet werden. Diese Funktionen helfen dabei, das Arbeiten mit Arrays und Objekten auf deklarative und funktionale Weise zu gestalten.

push()
pop()
shift()
unshift()
join()
split()
reverse()
sort()
concat()
splice()
slice()
indexOf()
lastIndexOf()

![](image/Pasted%20image%2020241123151245.png)


# 1 遍历数组 (for, forEach(), for in, for..of  )

用 listOfStuff[i].value 是无效的, 是会报错的 

```js
// 数组索引访问数组中的元素
var arr = ['red','green', 'blue'];
console.log(arr[0]) // red
console.log(arr[1]) // green
console.log(arr[2]) // blue

// for zeigt auch leere Elemente als undefined;   does show empty slots as undefined
// empty 处 显示 为 undefined in Console 
// booleanische Value (值 为 true 或者 false) . 值 为 null, 值为字符串类型的  处的 元素 都能正常显示. 
for(let i=0; i<listOfStuff.length; i++){
    console.log(listOfStuff[i]);  
}


// for循环遍历数组
var arr = ['red','green', 'blue'];
for (var i = 0; i < arr.length; i++){
    console.log(arrStus[i]);
}

// forEach() zeigt nicht die leeren Elemente
// empty 处 显示 不会显示为 undefined in Console, 根本就不显示在 console 中 
// booleanische Value (值 为 true 或者 false) . 值 为 null, 值为字符串类型的  处的 元素 都能正常显示. 
 
listOfStuff.forEach(element => {
    console.log(element);
});



// for...in zeigt nicht die leeren Elemente
// empty 处 显示 不会显示为 undefined in Console, 根本就不显示在 console 中. do not show undefineds,
// booleanische Value (值 为 true 或者 false) . 值 为 null, 值为字符串类型的  处的 元素 都能正常显示. 
for(let item in listOfStuff){
    console.log(listOfStuff[item]);
}

```


```js
 /*write a function that takes any array or list and some text 
 and iterates over the array with for*/
 
 function denseArray(arr,text){
  let showArr="";	
  let i=0;
  let len=arr.length;
  for(i;i<len;i++){
   showArr+=" "+arr[i];
  }
  console.log("for: " + text + showArr);
 }

 denseArray(listOfStuff, "listOfStuff");
 
 console.log("--------------1");




 /*write a function that takes any array or list and some text 
 and iterates of the array with for-in*/
 function sparseArray(arr,text){
  let showArr="";
  for(let item in arr){
   showArr+=" "+arr[item];
  }
  console.log("for in: "+ text + showArr);
 }

 sparseArray(listOfStuff,"listOfStuff");




 /*Write it again as Arrow-Function*/
 const denseArr = (arr, text) => {
    let showArr = "";
    for (let item in arr) {
      showArr += " " + arr[item];
    }
    let result = "for: " + text + showArr;
    return result;
  };
 console.log(denseArr(listOfStuff, "listOfStuff"));





 /* Write it again with forEach() */
  const denseForEach = (arr, text) => {
    let showArr = "";
    arr.forEach(element => {
      showArr += " " + element;
    });
    let result = "forEach(): " + text + showArr;
    return result;
  };

  console.log(denseForEach(listOfStuff, "listOfStuff: "));
```


## 1.1 for..in, for..of 
如果  
```js
let anyObject = {
    firstName:	"me",
    lastName:	"Object",
    human:	false
};
```

 `for..of` 得到的是 key的值, firstName, lastName, human
 `for..in` 得到的是 value 的值,  "me", "Object", false

> Both `for..of` and `for..in` statements iterate over lists; the values iterated on are different though, `for..in` returns a list of keys on the object being iterated, whereas `for..of` returns a list of values of the numeric properties of the object being iterated.
> 
Here is an example that demonstrates this distinction:
 
 ```javascript
> let list = [4, 5, 6];
> 
> for (let i in list) {
>     console.log(i); // "0", "1", "2",
> }
> 
> for (let i of list) {
>     console.log(i); // 4, 5, 6
> }
> 
```

 Another distinction is that `for..in` operates on any object; it serves as a way to inspect properties on this object. 
 `for..of` on the other hand, is mainly interested in values of iterable objects. Built-in objects like `Map` and `Set` implement `Symbol.iterator` property allowing access to stored values.
 
 ```javascript
> let pets = new Set(["Cat", "Dog", "Hamster"]);
> pets["species"] = "mammals";
> 
> for (let pet in pets) {
>     console.log(pet); // "species"
> }
> 
> for (let pet of pets) {
>     console.log(pet); // "Cat", "Dog", "Hamster"
> }
 ```

## 1.2 forEach()
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

---

Die Methode forEach wird verwendet, um eine gegebene Funktion auf jedes Element eines Arrays anzuwenden. Sie verändert das Array nicht und ==gibt auch keinen Wert zurück.==

```js
let numbers = [1, 2, 3, 4];
numbers.forEach(function(num) {
    console.log(num * 2);
}); // Output: 2, 4, 6, 8
```

Verwendung: Für das Iterieren über ein Array, wenn man eine Aktion für jedes Element ausführen möchte, ohne das Array zu modifizieren.


# 2 修改数组元素的方法 push() pop() unshift() shift()
| 方法名                   | 说明                                  | 返回值                   |
| --------------------- | ----------------------------------- | --------------------- |
| listOfStuff[8] = 100; | listOfStuff 原先只有 4 位, 直接在第八位 插入 100 |                       |
| push(参数1…)            | 末尾添加一个或多个元素，注意修改原数组                 | 并返回新的长度               |
| pop()                 | 删除数组最后一个元素, 修改原数组                   | 返回它删除的元素的值            |
| unshift(参数1…)         | 向数组的开头添加一个或更多元素，注意修改原数组             | 并返回新的长度               |
| shift()               | 删除数组的第一个元素，数组长度减1，无参数，修改原数组         | 并返回第一个元素 (返回它删除的元素的值) |



```js
// push() 在我们数组的末尾，添加一个或者多个数组元素 push 推
var arr = [1, 2, 3];
arr.push(4, '秦晓');
console.log(arr);
console.log(arr.push(4, '秦晓'));
console.log(arr);
// push 完毕之后，返回结果是新数组的长度

myArray.push("Zweites Element");
console.log(myArray); // ["Erstes Element", "Zweites Element"]



// pop() 它可以删除数组的最后一个元素，一次只能删除一个元素
arr.pop(); //不加参数

let lastElement = a.pop(); // entfernt das letzte Element console.log(a); // das Array ohne das letzte Element console.log(lastElement); // das entfernte Element





// unshift 在我们数组的开头 添加一个或者多个数组元素
arr.unshift('red');
console.log(arr);





// shift() 它剋删除数组的第一个元素,一次只能删除一个元素
arr.shift(); //不加参数

let firstElement = a.shift(); // entfernt das erste Element console.log(a); // das Array ohne das erste Element console.log(firstElement); // das entfernte Element

```



例子: 筛选数组
有一个包含工资的数组[1500,1200,2000,2100,1800],要求把数组中工资超过2000的删除，剩余的放到新数组里面
```js
var arr = [1500, 1200, 2000, 2100, 1800];
var newArr = [];
for (var i = 0; i < arr.length; i++) {
    if (arr[i] < 2000) {
        newArr.push(arr[i]);
    }
}
console.log(newArr);
```



# 3 翻转数组 reverse()	
|方法名	|说明	|是否修改原数组|
|---|---|---|
|reverse()	|颠倒数组中元素的顺序，无参数	|该方法会改变原来的数组，返回新数组|
|sort()|	对数组的元素进行排序	|该方法会改变原来的数组，返回新数组|

1

```js
// 1.翻转数组
var arr = ['pink','red','blue'];
arr.reverse();
console.log(arr);  

反转前: ['H', 'a', 'l', 'l', 'o', '!']
反转后: ['!', 'o', 'l', 'l', 'a', 'H']

```

2 
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



# 4 数组排序 sort()

| 方法名       | 说明             | 是否修改原数组           |
| --------- | -------------- | ----------------- |
| reverse() | 颠倒数组中元素的顺序，无参数 | 该方法会改变原来的数组，返回新数组 |
| sort()    | 对数组的元素进行排序     | 该方法会改变原来的数组，返回新数组 |



sort sortiert die Elemente eines Arrays in-place nach einer bestimmten Funktion. Das ursprüngliche Array wird dabei verändert.

```js
let numbers = [4, 2, 3, 1];
numbers.sort(function(a, b) {
    return a - b;
});
console.log(numbers); 
// [1, 2, 3, 4]


let numbers = [4, 2, 3, 1];
numbers.sort(function(a, b) {
    return a > b ? 1 : -1;
});
console.log(numbers); 
// [1, 2, 3, 4]



let hasEven = numbers.some(); //会报错
let hasEven = numbers.sort(); //不会报错, 以为 sort() 有默认的 comparator

```


`a > b ? 1 : -1;` 的解释

```
// Syntax 
(Bedingung) ? (Ausdruck_wenn_true) : (Ausdruck_wenn_false);

```

Der ternäre Operator (auch Conditional Operator genannt) ist ein kompakter Ausdruck in Programmiersprachen wie JavaScript, um einfache Bedingungen auszudrücken.

```js

// Beispiel mit if-else-statement:
let x = prompt("Please enter a number: ");
if (x % 2 == 0) {
console.log(x + " is even.");
} else {
console.log(x + " is odd.");
}



// Das gleiche mit dem ternären Operator
let x = prompt("Please enter a number: ");
console.log(x % 2 == 0 ? x + " is even." : x + " is odd.");

// x = 2; Ausgabe: "2 is even"
// x = 5; Ausgabe: "5 is odd."

```



## 4.1 不给入自定义的 vergleichsfunktion
按照  alphabetisch 排序
Wird kein Argument übergeben, dann wird das array alphabetisch sortiert.

sort 的排序规则 很奇怪 

Sort 的结果
1. Nummer 在前: 1, 100, 2, 3
2. 然后是 string
3. 然后是 boolean value 混杂着 null, 按照  alphabetisch 排序
4. 然后是 empty, undefined Elemente werden an das Ende des arrays gesetzt.

```js
var arr1 = [3,4,7,1];
arr1.sort();
console.log(arr1);


 let numbers = [7,1,102,40,10];
  console.log(numbers);  // [7, 1, 102, 40, 10]
 console.log(numbers.sort()); // [1, 10, 102, 40, 7]


let listOfAllTypes = [true,5,null,1,100,,undefined,"a","A","b","B","z",false,"f","F","g","m","s",null];
console.log(listOfAllTypes);
listOfAllTypes.sort();
console.log(listOfAllTypes); // [1, 100, 5, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty]



console.log(listOfStuff);  // [1, 2, 3, empty, true, 'Hallo Welt', false, null, empty × 2, 100]
console.log(listOfStuff.sort()); // [1, 100, 2, 3, 'Hallo Welt', false, null, true, empty × 3]    
```

## 4.2 自定义的 Vergleichsfunktion 
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

A 为当前元素, b 为下一个元素 
如果 compareFn(a, b) 大于 0，b 会被排列到 a 之前。
如果 compareFn(a, b) 小于 0，那么 a 会被排列到 b 之前；
如果 compareFn(a, b) 等于 0，a 和 b 的相对位置不变。备注：ECMAScript 标准并不保证这一行为，而且也不是所有浏览器都会遵守（例如 Mozilla 在 2003 年之前的版本）；
compareFn(a, b) 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。

function(a,b){return a-b;} : Wenn a<b,  a-b 小于零, 则a 这个元素就往link移动 ,  a 会被排列到 b 之前
function(a,b){return b-a;} : Wenn a<b,  a-b 大于零, 则b 这个元素就往link移动 ,  b 会被排列到 a 之前

```js
// 对于双位数
var arr = [1,64,9,61];
arr.sort(function(a,b) {
     return b - a;  //降序的排列
     return a - b; //升序
 	}
 )


// 可以变为 arrow function
listOfStuff.sort(function(a,b){return a-b;});
listOfNumbers.sort((a,b) => a-b);
```

```js
 listOfAllTypes = [1, 100, 5, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty];
 console.log(listOfAllTypes);  // [1, 100, 5, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty]
 
 listOfAllTypes.sort((a,b) => a-b);
 console.log(listOfAllTypes); // [1, 5, 100, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', null, null, 's', true, 'z', undefined, empty]
 
 listOfAllTypes.sort((a,b) => b-a);
 console.log(listOfAllTypes); // [100, 5, 1, 'A', 'B', 'F', 'a', 'b', 'f', false, 'g', 'm', true, null, null, 's', 'z', undefined, empty]


 listOfAllTypes = [true,5,null,1,100,,undefined,"a","A","b","B","z",false,"f","F","g","m","s",null];
 console.log(listOfAllTypes);
 listOfAllTypes.sort((a,b) => a-b);
 console.log(listOfAllTypes); // [null, true, 1, 5, 100, 'a', 'A', 'b', 'B', 'z', false, 'f', 'F', 'g', 'm', 's', null, undefined, empty]
 listOfAllTypes.sort((a,b) => b-a);
 console.log(listOfAllTypes); //  [100, 5, true, 1, null, 'a', 'A', 'b', 'B', 'z', false, 'f', 'F', 'g', 'm', 's', null, undefined, empty]


```

## 4.3 冒泡排序
将数组 `[5, 4, 3, 2, 1]`中的元素按照从小到大的顺序排序，输出： 1，2，3，4，5

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



# 5 数组索引 indexOf() lastIndexOf()
|方法名	|说明|	返回值|
|---|---|---|
|indexOf(true, 4)或者 indexOf("Z") 	|数组中查找给定元素的第一个索引	|如果存在返回索引号，如果不存在，则返回-1, gibt den index eines gesuchten Wertes zurück, Wird ein Wert nicht gefunden, liefert sie -1 zurück|
|lastIndexOf()	|在数组的最后一个索引，从后向前索引, den ersten Index von hinten 	|如果存在返回索引号，如果不存在，则返回-1|

 gibt den index eines gesuchten Wertes aus einem array zurück. 
 Wenn ein Wert nicht gefunden wird, dann gibt die Methode -1 zurück.
 Dabei wird das array mit indexOf() von vorn beginnend durchlaufen 
 und mit lastIndexOf() von hinten.
 Optional kann als zweites Argument der index übergeben werden, 
 ab dem gesucht werden soll.

```js
var arr = ['red','green','blue','pink','blue'];

console.log(arr.indexOf('blue'));  // 2
console.log(listOfStuff.indexOf(red,4));   // erst ab index=4 suchen:


console.log(arr.lastIndexOf('blue')); // 4

// 如果是查找字符串的话, 是 case -sensitive 的
listOfStuff.push("z");
console.log(listOfStuff.indexOf("Z")); // 结果是 找不到 显示  -1 

``` 



# 6 数组的连接 concat() and `[...arr, ...secondArray]`


| 方法名                                 | 说明               | 返回值                 |
| ----------------------------------- | ---------------- | ------------------- |
| let a = arr.concat(secondArray)     | 连接两个或多个数组 不影响原数组 | 返回一个新的数组, 原来的数组不受影响 |
| `let a = [...arr, ...secondArray] ` |                  |                     |


```js
 console.log(numbers); // [1, 7, 10, 40, 102]
 let newList=numbers.concat(4,5);  
 console.log(newList); // [1, 7, 10, 40, 102, 4, 5]
 console.log(numbers); // [1, 7, 10, 40, 102]

 // arr 和 aecondArray 都是数组 

 newList=numbers.concat(newList,['aha'],[true,false,[0]],5678);
 console.log(newList); // [1, 7, 10, 40, 102, 1, 7, 10, 40, 102, 4, 5, 'aha', true, false, Array(1), 5678]

```


# 7 数组的截取 

| 方法名      | 说明                                                    | 返回值                                            |
| -------- | ----------------------------------------------------- | ---------------------------------------------- |
| slice()  | 数组截取slice(begin,end)                                  | 返回被截取项目的新数组,  原来的数组不受影响                        |
| splice() | 数组删除splice(第几个开始要删除的个数), 从某个位置移除数组的几个元素 ，并在这个位置上添加新元素 | 原数组被改为被删除项目后的数组，会return一个数组, 这个额数据包含了 那些元素被删除了 |

### 7.1.1 slice()



1 
slice() 中给入一个值 
Wird nur ein Argument übergeben, dann spezifiziert dieses den Anfang des Teilbereiches und das Ende wird durch das Ende des array spezifiziert.
从 index =3 的地方开始取值, 
取到最后 最后一个值要被取进去 

```js
// Syntax
arrayName.slice(indexFrom, indexToButNotIncluded);
// erstellt einen Teil des Arrays von Index indexFrom bis 
// (aber nicht einschließlich) indexToButNotIncluded
```


```js
 console.log(numbers); // [1, 7, 10, 40, 102]
 console.log(numbers.slice(3)); // [40, 102]
 
```

Negative Argumente beginnen mit dem Teilbereich am Ende des arrays, zählen aber nach rechts.
从 index 为倒数第三的地方开始取,  包括 index=-3 的这个位置  的地方开始取值,  取到最后, 最后一个值要被取进去 
```js
 console.log(numbers.slice(-3));
```

2 
slice() 中给入两个值 
 Die Methode gibt einen beliebigen Teilbereich aus einem array zurück.   Mit zwei Argumenten werden Anfang und Ende des Teilbereiches spezifiziert. 
 Dabei wird der Wert des ersten Argumentes mit ausgegeben, aber nicht der des zweiten. Das ursprüngliche array wird nicht verändert.
```js
 console.log(numbers); //[ 1, 7, 10, 40, 102]
 let partNumbers = numbers.slice(1,3); //   从 index =1 的地方开始取值, 到 index=3 , index=3 的值不被取
 console.log(partNumbers); // [7, 10]


// Example
let slicedArray = a.slice(1, 3);
// erstellt einen Teil des Arrays von Index 1 bis (aber nicht einschließlich) 3
console.log(slicedArray); // der abgeschnittene Teil des Arrays
```


### 7.1.2 splice()

entfernen und hinzufügen

ändert den Inhalt eines Arrays, indem vorhandene Elemente entfernt oder ersetzt und/oder neue Elemente hinzugefügt werden. 
==对原数组直接进行改变== Dies geschieht direkt im Array (in-place), ohne dass ein neues Array erstellt wird.


 Mit dieser Methode können Elemente sowohl eingefügt als auch entfernt werden.  Dabei wird das ursprüngliche array verändert.
  Die Methode gibt ein array zurück, welches die entfernten Elemente enthält.  
 - Das erste Argument spezifiziert die Position des Einfügens oder Entfernens.
 - Das zweite Argument spezifiziert die Anzahl der Elemente,  die entfernt werden sollen.
 - Wird das zweite Argument nicht übergeben, wird das Ende des Arrays angenommen.
 - Ab dem 3. Argument kann hinzugefügt werden.
 - 如果只有 前两个 argument, 则 效果为移除 n Elemente ( Wert von zweiten Argument) from der Position index  ( Wert von ersten Argument)

给入三个值 
```js
// Syntax
arrayName.splice(index, n, elements); 
// ersetzt n Elemente an der Position index gegen elements

// Example
a.splice(1, 1, 'New element');
// ersetzt ein Element an der Position 1 gegen 'New element'


let arr_3 = [1, 2, 3];
// 第一个1的意义: Entfernt das Element an Index 1
// 第二个1的意义 (ab 1 position nur  1 elemnt modify)
// 第三个neu的意义: fügt "neu" hinzu
arr_3.splice(1, 1, "neu"); 
console.log(arr_3); // [1, "neu", 3]


// 如果 第二值的大于 数组本身长度
arr_3.splice(1, 5, "neu"); // return  [1, "neu", neu", neu",neu",neu"]  // 5 elemnts will be removed and 5 elemnts will be added. although we have only 3 elemnts in array arr_3 orignally

```




 
```js
console.log(numbers); //  [1, 7, 10, 40, 102]
let spliceNumber = numbers.splice(1,0,5,true);
console.log(spliceNumber); // []
console.log(numbers); // [1, 5, true, 7, 10, 40, 102]


console.log(numbers); //  [1, 7, 10, 40, 102]
let spliceNumber = numbers.splice(1,1,5,true);
console.log(spliceNumber); // [7]
console.log(numbers); // [1, 5, true,10, 40, 102]


// Übung: finde alle true und entferne sie
function findTrue(arr){
    let i=0;
    while(i !== -1){
        i = arr.indexOf(true);
        console.log(i);
        arr.splice(i,1);
    }
}

findTrue(listOfStuff);
console.log(listOfStuff);

```


# 8 map

map erstellt ein neues Array, indem es eine gegebene Funktion auf jedes Element des ursprünglichen Arrays anwendet. Das ursprüngliche Array bleibt unverändert.

```js
let numbers = [1, 2, 3, 4];
let doubled = numbers.map(function(num) {
    return num * 2;
});
console.log(doubled); // [2, 4, 6, 8]
```

Verwendung: Wenn man ein neues Array basierend auf den Werten eines anderen Arrays erzeugen möchte.

---



`map()`方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。

```js
    let a = [0, 1, 2, 3, 4, [5, 6, null]];

 // Die Abbildung jeden Wertes auf je ein Funktionsergebnis (hier: gerade Zahlen)
    a.map((i) => {return i * 2;});  // 0,2,4,6,8,NaN

    
```

```js
var numbers = [1, 2, 3];

numbers.map(function (n) {
  return n + 1;
});
// [2, 3, 4]

numbers
// [1, 2, 3]
```

上面代码中，`numbers`数组的所有成员依次执行参数函数，运行结果组成一个新数组返回，原数组没有变化。

`map()`方法接受一个函数作为参数。该函数调用时，`map()`方法向它传入三个参数：当前成员、当前位置和数组本身。

```js
[1, 2, 3].map(function(elem, index, arr) {
  return elem * index;
});
// [0, 2, 6]
```

上面代码中，`map()`方法的回调函数有三个参数，`elem`为当前成员的值，`index`为当前成员的位置，`arr`为原数组（`[1, 2, 3]`）。

`map()`方法还可以接受第二个参数，用来绑定回调函数内部的`this`变量（详见《this 变量》一章）。

```js
var arr = ['a', 'b', 'c'];

[1, 2].map(function (e) {
  return this[e];
}, arr)
// ['b', 'c']
```

上面代码通过`map()`方法的第二个参数，将回调函数内部的`this`对象，指向`arr`数组。

如果数组有空位，`map()`方法的回调函数在这个位置不会执行，会跳过数组的空位。

```js
var f = function (n) { return 'a' };

[1, undefined, 2].map(f) // ["a", "a", "a"]
[1, null, 2].map(f) // ["a", "a", "a"]
[1, , 2].map(f) // ["a", , "a"]
```

上面代码中，`map()`方法不会跳过`undefined`和`null`，但是会跳过空位。


# 9 filter 

filter erstellt ein neues Array, indem es eine Funktion auf jedes Element des Arrays anwendet und nur die Elemente zurückgibt, die die Bedingung erfüllen (also für die die Funktion true zurückgibt).

```js
let numbers = [1, 2, 3, 4];
let evenNumbers = numbers.filter(function(num) {
    return num % 2 === 0;
});
console.log(evenNumbers); // [2, 4]

function filter(array, test) {
  let passed=[];
  for (let i=0; i<array.length; i++)
    if (test(array[i]))
      passed.push(array[i]);
  return passed;
};

filter(ancestry, function(person) {
  return person.born>1900 && person.born<1925;
});

ancestry.filter(function(person) {
  return person.father=="Carel Haverbeke";
});
```

Verwendung: Wenn man ein Array nach bestimmten Kriterien filtern möchte.

- Die Funktion `**filter(...)**` entnimmt einem Feld diejenigen Elemente, welche einen "Test" erfüllen
- `**test**` ist ein **_Funktionsargument_**, das die Referenz auf eine Funktion enthält, welche die Bedingung des Tests enthält
- Hier: Beispielimplementierung von `**filter()**`

- Hier: Verwendung der auf Feldern definierten Standardmethode `**filter()**`


----


array.filter(function(currentValue,index,arr))
filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组
注意它直接返回一个新数组
-   currentValue : 数组当前项的值
-   index ：数组当前项的索引
-   arr : 数组对象本身

```js
let a = [0, 1, 2, 3, 4, [5, 6, null]];

// Das Filtern auf genau jene Elemente, für die die Bedingung WAHR lautet (hier: ungerade Zahlen)
a.filter((i) => {return i % 2 == 1 ? true : false;});  // 1,3

```

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



`filter()`方法用于过滤数组成员，满足条件的成员组成一个新数组返回。

它的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。该方法不会改变原数组。

```js
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})
// [4, 5]
```

上面代码将大于`3`的数组成员，作为一个新数组返回。

```js
var arr = [0, 1, 'a', false];

arr.filter(Boolean)
// [1, "a"]
```

上面代码中，`filter()`方法返回数组`arr`里面所有布尔值为`true`的成员。

`filter()`方法的参数函数可以接受三个参数：当前成员，当前位置和整个数组。

```js
[1, 2, 3, 4, 5].filter(function (elem, index, arr) {
  return index % 2 === 0;
});
// [1, 3, 5]
```

上面代码返回偶数位置的成员组成的新数组。

`filter()`方法还可以接受第二个参数，用来绑定参数函数内部的`this`变量。

```js
var obj = { MAX: 3 };
var myFilter = function (item) {
  if (item > this.MAX) return true;
};

var arr = [2, 8, 3, 4, 1, 3, 2, 9];
arr.filter(myFilter, obj) // [8, 4, 9]
```

上面代码中，过滤器`myFilter()`内部有`this`变量，它可以被`filter()`方法的第二个参数`obj`绑定，返回大于`3`的成员。

# 10 reduce

`reduce` wird verwendet, um alle Elemente eines Arrays auf einen einzelnen Wert zu reduzieren. Es iteriert über das Array und wendet eine Funktion an, die zwei Argumente verwendet: den "Akkumulator" (das Ergebnis der vorherigen Iteration) und das aktuelle Element.

```js
let numbers = [1, 2, 3, 4];
let sum = numbers.reduce(function(acc, num) {
    return acc + num;
}, 0);
console.log(sum); // 10


function reduce(array, combine, start) {
  let current=start;
  for (let i=0; i<array.length; i++)
    current=combine(current, array[i]);
  return current;
};

reduce([1,2,3,4], function(a,b) {
  return a+b;}, 0);
}

reduce(ancestry, function(a,b) {
  if (b.sex=="f") return a+1;
  else return a;}, 0); 
}


ancestry.reduce(function(min, cur) {
  if (cur.born<min.born) return cur;
  else return min;
});

```

acc 的初始值 为0
num 为 numbers 这个array 中 的每一个值 迭代取 


Verwendung: Wenn man einen einzelnen Wert aus einem Array berechnen möchte, wie z. B. die Summe oder das Produkt aller Elemente.



---



`reduce()`方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，`reduce()`是从左到右处理（从第一个成员到最后一个成员）。

语法:`arr.reduce(function(累计值, 当前元素){}, 起始值)`

```js
[1, 2, 3, 4, 5].reduce(function (a, b) {
  console.log(a, b);
  return a + b;
})
// 1 2
// 3 3
// 6 4
// 10 5
//最后结果：15


   // Die Reduktion des Array-Inhalts (hier: 10 und das einzelne Array [5,6,null] !)
       let a = [0, 1, 2, 3, 4, [5, 6, null]];
    a.reduce((p, n) => {return p + n;});  // 105,6,

    
```

上面代码中，`reduce()`方法用来求出数组所有成员的和。`reduce()`的参数是一个函数，数组每个成员都会依次执行这个函数。如果数组有 n 个成员，这个参数函数就会执行 n - 1 次。

- 第一次执行：`a`是数组的第一个成员`1`，`b`是数组的第二个成员`2`。
- 第二次执行：`a`为上一轮的返回值`3`，`b`为第三个成员`3`。
- 第三次执行：`a`为上一轮的返回值`6`，`b`为第四个成员`4`。
- 第四次执行：`a`为上一轮返回值`10`，`b`为第五个成员`5`。至此所有成员遍历完成，整个方法的返回值就是最后一轮的返回值`15`。

`reduce()`方法的第一个参数都是一个函数。该函数接受以下四个参数。

1. 累积变量。第一次执行时，默认为数组的第一个成员；以后每次执行时，都是上一轮的返回值。
2. 当前变量。第一次执行时，默认为数组的第二个成员；以后每次执行时，都是下一个成员。
3. 当前位置。一个整数，表示第二个参数（当前变量）的位置，默认为`1`。
4. 原数组。

这四个参数之中，只有前两个是必须的，后两个则是可选的。

```js
[1, 2, 3, 4, 5].reduce(function (
  a,   // 累积变量，必须
  b,   // 当前变量，必须
  i,   // 当前位置，可选
  arr  // 原数组，可选
) {
  // ... ...
```

如果要对累积变量指定初值，可以把它放在`reduce()`方法的第二个参数。

```js
[1, 2, 3, 4, 5].reduce(function (a, b) {
  return a + b;
}, 10);
// 25
```

上面代码指定参数`a`的初值为10，所以数组从10开始累加，最终结果为25。注意，这时`b`是从数组的第一个成员开始遍历，参数函数会执行5次。

建议总是加上第二个参数，这样比较符合直觉，每个数组成员都会依次执行`reduce()`方法的参数函数。另外，第二个参数可以防止空数组报错。

```js
function add(prev, cur) {
  return prev + cur;
}

[].reduce(add)
// TypeError: Reduce of empty array with no initial value
[].reduce(add, 1)
// 1
```

上面代码中，由于空数组取不到累积变量的初始值，`reduce()`方法会报错。这时，加上第二个参数，就能保证总是会返回一个值。

**总结**

```js
//reduce 返回函数累计处理的结果，经常用于求和等
/*
计值参数：
1. 如果有起始值，则以起始值为准开始累计， 累计值 = 起始值
2. 如果没有起始值， 则累计值以数组的第一个数组元素作为起始值开始累计
3. 后面每次遍历就会用后面的数组元素 累计到 累计值 里面（类似求和里面的 sum ）
*/
```



# 11 some()，every()


这两个方法类似“断言”（assert），返回一个布尔值，表示判断数组成员是否符合某种条件。

它们接受一个函数作为参数，所有数组成员依次执行该函数。该函数接受三个参数：当前成员、当前位置和整个数组，然后返回一个布尔值。

注意，对于空数组，`some`方法返回`false`，`every`方法返回`true`，回调函数都不会执行。

```js
function isEven(x) { return x % 2 === 0 }

[].some(isEven) // false
[].every(isEven) // true
```

`some`和`every`方法还可以接受第二个参数，用来绑定参数函数内部的`this`变量。

## 11.1 some()


some prüft, ob mindestens ein Element im Array eine bestimmte Bedingung erfüllt. Es gibt true zurück, sobald die Bedingung auf mindestens ein Element zutrifft.


```js
let numbers = [1, 2, 3, 4];
let hasEven = numbers.some(function(num) {
    return num % 2 === 0;
});
console.log(hasEven); // true


let hasEven = numbers.some(); //会报错
let hasEven = numbers.sort(); //不会报错, 以为 sort() 有默认的 comparator
```



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


`some`方法是只要一个成员的返回值是`true`，则整个`some`方法的返回值就是`true`，否则返回`false`。

```js
var arr = [1, 2, 3, 4, 5];
arr.some(function (elem, index, arr) {
  return elem >= 3;
});
// true
```

上面代码中，如果数组`arr`有一个成员大于等于3，`some`方法就返回`true`。

## 11.2 every()


`every`方法是所有成员的返回值都是`true`，整个`every`方法才返回`true`，否则返回`false`。

```js
var arr = [1, 2, 3, 4, 5];
arr.every(function (elem, index, arr) {
  return elem >= 3;
});
// false
```

上面代码中，数组`arr`并非所有成员大于等于`3`，所以返回`false`。



every prüft, ob alle Elemente im Array eine bestimmte Bedingung erfüllen. Es gibt true zurück, wenn jedes Element die Bedingung erfüllt, und false, sobald ein Element die Bedingung nicht erfüllt.

```js
let numbers = [2, 4, 6, 7];
let allEven = numbers.every(function(num) {
    return num % 2 === 0;
});
console.log(allEven); // false
```


# 12 find()，findIndex(), findLast()，findLastIndex()

1
数组实例的`find()`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

```js
[1, 4, -5, 10].find((n) => n < 0)
// -5
```

上面代码找出数组中第一个小于 0 的成员。

```js
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

上面代码中，`find()`方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

2 
数组实例的`findIndex()`方法的用法与`find()`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

```js
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```

这两个方法都可以接受第二个参数，用来绑定回调函数的`this`对象。

```js
function f(v){
  return v > this.age;
}
let person = {name: 'John', age: 20};
[10, 12, 26, 15].find(f, person);    // 26
```

上面的代码中，`find()`函数接收了第二个参数`person`对象，回调函数中的`this`对象指向`person`对象。

另外，这两个方法都可以发现`NaN`，弥补了数组的`indexOf()`方法的不足。

```js
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

上面代码中，`indexOf()`方法无法识别数组的`NaN`成员，但是`findIndex()`方法可以借助`Object.is()`方法做到。

`find()`和`findIndex()`都是从数组的0号位，依次向后检查。

3 
[ES2022](https://github.com/tc39/proposal-array-find-from-last) 新增了两个方法`findLast()`和`findLastIndex()`，从数组的最后一个成员开始，依次向前检查，其他都保持不变。

```js
const array = [
  { value: 1 },
  { value: 2 },
  { value: 3 },
  { value: 4 }
];

array.findLast(n => n.value % 2 === 1); // { value: 3 }
array.findLastIndex(n => n.value % 2 === 1); // 2
```

上面示例中，`findLast()`和`findLastIndex()`从数组结尾开始，寻找第一个`value`属性为奇数的成员。结果，该成员是`{ value: 3 }`，位置是2号位。

## 12.1 find


find gibt das erste Element eines Arrays zurück, das eine gegebene Bedingung erfüllt. Wenn kein Element die Bedingung erfüllt, gibt es undefined zurück.

```js
let numbers = [1, 2, 3, 4];
let firstEven = numbers.find(function(num) {
    return num % 2 === 0;
});
console.log(firstEven); // 2
```


## 12.2 findIndex 

findIndex funktioniert ähnlich wie find, gibt jedoch den Index des ersten Elements zurück, das die Bedingung erfüllt. Wenn kein Element die Bedingung erfüllt, gibt es -1 zurück.

```js
let numbers = [1, 2, 3, 4];
let firstEvenIndex = numbers.findIndex(function(num) {
    return num % 2 === 0;
});
console.log(firstEvenIndex); // 1
```


# 13 flat()

Dimension des Arrays auf 1 herabsetzen, alle Werte
```js
let a = [0, 1, 2, 3, 4, [5, 6, null]];
a.flat(Infinity);  // 0,1,2,3,4,5,6,

```
  

# 14 fill()

`arr.fill(value[, start[, end]])`方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
起始索引，默认值为 0。
终止索引，默认值为 this.length。

```js
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

上面代码表明，`fill`方法用于空数组的初始化非常方便。数组中已有的元素，会被全部抹去。

`fill`方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。

```js
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

上面代码表示，`fill`方法从 1 号位开始，向原数组填充 7，到 2 号位之前结束。

注意，如果填充的类型为对象，那么被赋值的是同一个内存地址的对象，而不是深拷贝对象。

```js
let arr = new Array(3).fill({name: "Mike"});
arr[0].name = "Ben";
arr
// [{name: "Ben"}, {name: "Ben"}, {name: "Ben"}]

let arr = new Array(3).fill([]);
arr[0].push(5);
arr
// [[5], [5], [5]]
```

# 15 at()

长久以来，JavaScript 不支持数组的负索引，如果要引用数组的最后一个成员，不能写成`arr[-1]`，只能使用`arr[arr.length - 1]`。

这是因为方括号运算符`[]`在 JavaScript 语言里面，不仅用于数组，还用于对象。对于对象来说，方括号里面就是键名，比如`obj[1]`引用的是键名为字符串`1`的键，同理`obj[-1]`引用的是键名为字符串`-1`的键。由于 JavaScript 的数组是特殊的对象，所以方括号里面的负数无法再有其他语义了，也就是说，不可能添加新语法来支持负索引。

为了解决这个问题，ES2022为数组实例增加了`at()`方法，接受一个整数作为参数，返回对应位置的成员，并支持负索引。这个方法不仅可用于数组，也可用于字符串和类型数组（TypedArray）。

```js
const arr = [5, 12, 8, 130, 44];
arr.at(2) // 8
arr.at(-2) // 130
```

如果参数位置超出了数组范围，`at()`返回`undefined`。

```js
const sentence = 'This is a sample sentence';

sentence.at(0); // 'T'
sentence.at(-1); // 'e'

sentence.at(-100) // undefined
sentence.at(100) // undefined
```

# 16 entries()，keys() 和 values()

ES6 提供三个新的方法——`entries()`，`keys()`和`values()`——用于遍历数组。它们都返回一个遍历器对象，可以用`for...of`循环进行遍历，唯一的区别是`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。

```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```



# 17 查询数组是否包含一个元素 `.includes()`



2 `.indexOf()`
```
let elemIndex = a.indexOf('New element'); console.log(elemIndex);
```
.indexOf() gibt das Index zurück, wenn 'New element' im Array enthalten ist, sonst gibt -1 zurück


1 `.includes()`
```
let included = a.includes('New element');
console.log(included);
```

.includes() gibt true zurück, wenn 'Neues Element' im Array enthalten ist, sonst false, wenn es nicht enthalten ist

表示某个数组是否包含给定的值，返回布尔值
`Array.prototype.includes`方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的`includes`方法类似。ES2016 引入了该方法。

```js
[1, 2, 3].includes(2)     // true
[1, 2, 3].includes(4)     // false
[1, 2, NaN].includes(NaN) // true
```

该方法的第二个参数表示搜索的起始位置，默认为`0`。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为`-4`，但数组长度为`3`），则会重置为从`0`开始。

```js
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```

没有该方法之前，我们通常使用数组的`indexOf`方法，检查是否包含某个值。

```js
if (arr.indexOf(el) !== -1) {
  // ...
}
```

`indexOf`方法有两个缺点，一是不够语义化，它的含义是找到参数值的第一个出现位置，所以要去比较是否不等于`-1`，表达起来不够直观。二是，它内部使用严格相等运算符（`===`）进行判断，这会导致对`NaN`的误判。

```js
[NaN].indexOf(NaN)
// -1
```

`includes`使用的是不一样的判断算法，就没有这个问题。

```js
[NaN].includes(NaN)
// true
```

另外，Map 和 Set 数据结构有一个`has`方法，需要注意与`includes`区分。

- Map 结构的`has`方法，是用来查找键名的，比如`Map.prototype.has(key)`、`WeakMap.prototype.has(key)`、`Reflect.has(target, propertyKey)`。
- Set 结构的`has`方法，是用来查找值的，比如`Set.prototype.has(value)`、`WeakSet.prototype.has(value)`。

# 18 toReversed()，toSorted()，toSpliced()，with()

很多数组的传统方法会改变原数组，比如`push()`、`pop()`、`shift()`、`unshift()`等等。数组只要调用了这些方法，它的值就变了。现在有一个提案，允许对数组进行操作时，不改变原数组，而返回一个原数组的拷贝。

这样的方法一共有四个。

- `Array.prototype.toReversed() -> Array`
- `Array.prototype.toSorted(compareFn) -> Array`
- `Array.prototype.toSpliced(start, deleteCount, ...items) -> Array`
- `Array.prototype.with(index, value) -> Array`

它们分别对应数组的原有方法。

- `toReversed()`对应`reverse()`，用来颠倒数组成员的位置。
- `toSorted()`对应`sort()`，用来对数组成员排序。
- `toSpliced()`对应`splice()`，用来在指定位置，删除指定数量的成员，并插入新成员。
- `with(index, value)`对应`splice(index, 1, value)`，用来将指定位置的成员替换为新的值。

上面是这四个新方法对应的原有方法，含义和用法完全一样，唯一不同的是不会改变原数组，而是返回原数组操作后的拷贝。

下面是示例。

```js
const sequence = [1, 2, 3];
sequence.toReversed() // [3, 2, 1]
sequence // [1, 2, 3]

const outOfOrder = [3, 1, 2];
outOfOrder.toSorted() // [1, 2, 3]
outOfOrder // [3, 1, 2]

const array = [1, 2, 3, 4];
array.toSpliced(1, 2, 5, 6, 7) // [1, 5, 6, 7, 4]
array // [1, 2, 3, 4]

const correctionNeeded = [1, 1, 3];
correctionNeeded.with(1, 2) // [1, 2, 3]
correctionNeeded // [1, 1, 3]
```



# 19 案例


## 19.1 数组中新增元素

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

---

例子

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


## 19.2 删除指定数组元素


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




1.请将` [“关羽”,“张飞”,“马超”,“赵云”,“黄忠”,“刘备”,“姜维”];` 数组里的元素依次打印到控制台

`var arr = ["关羽","张飞","马超","赵云","黄忠","刘备","姜维"]; `

```
// 遍历  从第一个到最后一个
for(var i = 0; i < arr.length; i++ )  { 
   console.log( arr[i] );
} 
```

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

## 19.3 案例: hangman

https://codepen.io/cathydutton/pen/JjpxMm
https://codesandbox.io/s/z9fhk?file=/src/index.js:3525-3536
https://itsourcecode.com/free-projects/jsprojects/hangman-game-javascript-from-scratch-with-source-code/



## 19.4 数组去重

分析：把旧数组里面不重复的元素选取出来放到新数组中，重复的元素只保留一个，放到新数组中去重。

核心算法：我们遍历旧数组，然后拿着旧数组元素去查询新数组，如果该元素在新数组里面没有出现过，我们就添加，否则不添加。

我们怎么知道该元素没有存在？ 利用 新数组.indexOf(数组元素) 如果返回是 -1 就说明 新数组里面没有改元素

```js
// 封装一个去重的函数 unique 独一无二的
function unique(arr) {
    var newArr = [];
    for (var i = 0; i < arr.length; i++) {
        if (newArr.indexOf(arr[i]) === -1) {
            newArr.push(arr[i]);
        }
    }
    return newArr;
}
var demo = unique(['c', 'a', 'z', 'a', 'x', 'a', 'x', 'c', 'b']);
console.log(demo);
```




