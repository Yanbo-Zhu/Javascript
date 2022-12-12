# 1 注释

1 单行注释 :  // xxx
快捷键ctrl + /

2 多行注释
快捷键 shift + alt + a

```
/*
    多行注释
*/    
```

# 2 Browsermethoden/输入输出语句
Es handelt sich um Methoden, die vom Browser zur Verfügung gestellt werden.
Verwenden Sie sie anfangs um Informationen an und vom Anwender zu transportieren.

| 方法                     | 说明                            | 归属  |
| ---------------------- | ----------------------------- | --- |
| alert(msg);            | 浏览器弹出警示框. 主要用来显示消息给用户         | 浏览器 |
| console.log(msg);      | 浏览器控制台打印输出信息. 用来给程序员看自己运行时的消息 | 浏览器 |
|console.clear();|||
| prompt(info);          | 浏览看弹出输入框，用户可以输入               | 浏览器 |
| document.write()文档页面输出 |                               |     |

- alert()警告框  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/cd5487e3cc4c48a8ae252aa4dbe87ac2.png#pic_center)

- prompt() 输入框  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/4723f1b1f1a6485c8501e6ee2e5bb90d.png#pic_center)

- console.log()控制台输出  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/818421338119471c89a76d287655c805.png#pic_center)

- document.write()文档页面输出 : 直接在页面输出

## 2.1 例子

```js
    <script>
        // 1.弹出警示框  输出的 展示给用户的
        alert('秀儿同学,请你坐下！');
        // 2.输入框
        prompt('请输入密码:','1234');
        prompt('请输入你的名字:');
        // 3.控制台输出 控制台可见
        console.log('看到了吗,码农兄弟?');
        //4.文档页面输出
        document.write('666');
    </script>
```
