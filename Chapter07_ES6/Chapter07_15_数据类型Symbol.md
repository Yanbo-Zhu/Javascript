
es6引入了一种新的原始的数据类型Symbol，表示独一无二的值，是js中的第七种数据类型，类似于字符串数据类型

# 1 特点

Symbol的值是惟一的，用来解决命名冲突的问题
Symbol值不能与其他数据类型进行运算
Symbol定义的对象不能使用for…in循环遍历，但可以使用Reflect.ownKeys来获取对象的所有键名

# 2 基本使用

//创建Symbol
let s=Symbol();
console.log(s,typeof s);//返回s的值以及类型
let s2 = Symbol('sgg');
let s3 = Symbol('sgg');
console.log(s2===s3);//返回false
//Symbol.for创建
let s4 = Symbol.for('sgg');
let s5 = Symbol.for('sgg');
console.log(s4===s5);//返回true


# 3 js数据类型总结
USONB

U：undefined
S:string、symbol
O：object
N:null、number
B：boolean

# 4 对象添加symbol类型的属性

向对象中添加方法
![在这里插入图片描述](https://img-blog.csdnimg.cn/2f0ba9aab52645bfaa910ef637a0209b.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/9f245a7dfb57449eb95b2a645ab65066.png)

# 5 内置属性
除了定义自己使用的Symbol值以外，es6还提供了11个内置的Symbol值，指向语言内部使用的方法

|x|x|
|---|--|
|Symbol.haslnstance	|当其他对象使用instanceof运算符，判断是否为该对象的实例时，会调用这个方法|
|Symbol.isConcatSpreadable	|对象的Symbol.isConcatSpreadable属性等于的是一个布尔值，表示该对象用于Array.prototype.concat()时，是否可以展开|
|Symbol.unscopables|	该对象指定了使用with关键字时，哪些属性会被with环境排除|
|Symbol.match|	当执行str.match(myObject)时，如果该属性存在，会调用它，返回该方法的返回值|
|Symbol.replace	|当该对象被str.replace(myObject)方法调用时，会返回该方法的返回值|
|Symbol.search	|当该对象被str.search(myObject)方法调用时，会返回该方法的返回值|
|Symbol.split|	当该对象被str.split(myObject)方法调用时，会返回该方法的返回值|
|Symbol.iterator|	对象进行for…of循环时，会调用Symbol.iterator方法，返回该对象的默认遍历器|
|Symbol.toPrimitive	|该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值|
|Symbol.toStringTag	|在该对象上面调用toString方法时，返回该方法的返回值|
|Symbol.species|	创建衍生对象时，会使用该属性|
