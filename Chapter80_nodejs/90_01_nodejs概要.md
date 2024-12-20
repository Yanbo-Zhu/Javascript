
Seit 2005 entwickelt von Ryan Dahl, 2009 erstmals veröffentlicht auf der jsconf.eu-Konferenz in Berlin

Basiert auf JavaScript und der JavaScript-Laufzeitumgebung V8, ursprünglich entwickelt für Google Chrome Ereignisgesteuerte, ressourcensparende Architektur, die
eine Großzahl gleichzeitig bestehender Netzverbindungen erlaubt. 

Integrierte Module für HTTP-Client- und Serverfunktionalitäten, Zugriff auf das Dateisystem etc. Beliebig erweiterbar durch zahlreiche externe Module

In der Vorlesung als Webserver und als Basis für die Entwicklungsumgebung Vite genutzt

> Node.js ermöglicht das Ausführen von JavaScript außerhalb des Browsers, also auf Servern oder Computern, was die Erstellung von serverseitigen Anwendungen in JavaScript ermöglicht.

# 1 npm (nodejs package manager)



Eingebauter Packet-Manager von node.js

Tool zum Installieren, Aktualisieren und Entfernen von node.js- Paketen

Steuerung mittels Command Line Interface npm Registry ist ein Repository mit mehr als 350.000 Paketen für node.js

![](image/Pasted%20image%2020241030151148.png)



# 2 nodejs 中的implicit type conversion

## 2.1 add operator (a string + a number): 优先number变成string

```
let x = 2;
let y = "3";
let z = "4";
```

When you use the `+` operator with a number (`x = 2`) and a string (`y = "3"`), JavaScript converts the number to a string and performs **string concatenation** rather than addition. So `x + y` becomes `"2" + "3"`, which results in the string `"23"`.



## 2.2 subtraction operation: 优先string变成number

```
let y = "3";
let z = "4";
console.log(z - y);
```

- The `-` operator in JavaScript triggers **implicit type conversion** for both `z` and `y`, treating them as numbers for the subtraction operation.
- So `z - y` becomes `4 - 3`, resulting in `1`.

## 2.3 multiple operator (a string + a number): string变成number


例子1
```
let x = 2;
let y = "3";
console.log(x * y);
```


- The `*` operator in JavaScript automatically tries to convert `y` (a string, `"3"`) to a number when performing multiplication.
- So `x * y` becomes `2 * 3`, resulting in `6`.


例子2
```
let x = 2;
let y = "3";
let z = "4";
console.log(z + y * x);
```

- **Order of Operations**: JavaScript follows the order of operations (PEMDAS/BODMAS), where multiplication (`*`) takes precedence over addition (`+`).
- **Evaluation**:
    - `y * x` is evaluated first, where `y` (a string, `"3"`) is implicitly converted to a number. So, `y * x` becomes `3 * 2`, resulting in `6`.
    - Next, `z + 6` is evaluated. Since `z` is a string (`"4"`), JavaScript implicitly converts `6` to a string and performs string concatenation. So, `z + 6` becomes `"4" + "6"`, resulting in `"46"`.





## 2.4 总结
Zusammenfassung:

![](image/Pasted%20image%2020241030154053.png)

