
# 1 variadische Funktionen und die Methode apply()

Wenn man einer Funktion eine vorab unbekannte Anzahl von Methoden geben möchte, nutzt man variadische Funktionen mit dem Objekt arguments. Beispiel:

```js
var dojo = ["Stephen Kam", "Jackie Brand", "Rolf Chan", "Lee Yuen Chow"];

function welcomeDojo () {

 var args = Array.prototype.slice.call(arguments);

 var lastItem = args.pop();
 console.log("Willkommen " + args.join (", ") + ", und " + lastItem + ".");

}

welcomeDojo.apply(null, dojo);
```

Bequemer geht es indes so, mit der Ellipse ...:
```js
function foo(...a) {
   return a[0] + a[2];
}
```


Das ergibt z.B. beim Aufruf foo(47,1,1) den Wert 48. Probieren Sie den Aufruf mit nur 2 Argumenten, z. B. foo(47,1), und dann mit drei Argumenten, z. B. foo(47,1,1,'bar'), und bewundern das Ergebnis.

# 2 Fetch-API

Die Fetch-API ist der Nachfolger zu AJAX und dient dem asynchronen Nachladen von Webseitenelementen, auch Code. Eine Anwendung, die fetchdata.txt nachlädt:

[...]
fetch('./fetchdata.txt')
.then(response => response.json())
.then(data => {
console.log(data) // Druckt Ergebnis von `response.json()` in
getRequest
})
.catch(error => console.error(error))
[...]

then ist ein alternativer Weg, ein Promise asynchron einzulösen (zu evaluieren) und fortzufahren, sobald das Ergebnis geliefert wird. Mit catch() wird im Fehlerfall verzweigt. Bald mehr dazu im Kapitel zu AJAX.

# 3 Threads in Javascript: Web Worker

Web Worker dienen dem nebenläufigen Ausführen von Javascript-Code. Anders als AJAX sollen sie i.d.R. keine Seiteneffekte haben und nur optional einen Rückgabewert geben. Web Worker sind flexibler als Event-basierte Aufrufe, die zwar asynchron, aber nicht zwingend Multi-threaded, ablaufen.

Je ein Web Worker wird in einem Thread ausgeführt. Es gibt Dedicated und Shared Worker. Im Folgenden sollen Dedicated Worker betrachtet werden. [https://www.w3.org/TR/workers/#examples](https://www.w3.org/TR/workers/#examples) gibt ein Beispiel zum Auffinden von Primzahlen. Hier wird ein nebenläufiger Thread gestartet, es dürfen generell mehrere sein:

```html 
<!DOCTYPE HTML>
<html>
 <head>
  <title>Worker example: One-core computation</title>
 </head>
 <body>
  <p>The highest prime number discovered so far is: <output id="result"></output></p>
  <script>
   var worker = new Worker('worker.js');
   worker.onmessage = function (event) {
     document.getElementById('result').textContent = event.data;
   };
  </script>
 </body>
</html>
```

worker.js:
```js
var n = 1;
search: while (true) {
  n += 1;
  for (var i = 2; i <= Math.sqrt(n); i += 1)
    if (n % i == 0)
     continue search;
  // found a prime!
  postMessage(n);
}
```

Mit onmessage() werden die mit postMessage() verschickten Nachrichten entgegengenommen. Mit worker.terminate() kann der Erzeuger den Thread abbrechen. Die Web-Anwendung berechnet im Thread die Primzahlen die dann an den Erzeuger gesendet und dort in der Webseite angezeigt werden.