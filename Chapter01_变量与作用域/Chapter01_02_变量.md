https://blog.csdn.net/Augenstern_QXL/article/details/119249534


# 1 变量

变量是用于存放数据的容器，我们通过变量名获取数据，甚至数据可以修改
本质：变量是程序在内存中申请的一块用来存放数据的空间

## 1.1 变量的命名规范 Namingkonvention 

Groß- und Kleinschreibung wird unterschieden
ein Variablenname besteht nur aus Buchstaben, Ziffern oder dem Unterstrich, keine Leerzeichen
das erste Zeichen darf keine Ziffer sein
JavaScript-Schlüsselworte dürfen keine Variablennamen sein

1. 由字母(A-Za-z)、数字(0-9)、下划线(_)、美元符号( $ )组成
   1. 如：usrAge, num01, _name
2. 严格区分大小写
   1. var app; 和 var App; 是两个变量
3. 不能 以数字开头
   1. 18age 是错误的
4. 不能 是关键字、保留字
   1. 例如：var、for、while
5. 变量名必须有意义，做到 见其名，知其意
   1. MMD 、BBD、 nl → age
6. 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。 myFirstName

## 1.2 标识符、关键字、保留字

（1）标识符
标识(zhi)符：就是指开发人员为变量、属性、函数、参数取的名字。
标识符不能是关键字或保留字。

（2）关键字
关键字：是指 JS本身已经使用了的字，不能再用它们充当变量名、方法名。
包括：break、case、catch、continue、default、delete、do、else、finally、for、function、if、in、instanceof、new、return、switch、this、throw、try、typeof、var、void、while、with 等。

（3）保留字
保留字：实际上就是预留的“关键字”，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。
包括：boolean、byte、char、class、const、debugger、double、enum、export、extends、fimal、float、goto、implements、import、int、interface、long、mative、package、private、protected、public、short、static、super、synchronized、throws、transient、volatile 等。


## 1.3 变量初始化

1. var是一个JS关键字，用来声明变量(variable变量的意思)。使用该关键字声明变量后，计算机会自动为变量分配内存空间。
2. age 是程序员定义的变量名，我们要通过变量名来访问内存中分配的空间

```js
//声明变量同时赋值为18
var age = 18; 
//同时声明多个变量时，只需要写一个 var， 多个变量名之间使用英文逗号隔开。

var age = 18, address ='火影村',salary = 15000;
```

```js
<script>
        // 变量的使用：
        // 1.声明变量  声明了一个age 的变量
        var age; //age 为变量名
        //2.赋值 把值存入这个变量中
        age = 20;
        // 3.在控制台输出结果
        console.log(age); 

        alert(userName);
        // 4.变量的初始化 （常用）
        // 声明一个变量并赋值，称之为变量的初始化
        var onename = '血灵';//尽量不用name作为变量名，因为name在一些浏览器中是有关键字
        console.log(onename);
</script>
```

## 1.4 变量的声明,赋值

- let - blockscope
- const - blockscope
- var - functionscope

同时声明多个变量时，只需要写一个 var， 多个变量名之间使用英文逗号隔开。

```js
var age = 10, name = 'zs', sex = 2;
var oneName = '白夜',
    address = '地球',
              age = 500;
```

声明变量特殊情况

| 情况                         | 说明           | 结果        |
| -------------------------- | ------------ | --------- |
| var age; console.log(age); | 只声明，不赋值      | undefined |
| console.log(age)           | 不声明 不赋值 直接使用 | 报错        |
| age = 10;console.log(age); | 不声明 只赋值      | 10        |

```js
// 1只声明不赋值 输出undefined 因为程序也不知道里面存的是啥  未定义的
var sex;
console.log(sex);
// 2不声明 不赋值 直接使用会报错
// console.log(tel);  //需注释掉，否则下行无法执行，因为js是逐行解释，解释一句，执行一句....
// 3不声明 直接赋值使用
//不提倡如此使用
qq = 123232;
console.log(qq);
```

