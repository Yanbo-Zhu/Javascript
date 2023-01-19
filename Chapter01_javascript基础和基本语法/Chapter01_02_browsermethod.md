
# 1 总览 
Es handelt sich um Methoden, die vom Browser zur Verfügung gestellt werden.
Verwenden Sie sie anfangs um Informationen an und vom Anwender zu transportieren.
Die Methoden sind streng genommen kein JavaScript und deshalb werden js-intern auch Fehler oder Warnungen geben. Die Methoden gehören zum Browser und nichts desto trotz können sie gerade am Anfang beim Programmieren üben helfen.

| 方法                     | 说明                            | 归属  |
| ---------------------- | ----------------------------- | --- |
| console.log(msg);      | 浏览器控制台打印输出信息. 用来给程序员看自己运行时的消息 , console.log(allP, typeof allP); 可以一次性输入多个变量| 浏览器 |
| console.clear();|||
| document.write()文档页面输出 |                               |     |
| prompt(info);          | 浏览看弹出输入框，用户可以输入               | 浏览器 |
| alert(msg);            | 浏览器弹出警示框. 主要用来显示消息给用户         | 浏览器 |
| confirm() |                               |     |


- alert()警告框  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/cd5487e3cc4c48a8ae252aa4dbe87ac2.png#pic_center)

- prompt() 输入框  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/4723f1b1f1a6485c8501e6ee2e5bb90d.png#pic_center)

- console.log()控制台输出  
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/818421338119471c89a76d287655c805.png#pic_center)

- document.write()文档页面输出 : 直接在页面输出

## 1.1 例子

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


# 2 Window Object Model (WOM)
die modalen Fenster. Es gibt Funktionen, die mit dem window-Objekt, dem Bezeichner für Browserfenster, erreicht werden können, dem manchmal so genannten Window Object Model (WOM).


## 2.1 Warnungen: window.alert()
Diese Möglichkeit der modalen Fenster haben Sie bereits kennengelernt: mit window.alert() wird ein Fenster angezeigt, mit Text und ggfs. einem Warndreieck. Der Benutzer oder die Benutzerin hat lediglich die Möglichkeit auf "OK" zu klicken. Das ist seine einzige Möglichkeit, um zum Hauptfenster zurückzukehren. Sie deklarieren Warnfenster mit:

window.alert("Warnung");


## 2.2 Bestätigungen: window.confirm() 
Mit einem modalen Bestätigungsfenster hat der Benutzer bereits Interaktionsmöglichkeiten, wenn auch begrenzt. Es gibt standardmäßig eine "OK"-Schaltfläche und eine Schaltfläche zum "Abbrechen" des Vorgangs. Bestätigungsfenster werden mit

window.confirm("Bestätigungstext");

erstellt und aufgerufen. Klickt der Benutzer auf "OK", liefert die Methode true zurück, bei "Abbrechen" false.

## 2.3 Benutzereingaben: window.prompt();

Die dritte Möglichkeit der modalen Fenster wird durch

window.prompt("Fenstertext", "voreingestellter Text");

deklariert und bietet dem Nutzer die Option, neben den Schaltflächen "OK" und "Abbrechen" noch selbst eine Eingabe über ein Textfeld zu tätigen. Diese Funktion wird z.B. bei der Überprüfung von Formulardaten nützlich.

Als Rückgabewert bestimmt die Methode den eingegebenen Text, sofern der Nutzer auf "OK" klickt und eine Eingabe getätigt hat. Wie Sie oben sehen können, besitzt die Methode zwei Parameter. Der Zweite bestimmt den Text, der schon im Textfeld sichtbar ist, er ist allerdings optional.

## 2.4 Drucken: window.print()

Die Funktion window.print() bietet es an, den Druck-Dialog des Browserfensters zu starten, so können Sie dem Benutzer das Drucken der Website erleichtern. Er muss nun nicht mehr über die Kontextmenüs zum Druck-Dialog gelangen.

[![5 4 screenshot druckdialog.jpg](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/d/d5/5_4_screenshot_druckdialog.jpg)](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/d/d5/5_4_screenshot_druckdialog.jpg)


# 3 History-Objekte (back() , forward() , go () )
Die History oder Chronik eines Browser zeigt die Seiten, die der Benutzer in einem bestimmten Zeitabschnitt besucht hat. Mit dem JavaScript-Objekt history können Sie innerhalb dieser Chronik navigieren. Dazu gibt es die Funktionen back(), forward() und go().
-   back() – mit history.back() springen Sie im Verlauf eine Seite nach hinten („zurück“)
-   forward() – mit history.forward() rücken Sie eine Seite nach vorne
-   go() – history.go() ist eine besondere Funktion, da sie noch einen Zahlen-Parameter erwartet der angibt um wie viel zurück (negativer Parameter) oder vorwärts (positiver Parameter) gesprungen werden soll
-   go(0) – mit history.go(0) laden Sie die Seite neu