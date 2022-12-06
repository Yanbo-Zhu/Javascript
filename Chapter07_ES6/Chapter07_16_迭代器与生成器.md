
# 1 迭代器

迭代器是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署iterator接口（对象里面的一个属性Symbol.iterator），就可以完成遍历操作。es6创建了一种新的遍历命令for…of循环（保存的是键值，for…in保存的是键名 ）

## 1.1 for…of的使用

```js
const xiyou =['ts','swk','zbj','ss']; for(let v of xiyou){ console.log(v); }
```

## 1.2 工作原理

-   创建一个指针对象，指向当前数据结构的起始位置
-   第一次调用对象的next方法，指针自动指向数据结构的第一个成员
-   接下来不断调用next方法，指针一直网后移动，知道指向最后一个成员
-   每调用next方法返回一个包含value和done属性的对象

注：需要自定义遍历数据的时候，要想到迭代器


## 1.3 3、迭代器的应用-自定义遍历数据
```js
//声明一个对象
const banji={
	name="终极一班",
	stus:[
			'xaioming',
			'xiaoning',
			'knight'
	],
	[Symbol.iterator](){
		//索引变量
		let index = 0;
		let _this = this;
		return{
			next:function(){
				if(index<_this.sts.length){
					const result = {value: _this.stus[i],done:false};
					index++;
					return result;
				}else {
					return{value:undefined}
				}
			}
		};
	}
}
//遍历这个对象
for(let v of banji){
	console.log(v);
}

```


# 2 生成器

**生成器函数**是es6提供的一种**异步编程**解决方案，语法行为与传统函数完全不同  
## 2.1 声明与调用  
需要通过next()来调用
![在这里插入图片描述](https://img-blog.csdnimg.cn/e104b4337d1144d9bab948d883cd74a9.png)  
打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2ea5e9b00aad4502a71166f2e2f47e6d.png)  


![在这里插入图片描述](https://img-blog.csdnimg.cn/77a7cec53af944ffab0b19c940383e7f.png)
打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/7568a8acce274a8cb4abf06dd2ef512e.png)

## 2.2 生成器函数的参数  
![在这里插入图片描述](https://img-blog.csdnimg.cn/9fe068e58d1a425c8bfab357ec99fe7d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5ZCE56eNX0RlbW8=,size_20,color_FFFFFF,t_70,g_se,x_16)


## 2.3 生成器函数的实例  
异步编程：文件操作、网络操作（ajax、request）、数据库操作，下面就为异步编程：  


1 1s后控制台输出111,再2s后输出222,再3s后输出333
```js
//直接用计时器就会出现回调地狱
setTimeout(() => {
    console.log(111);
    setTimeout(() => {
        console.log(222);
        setTimeout(() => {
            console.log(333);
        }, 3000)
    }, 2000)
}, 1000)
//用生成器函数就不会出现回调地狱
function one() {
    setTimeout(() => {
        console.log(111);
        iter.next();
    }, 1000)
}

function two() {
    setTimeout(() => {
        console.log(222);
        iter.next();
    }, 2000)
}

function three() {
    setTimeout(() => {
        console.log(333);
        iter.next();
    }, 3000)
}

function* gen() {
    yield one();
    yield two();
    yield three();
}
let iter = gen();
iter.next();

```

2 模拟获取：用户数据、订单数据、商品数据
```js
function getUsers() {
    setTimeout(() => {
        let data = '用户数据';
        iter.next(data);

    }, 1000);
}

function getOrders() {
    setTimeout(() => {
        let data = '订单数据';
        iter.next(data);

    }, 1000);
}

function getGoods() {
    setTimeout(() => {
        let data = '商品数据';
        iter.next(data);

    }, 1000);
}

function* gen() {
        let users = yield getUsers();
        console.log(users);
        let orders = yield getOrders();
        console.log(orders);
        let goods = yield getGoods();
        console.log(goods);
    }
    //调用生成器函数
let iter = gen();
iter.next();

```

