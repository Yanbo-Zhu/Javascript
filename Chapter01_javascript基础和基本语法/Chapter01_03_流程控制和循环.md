

# 1 流程控制

流程控制主要有三种结构，分别是顺序结构、分支结构和循环结构，这三种结构代表三种代码执行的顺序
JS 语言提供了两种分支结构语句：JS 语句 switch语句

- Mehrere `**if**`/`**else**`-Anweisungen können miteinander verknüpft werden   
- `**switch**`-Anweisung ist oftmals anstelle von langen Ketten von `**if**`/`**else**`-Anweisungen vorzuziehen
- Ein `**case**` ist ein Einsprungpunkt, ab dem mit der Ausführung einer Sequenz von Anweisungen begonnen wird
- Ausdruck hinter `**switch**` wird evaluiert und mit den Werten hinter `**case**` verglichen
- Bei Übereinstimmung wird mit der Ausführung ab der Anweisung hinter `**case**` fortgesetzt bis zum Ende der `**switch**`-Blockes 
- Bei einem `**break**` wird die Ausführung abgebrochen und der `**switch**`-Block verlassen
- Gibt es für keinen `**case**`-Wert eine Übereinstimmung, wird mit den Anweisungen hinter `**default**` fortgesetzt

## 1.1 三元表达式

语法结构 : 表达式1 ? 表达式2 : 表达式3
执行思路

如果表达式1为true，则返回表达式2的值, 
如果表达式1为false，则返回表达式3的值


### 1.1.1 案例：数字补0

用户输入数字，如果数字小于10，则在前面补0，比如01，09，
如果数字大于10，则不需要补，比如20

```js
var figuer = prompt('请输入0~59之间的一个数字');
        var result = figuer < 10 ? '0' + figuer : figue
        alert(result);
```


## 1.2 if 语句



Für den Vergleich existieren zwei Operatoren, == und `===`. Dabei vergleich == den Wert der Operanden und `===` den Wert als auch den Typ der Operanden.

### 1.2.1 if语句
// 条件成立执行代码，否则什么也不做
if (条件表达式) {
    //条件成立执行的代码语句
}


案例：进入网吧
弹出一个输入框，要求用户输入年龄，如果年龄大于等于 18 岁，允许进网吧

```js
var usrAge = prompt('请输入您的年龄:');
if(usrAge >= 18)
{
      alert('您的年龄合法，欢迎来到老子网吧享受学习的乐趣！');
}
```


### 1.2.2 if else 语句
// 条件成立，执行if里面代码，否则执行else里面的代码
if(条件表达式)
{
    //[如果]条件成立执行的代码
}
else
    {
        //[否则]执行的代码
    }

#### 1.2.2.1 案例：判断闰年

接收用户输入的年份，如果是闰年就弹出闰年，否则弹出是平年
算法：能被4整除且不能整除100的为闰年（如2004年就是闰年，1901年不是闰年）或者能够被 400 整除的就是闰年

```js
var year = prompt('请输入年份');

if (year % 4 == 0 && year % 100 !=0 || year % 400 ==0)
{
   alert('这个年份是闰年');
}
else
{
  alert('这个年份是平年');
}
```


### 1.2.3 if else if 语句

```js
if(条件表达式1)
{
  语句1;
}
else if(条件表达式2)
{
   语句2;
}
else if(条件表达式3)
{
  语句3;
}
else
{
   //上述条件都不成立执行此处代码
}
```


### 1.2.4 案例
接收用户输入的分数，根据分数输出对应的等级字母 A、B、C、D、E

其中：

90分(含)以上 ，输出：A

80分(含)~ 90 分(不含)，输出：B

70分(含)~ 80 分(不含)，输出：C

60分(含)~ 70 分(不含)，输出：D

60分(不含) 以下，输出： E

```js
 var score = prompt('请您输入分数:');
        if (score >= 90) {
            alert('宝贝，你是我的骄傲');
        } else if (score >= 80) {
            alert('宝贝，你已经很出色了');
        } else if (score >= 70) {
            alert('你要继续加油喽');
        } else if (score >= 60) {
            alert('孩子，你很危险');
        } else {
            alert('可以再努力点吗，你很棒，但还不够棒');
        }
```




## 1.3 switch
- switch ：开关 转换 ， case ：小例子 选项
- 关键字 switch 后面括号内可以是表达式或值， 通常是一个变量
- 关键字 case , 后跟一个选项的表达式或值，后面跟一个冒号
- switch 表达式的值会与结构中的 case 的值做比较
- 如果存在匹配全等(`===`) ，则与该 case 关联的代码块会被执行，并在遇到 break 时停止，整个 switch 语句代码执行结束
- 如果所有的 case 的值都和表达式的值不匹配，则执行 default 里的代码
- 执行case 里面的语句时，如果没有break，则继续执行下一个case里面的语句

```js

let variable;

switch(variable){

 case 1 : //Anweisungen
 break;
 case 2 : //Anweisungen
 break;
 case 3 : //Anweisungen
 break;
 default : //Anweisungen
}

// 用户在弹出框里面输入一个水果，如果有就弹出该水果的价格， 如果没有该水果就弹出“没有此水果”
var fruit = prompt('请您输入查询的苹果');
switch (fruit) {
    case '苹果':
        alert('苹果的价格为3.5元/千克');
        break;
    case '香蕉':
        alert('香蕉的价格为3元/千克');
        break;
    default:
        alert('没有这种水果');
}
```

```js
switch(prompt("Gib einen HTTP Status Code ein!")) {
  case 200: console.log("OK"); break;
  case 201: console.log("Created"); break;
  case 202: console.log("Accepted"); break; 
  case 203: console.log("Non-Authorative Information"); break;
  case 204: console.log("No Content"); break;
  default: console.log("Unbekannter Status Code"); break;
}


```
# 2 循环
## 2.1 for循环
在程序中，一组被重复执行的语句被称之为循环体，能否继续重复执行，取决于循环的终止条件。由循环体及循环的终止条件组成的语句，被称之为循环语句

```js
for(初始化变量;条件表达式;操作表达式)
{
   //循环体
}

let end=10;

 for(let i=0; i<10; i++){
   //Die Anweisungen hier werden 10x ausgeführt.
 }

```

Initialisierungswert – dieser initialisiert die Zählervariable, sie läuft bei for-Schleifen mit und ist meist diejenige, die in den Befehlen erhöht wird
Bedingung – solange diese erfüllt ist, wird die Schleife ausgeführt
Anweisungen – diese werden ausgeführt, solange bzw. so oft die for-Schleife durchläuft, also solange die Bedingung noch erfüllt ist
Befehle – nach jedem Durchlauf der Schleife werden die Befehle ausgeführt, meist wird der Zähler erhöht. Dies geschieht am Ende, also erst wenn die Schleife einmal durchlaufen wurde.

### 2.1.1 例子
1.输入10句"娘子晚安哈！"

```js
//基本写法
for(var i = 1; i<=10; i++  )
    {
         console.log('娘子晚安哈');
    }
// 用户输入次数
var num = prompt('请输入次数:');
for(var i = 1; i<= num ;i++)
    {
        console.log('娘子晚安哈');
    }
```




2.求1-100之间所有整数的累加和

```js
// 求1-100所以的整数和
var sum = 0;
for (var i = 1; i <= 100; i++) {
    var sum = sum + i;
}
console.log(sum);
```



3.求1-100之间所有数的平均值

```js
 // 3.求1-100之间所有数的平均值
var sum = 0;
for (var i = 1; i <= 100; i++) {
    var sum = sum + i;
}
console.log(sum / 100);
```


## 2.2 ## 双重for循环

循环嵌套是指在一个循环语句中再定义一个循环语句的语法结构，例如在for循环语句中，可以再嵌套一个for 循环，这样的 for 循环语句我们称之为双重for循环。

for(外循环的初始;外循环的条件;外形循环的操作表达式){
    for(内循环的初始;内循环的条件;内循环的操作表达式){
        需执行的代码;
    }
}


内层循环可以看做外层循环的语句
内层循环执行的顺序也要遵循 for 循环的执行顺序
外层循环执行一次，内层循环要执行全部次数

### 2.2.1 例子

打印n行n列的星星
要求用户输入行数和列数，之后在控制台打印出用户输入行数和列数的星星

```js
var star = '';
var row = prompt('请输入行数');
var col = prompt('请输入列数');
for (var j = 1; j <= col; j++) {
    for (var i = 1; i <= row; i++) {
        star += '☆';
    }
    star += '\n';
}
console.log(star);
```



## 2.3 while循环

while(条件表达式){
  //循环体代码
}


执行思路：
- 先执行条件表达式，如果结果为 true，则执行循环体代码；如果为 false，则退出循环，执行后面代码
- 执行循环体代码
- 循环体代码执行完毕后，程序会继续判断执行条件表达式，如条件仍为true，则会继续执行循环体，直到循环条件为 false 时，整个循环过程才会结束

注意：
使用 while 循环时一定要注意，它必须要有退出条件，否则会称为死循环
while 循环和 for 循环的不同之处在于 while 循环可以做较为复杂的条件判断，比如判断用户名和密码


计算 1 ~ 100 之间所有整数的和
```js
var figure = 1;
var sum = 0;
while (figure <= 100) {
    sum += figure;
    figure++;
}
console.log('1-100的整数和为' + sum);
```



## 2.4 do while循环

do {
  //循环体代码-条件表达式为true的时候重复执行循环一代码
}while(条件表达式);


执行思路：
- 先执行一次循环体代码
- 再执行表达式，如果结果为true，则继续执行循环体代码，如果为false，则退出循环，继续执行后面的代码
- 先执行再判断循环体，所以dowhile循环语句至少会执行一次循环体代码


案例：弹出一个提示框， 你爱我吗？ 如果输入我爱你，就提示结束，否则，一直询问**

```js
do {
	var love = prompt('你爱我吗？');
} while (love != '我爱你');
	alert('登录成功');
```


## 2.5 continue 关键字
continue 关键字用于立即跳出本次循环，继续下一次循环（本次循环体中 continue 之后的代码就会少执行一次）。
Während break; Schleifen abbrechen lässt, sorgt continue; dafür, dass die Schleife sofort wieder von vorne beginnt. 
Alle Anweisungen die nach continue; aufgeführt sind, werden dann außer Acht gelassen.

```js
for(Initialisierungswert; Bedingung; Befehl){
    //Anweisung 1
    if(Bedingung){
        continue;
        //Anweisung 3   // 这个不会被执行 了
    }
    //Anweisung 2  // 这个还会被执行 
}
```

例如，吃5个包子，第3个有虫子，就扔掉第3个，继续吃第4个第5个包子
```js
for (var i = 1; i <= 5; i++) {
 if (i == 3) {
     console.log('这个包子有虫子，扔掉');
     continue; // 跳出本次循环，跳出的是第3次循环 
  }
  console.log('我正在吃第' + i + '个包子呢');
}
```



## 2.6 break关键字
break 关键字用于立即跳出整个循环
Zu diesem Zweck gibt es den JavaScript-Befehl break;, der das Verlassen der ganzen Schleife erzwingt. 
Der JS-Interpreter arbeitet anschließend nach der unterbrochenen Anweisung weiter. 
Oft findet man diesen Befehl in einer if-Abfrage, die selbst wieder in einer Schleife steht.

```js
while(Bedingung){
     //Anweisungen
     if(Bedingung){
        //Anweisungen
     }else{
        //Anweisungen
        break; // while schleifer wird unterbrochen 
     }
}
```

例如，吃5个包子，吃到第3个发现里面有半个虫子，其余的也不吃了

```js
for (var i = 1; i <= 5; i++) {
   if (i == 3) {
       break; // 直接退出整个for 循环，跳到整个for下面的语句
   }
   console.log('我正在吃第' + i + '个包子呢');
 }
```



## 2.7 for, forEach(), for ... in 的区别 

什么样的数据类型 适用于那种循环
for         Listen, Arrays
forEach()   Nodelist Arrays
for ... in  Objekt

```js
const allRadios = document.querySelectorAll("[type=radio]");

// for
// 要以 Array/ listen 的方式 去 呼唤 allRadios 中的每个单元
for (let i = 0; i < allRadios.length; i++) {
    if (allRadios[i].checked) {
        mood = allRadios[i].value;
        console.log(allRadios[i]);
        break; // break hier weil nur ein radio true zurück geben kann, anders für checkbox und option, wenn multiple
    }
}

// forEach
// 要以 Nodelist Arrays 的方式 去 呼唤 allRadios 中的每个单元 
// radio 是自己定义的命名的 变量  用于后面的 function 的使用 
allRadios.forEach(radio => {
    if(radio.checked)
        mood = radio.value;
}); 

// for ... in
// üblich für object, hier nur für Syntax
// 要以 Objekt 的方式 去 呼唤 allRadios 中的每个单元 
// radio 是自己定义的命名的 变量  用于后面的 function 的使用 
for(let radio in allRadios){
    if(allRadios[radio].checked)
        mood = allRadios[radio].value;
} 
```

