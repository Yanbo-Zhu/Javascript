
javascript, array 的 built-in function 

In JavaScript gibt es eine Reihe von beliebten Higher-Order Functions (HOFs), die auf Arrays und Objekte angewendet werden. Diese Funktionen helfen dabei, das Arbeiten mit Arrays und Objekten auf deklarative und funktionale Weise zu gestalten.

# 1 forEach

Die Methode forEach wird verwendet, um eine gegebene Funktion auf jedes Element eines Arrays anzuwenden. Sie verändert das Array nicht und gibt auch keinen Wert zurück.

```js
let numbers = [1, 2, 3, 4];
numbers.forEach(function(num) {
    console.log(num * 2);
}); // Output: 2, 4, 6, 8
```

Verwendung: Für das Iterieren über ein Array, wenn man eine Aktion für jedes Element ausführen möchte, ohne das Array zu modifizieren.



# 2 map

map erstellt ein neues Array, indem es eine gegebene Funktion auf jedes Element des ursprünglichen Arrays anwendet. Das ursprüngliche Array bleibt unverändert.

```js
let numbers = [1, 2, 3, 4];
let doubled = numbers.map(function(num) {
    return num * 2;
});
console.log(doubled); // [2, 4, 6, 8]
```

Verwendung: Wenn man ein neues Array basierend auf den Werten eines anderen Arrays erzeugen möchte.


# 3 filter 

filter erstellt ein neues Array, indem es eine Funktion auf jedes Element des Arrays anwendet und nur die Elemente zurückgibt, die die Bedingung erfüllen (also für die die Funktion true zurückgibt).

```js
let numbers = [1, 2, 3, 4];
let evenNumbers = numbers.filter(function(num) {
    return num % 2 === 0;
});
console.log(evenNumbers); // [2, 4]
```

Verwendung: Wenn man ein Array nach bestimmten Kriterien filtern möchte.

# 4 reduce

`reduce` wird verwendet, um alle Elemente eines Arrays auf einen einzelnen Wert zu reduzieren. Es iteriert über das Array und wendet eine Funktion an, die zwei Argumente verwendet: den "Akkumulator" (das Ergebnis der vorherigen Iteration) und das aktuelle Element.

```js
let numbers = [1, 2, 3, 4];
let sum = numbers.reduce(function(acc, num) {
    return acc + num;
}, 0);
console.log(sum); // 10
```

acc 的初始值 为0
num 为 numbers 这个array 中 的每一个值 迭代取 


Verwendung: Wenn man einen einzelnen Wert aus einem Array berechnen möchte, wie z. B. die Summe oder das Produkt aller Elemente.


# 5 some 

some prüft, ob mindestens ein Element im Array eine bestimmte Bedingung erfüllt. Es gibt true zurück, sobald die Bedingung auf mindestens ein Element zutrifft.


```js
let numbers = [1, 2, 3, 4];
let hasEven = numbers.some(function(num) {
    return num % 2 === 0;
});
console.log(hasEven); // true


let hasEven = numbers.some(); //会报错
let hasEven = numbers.sort(); //不会报错, 以为 sort() 有默认的 comparator
```

# 6 every

every prüft, ob alle Elemente im Array eine bestimmte Bedingung erfüllen. Es gibt true zurück, wenn jedes Element die Bedingung erfüllt, und false, sobald ein Element die Bedingung nicht erfüllt.

```js
let numbers = [2, 4, 6, 7];
let allEven = numbers.every(function(num) {
    return num % 2 === 0;
});
console.log(allEven); // false
```


# 7 find


find gibt das erste Element eines Arrays zurück, das eine gegebene Bedingung erfüllt. Wenn kein Element die Bedingung erfüllt, gibt es undefined zurück.

```js
let numbers = [1, 2, 3, 4];
let firstEven = numbers.find(function(num) {
    return num % 2 === 0;
});
console.log(firstEven); // 2
```


# 8 findIndex 

findIndex funktioniert ähnlich wie find, gibt jedoch den Index des ersten Elements zurück, das die Bedingung erfüllt. Wenn kein Element die Bedingung erfüllt, gibt es -1 zurück.

```js
let numbers = [1, 2, 3, 4];
let firstEvenIndex = numbers.findIndex(function(num) {
    return num % 2 === 0;
});
console.log(firstEvenIndex); // 1
```


# 9 sort
sort sortiert die Elemente eines Arrays in-place nach einer bestimmten Funktion. Das ursprüngliche Array wird dabei verändert.

```js
let numbers = [4, 2, 3, 1];
numbers.sort(function(a, b) {
    return a - b;
});
console.log(numbers); 
// [1, 2, 3, 4]


let numbers = [4, 2, 3, 1];
numbers.sort(function(a, b) {
    return a > b ? 1 : -1;
});
console.log(numbers); 
// [1, 2, 3, 4]



let hasEven = numbers.some(); //会报错
let hasEven = numbers.sort(); //不会报错, 以为 sort() 有默认的 comparator

```


`a > b ? 1 : -1;` 的解释

```
// Syntax 
(Bedingung) ? (Ausdruck_wenn_true) : (Ausdruck_wenn_false);

```

Der ternäre Operator (auch Conditional Operator genannt) ist ein kompakter Ausdruck in Programmiersprachen wie JavaScript, um einfache Bedingungen auszudrücken.

```js

// Beispiel mit if-else-statement:
let x = prompt("Please enter a number: ");
if (x % 2 == 0) {
console.log(x + " is even.");
} else {
console.log(x + " is odd.");
}



// Das gleiche mit dem ternären Operator
let x = prompt("Please enter a number: ");
console.log(x % 2 == 0 ? x + " is even." : x + " is odd.");

// x = 2; Ausgabe: "2 is even"
// x = 5; Ausgabe: "5 is odd."

```
