

![](image/Pasted%20image%2020241208210724.png)

- Spezifikation von Schnittstellen (Application Programming Interface, API) für den Zugriff auf HTML- (oder XML-) Dokumente
- Implementierung besteht aus einem Satz von Objekten (window, document, ...) zusammen mit deren Methoden und Eigenschaften
- Das DOM wird in einer hierarchischer Baumstruktur mit verschiedenen Knotentypen dargestellt


# 1 什么是DOM
Das Document Object Model ist eine allgemeine Vorgehensweise, um auf Bestandteile eines Dokumentes zugreifen zu können. 
Es bietet eine Schnittstelle für Script- und Programmiersprachen, sodass alle dieselben Funktionen aufrufen können und wurde vom W3C empfohlen.
Programmierschnittstelle für HTML- und XML-Dokumente

DOM (Document Object Model) Manipulation in JavaScript bezieht sich auf das Verändern, Hinzufügen oder Löschen von Elementen und deren Eigenschaften im HTML-Dokument, während es im Browser ausgeführt wird. Durch DOM-Manipulation wird es möglich, die Struktur, den Inhalt und das Styling einer Webseite dynamisch anzupassen.



文档对象模型（Document Object Model，简称 DOM），是 W3C 组织推荐的处理可扩展标记语言（HTML或者XML）的标准编程接口
W3C 已经定义了一系列的 DOM 接口，通过这些 DOM 接口可以改变网页的内容、结构和样式。
![在这里插入图片描述](https://img-blog.csdnimg.cn/fc42557d25be4683881c2f0f231bc778.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)


![](image/Pasted%20image%2020241211171615.png)

DOM 把以下内容都看做是对象
文档：一个页面就是一个文档，DOM中使用doucument来表示
元素：页面中的所有标签都是元素，DOM中使用 element 表示
节点：网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示


Ein HTML-Dokument ist hierarchisch, wie eine Baumstruktur, aus vielen Knoten aufgebaut. 
Der oberste oder Wurzelknoten ist das Dokument selbst, das document.
Mit js kann man auf das DOM zugreifen, es auslesen, Knoten löschen, ändern oder hinzufügen.


# 2 Use Cases des DOM
- Navigation zwischen den einzelnen Knoten
- Erzeugen, Verschieben und Löschen von Knoten
- Auslesen, Ändern und Löschen von Inhalten
- Veränderungen der CSS-Eigenschaften von Elementen
- Definition, Auslösen und Abfangen von Ereignissen (Events)



# 3 Web Rendering

![](image/Pasted%20image%2020241208211020.png)


- _**Web Rendering**_ bezeichnet die Darstellung von HTML- und CSS-Code in einer visuell wahrnehmbaren Form im Webbrowser
- Anhand der HTML-Seite erstellt der Browser das _**Document Object Model**_ (_**DOM**_), eine hierarchische Struktur der Webseite, die alle Elemente, Textkomponenten und Attribute als Knoten enthält
- Anhand der verschiedenen CSSs berechnet der Browser die CSS-Regeln für alle HTML-Elemente und stellt das Ergebnis in einem **CSS Object Model** (**CSSOM**) dar
- Der Render Tree vereint DOM und CSSOM und enthält nur die Elemente, die sichtbar sind und gerendert werden müssen, zusammen mit ihren entsprechenden CSS-Stilen
- Basierend auf dem Render Tree berechnet der Browser das Layout aller sichtbaren Elemente
- Beim _**Layout**_ wird bestimmt, wo im Viewport und in welcher Größe die Elemente erscheinen sollen
- Beim abschließenden _**Paint**_ bildet der Browser die Inhalte (Text, Farben, Bilder,...) in Form von Pixeln visuell im Viewport ab


## 3.1 Die Erstellung des DOM

```JS
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=..." />
    <link href="style.css" rel="stylesheet" />
    <title>Willkommen</title>
  </head>
  <body>
    <p>Hallo <span>Webtechnologien-</span>Studierende</p>
    <div><img src="awesome-photo.jpg" /></div>
  </body>
</html>
```


![](image/Pasted%20image%2020241208211143.png)



## 3.2 Die Erstellung des CSSOM

![](image/Pasted%20image%2020241208211253.png)


## 3.3 Render Tree

![](image/Pasted%20image%2020241208211307.png)



# 4 Schnittstelle zum DOM


![](image/Pasted%20image%2020241208211353.png)


- Das `**document**`-Objekt und von `**event**` abgeleitete Objekte ermöglichen die Interaktion zwischen DOM/CSSOM und JavaScript-Code
- `**document**` bildet eine Schnittstelle zum Lesen und Manipulieren von Knoten im DOM und des CSSOM
- Von `**event**` abgeleitete Objekte ermöglichen das Abonnieren von bestimmten Ereignissen, die auf bestimmten Elementknoten auftreten (z.B. Überfahren mit der Maus, Klicken mit der Maus, Tasteneingabe in ein Formularfeld, ...)
- Hinterlegter JS-Code wird dann beim Auftreten der Ereignisse aufgerufen, um die mit dem Ereignis gelieferten Daten zu verarbeiten
- **Die Manipulation des DOM führt zur sofortigen erneuten Ausführung aller nachfolgenden Rendering-Schritte**


# 5 Einführende Beispiele

Verschiedene Methoden und Eigenschaften für den Zugriff auf die Knoten des DOM-Baumes
Methode getElementById() ermöglicht Zugriff auf HTML-Elemente deren id-Attribut einen bestimmten Wert enthält
Eigenschaft innerHTML ermöglicht das Auslesen oder Ersetzen des Inhalts eines HTML-Elements


![](image/Pasted%20image%2020241208211640.png)

```js
<main>
  <h1>Die DOM Schnittstelle</h1>
  <p id="msg">Der Absatztext</p>
</main>

<script>
  var text = document.getElementById('msg').innerHTML;
  text += ' ' + 'wurde erweitert!';
  document.getElementById('msg').innerHTML = text;
</script>
```


----

![](image/Pasted%20image%2020241208211726.png)

```html
<main>
  <article id="lead">
    <h1>Die DOM Schnittstelle</h1>
    <p>Erster Absatztext im Artikel</p>
    <p>Zweiter Absatztext im Artikel</p>
  </article>
  <p>Erster Absatztext außerhalb des Artikels</p>
  <p>Zweiter Absatztext außerhalb des Artikels</p>
  <p id="result"></p>
</main>

<script>
  var text = '';
  var p_elements = document.getElementsByTagName('p');
  var text =
    'Insgesamt sind ' + p_elements.length + ' p-Elemente im Dokument';
  var article_elements = document.getElementById('lead');
  if (article_elements) {
    var art_p_elements = article_elements.getElementsByTagName('p');
    text +=
      ' und ' + art_p_elements.length + ' im article-Element enthalten!';
  } else {
    text += ' enthalten!';
  }
  text +=
    ' Der zweite Absatz im Artikel lautet: ' +
    art_p_elements[1].innerHTML;
  document.getElementById('result').innerHTML = text;
</script>
```



----


```html
<main>
  <h1 id="headline">Überschrift</h1>
  <p id="mainarticle">Absatztext</p>
  <button onclick="changeContent()">Ändern mit innerHTML</button>
</main>

<script>
  function changeContent() {
  document.getElementById('headline').innerHTML = 'Neue Überschrift!';
  var elem = document.getElementById('mainarticle');
    elem.innerHTML = 'Neuer Inhalt für den Absatztext';
  }
</script>
```


![](image/Pasted%20image%2020241208211750.png)



---



```html
<main>
  <h1>Bild tauschen</h1>
  <p>
    <img id="pic" src="https://tubcloud.tu-berlin.de/s/wraeT3mJ8PApYEX/preview" alt="Bild01" width="200" />
  </p>
  <button onclick="changePicture()">Bild tauschen</button>
</main>

<script>
  var xchange = true;
  function changePicture() {
    var current = document.getElementById('pic');
    if (xchange) {
      current.src = 'https://tubcloud.tu-berlin.de/s/RdYp5mmMeBT6oeH/preview';
      current.alt = 'Bild02';
      xchange = false;
    } else {
      current.src = 'https://tubcloud.tu-berlin.de/s/wraeT3mJ8PApYEX/preview';
      current.alt = 'Bild01';
      xchange = true;
    }
  }
</script>
```

![](image/Pasted%20image%2020241208211826.png)

---


- Änderung der CSS-Eigenschaften von Elementen in JavaScript mit style-Objekt innerhalb von document 
- Objekt enthält Eigenschaften, die denen von CSS entsprechen
- JavaScript erlaubt nicht die Verwendung von Bindestrichen in Eigenschafts- und Variablennamen ("-" wird als Minus interpretiert)
- Camel-Case-Schreibweise für CSS-Eigenschaften in JavaScript
- Beispiele: fontStyle statt font-style und borderTopRightRadius statt border-top-right-radius

```html
<main>
  <h1 id="headline">HTML Style ändern</h1>
  <p id="mainarticle">Ein einfacher Absatztext ...</p>
  <button onclick="changeColor()">Farbe ändern</button>
</main>

<script>
  var element = document.getElementById('mainarticle');
  element.style.color = 'white';
  element.style.background = 'black';

  function changeColor() {
    document.getElementById('headline').style.color = 'gray';
    document.getElementById('headline').style.fontStyle = 'italic';
  }
</script>
```


![](image/Pasted%20image%2020241208211911.png)


