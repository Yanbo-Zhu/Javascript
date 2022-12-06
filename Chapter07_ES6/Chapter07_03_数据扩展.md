```js
// 0. Number.EPSILON 是 js表示的最小精度，主要用在浮点数运算两个数的差值小于Number.EPSILON，这认为这两个数相等
console.log(0.1 + 0.2 === 0.3); //返回false
//只有这样来判断：
function equal(a, b) {
    if (Math.abs(a - b) < Number.EPSILON) {
        return true;
    } else {
        return false;
    }
}
console.log(equal(0.1 + 0.2, 0.3)); //这样才返回true

//1. 进制
let b = 0b1010; //二进制
let o = 0o777; //八进制
let d = 100; //十进制
let x = 0xff; //十六进制
console.log(b);
console.log(o);
console.log(d);
console.log(x);

// 2. Number.isFinite 检测一个数值是否为有限数
console.log(Number.isFinite(100));
console.log(Number.isFinite(100 / 0));
console.log(Number.isFinite(Infinity)); //无穷

// 3. Number.isNaN  检测一个数是否为NaN
console.log(Number.isNaN(123));

// 4. Number.parseFloat Number.parseInt 字符串转数
console.log(Number.parseInt('4243fdg23')); //4243
console.log(Number.parseFloat('42.43fdg')); //42.43

// 5. Number.isInteger 判断一个数是否为正数
console.log(Number.isInteger(2.4));

// 6. Math.trunc 将数字的小数部分去掉
console.log(Math.trunc(23.5643654));

// 7. Math.sign 判断一个数到底为正数(是则返回1) 负数(是则返回-1) 还是零(是则返回0)
console.log(Math.sign(100));
console.log(Math.sign(0));
console.log(Math.sign(-100));
————————————————
版权声明：本文为CSDN博主「东篱_Y」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_55935744/article/details/120586664
```