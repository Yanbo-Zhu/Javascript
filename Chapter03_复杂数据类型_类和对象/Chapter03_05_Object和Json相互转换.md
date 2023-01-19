
# 1 总览 
JSON: JavaScript Object Notation



# 2 Formatdefinition
JSON kennt also Objekte, Arrays, Zeichenketten, Zahlen, boolsche Werte oder den null-Wert. 

Zum Schluss noch einmal die Fakten zusammengefasst:

-   **Objekte** beginnen mit { und enden mit }
-   Ein Objekt kann eine ungeordnete Liste von Eigenschaften enthalten, die durch Kommata getrennt werden
-   **Eigenschaften** bestehen aus einem Namen und einem Wert
-   **Namen** sind immer Zeichenketten
-   Ein **Wert** kann ein Objekt sein, eine Zeichenkette, ein Array, eine Zahl, boolsche Werte oder der null-Wert
-   **Zeichenketten** beginnen und enden mit Anführungszeichen "
-   **Array** beginnen mit [ und enden mit ], sie können geordnete Wertlisten enthalten, die durch Kommata getrennt werden
-   Boolsche Werte sind true oder false, Anführungszeichen sind nicht nötig
-   **Zahlen** sind die Ziffern von 0-9, negative Zahlen sind möglich, Dezimalpunkte ebenfalls
-   Auch **Leerräume** sind erlaubt


## 2.1 Objekte
Objekte sind ungeordnete Mengen von Name-Wert-Paaren, sie werden wie folgt deklariert:

[![8 7 object.gif](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/3/3f/8_7_object.gif)](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/3/3f/8_7_object.gif)

Ein Objekt kann beliebig viele Name-Wert-Paare enthalten.

## 2.2 Arrays
Arrays sind, wie erwähnt, geordnete Wertlisten. Sie werden von eckigen Klammern eingeschlossen und durch Kommata getrennt:

[![8 7 array.gif](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/a/a8/8_7_array.gif)](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/a/a8/8_7_array.gif)


## 2.3 Werte
Werte können aus diversen Formaten bestehen, Objekte, Arrays, Zeichenketten und weiteren. Die folgende Abbildung zeigt die Formate, die Werte annehmen können in der korrekten Deklaration.

[![8 7 value.gif](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/3/32/8_7_value.gif)](https://vfhwebp.eduloop.de/mediawiki/images/vfhwebp.eduloop.de/3/32/8_7_value.gif)

Eine Verschachtelung der Strukturen (z.B. ist ein Wert, ein Objekt mit einem Array) ist möglich.

## 2.4 Zeichenketten
Zeichenketten können aus keinem (" ") bis mehreren Unicode-Zeichen bestehen. Jede Zeichenkette, egal ob leer oder nicht, wird von doppelten Anführungszeichen umschlossen.

" " (leere Zeichenkette)

"Ich bin eine Zeichenkette." (Zeichenkette mit Inhalt)

Des Weiteren können Zeichenketten noch Escape-Sequenzen mit einem einzelnen weiteren Zeichen sein, die unterschiedliche Bedeutungen haben ("\Escape-Sequenz"). Die wichtigsten sind im folgenden erklärt:

-   \" – ein Anführungszeichen, das ausgegeben werden soll
-   \\ – ein Backslash
-   \/ – ein Slash
-   \b – diese Zeile enthält ein Backspace
-   \n – eine neue Zeile beginnen

## 2.5 Zahlen
Zahlen in JSON sind denen in z.B. Java sehr ähnlich. Hexadezimale Zahlen allerdings, sind hier nicht möglich. Zahlen können folgende Elemente enthalten:
-   die Ziffern 0-9 (1234)
-   ein negatives Vorzeichen (-1234)
-   ein Punkt als Dezimaltrennung (12.34)
-   ein e (oder E) für einen Exponenten, gefolgt von einem + oder – und den Ziffern 0-9 (12e+34)


# 3 Unterschied zu XML
JSON ist ein Datenaustauschformat, XML ist ein Datenauszeichnungsformat.

Dort wo XML auch zum Datenaustausch verwendet wird, sollte immer die Auszeichnungsfähigkeit dieser Sprache wichtig sein. Andererseits ergibt es keinen Sinn, XML zu verwenden, wenn man seine Anforderungen mit einfacheren Schlüssel-/Wert-Paaren technisch abdecken kann, die viel angemessener in JSON repräsentiert werden können.

# 4 普通 object 和 json 转换 

- Objekte in flat data konvertieren zum Senden und Speichern
- key sind "string". 从 fomular 中获得的 nummber , 也会自动在获取的时候, 转为 string 这种 data type 
- values sind einfache Ausdrücke, Funktionen sind hier nicht erlaubt  
- 使用 let json_yzh = JSON.stringify( object_yzh); 的时候, 
    - object_yzh 中 method,  会被自动扔掉 进不到 json_yzh 中去
    - object_yzh 中 property,  会被自动 进json_yzh 中去,  object_yzh 中 property 不是必须满足 key value 一一对应的关系 . 
        - 可以是 firstName : "Susi",
        - 可以 是  hobbies : ["turnen","tanzen","tischlern"],


1 ins JSON konvertieren
JSON.stringify(simplePerson); 

2 aus JSON konvertieren
JSON.parse(personFlat)

## 4.1 例子

```js

{
    "use strict";

    const person = {  // 不但有 property, 还有 method
        firstName : "Susi",
        lastName : "Schmidt",
        hobbies : ["turnen","tanzen","tischlern"],
        birthYear : 2000,
        happy : true,
        age : function(...a){
            let thisYear = new Date().getFullYear();
            return thisYear - person.birthYear;
        }
    };

    const simplePerson = {  // 只有 property 
        firstName : "Susi",
        lastName : "Schmidt",
        happy : true
    };

    console.log(simplePerson);
    // in JSON konvertieren
    let simplePersonFlat = JSON.stringify(simplePerson);   // 没问题, 都转换了, 
    console.log(simplePersonFlat);  // {"firstName":"Susi","lastName":"Schmidt","happy":true}
    
    // aus JSON konvertieren
    console.log(JSON.parse(simplePersonFlat));



    // in JSON konvertieren
    let personFlat = JSON.stringify(person); // property 都转换了, method 被剔除在外了 
      // 
    
    // die function age ist dabei verloren gegangen
    console.log(personFlat);  //   {"firstName":"Susi","lastName":"Schmidt","hobbies":["turnen","tanzen","tischlern"],"birthYear":2000,"happy":true}

    // aus JSON konvertieren
    // age ist immer noch verschwunden
    console.log(JSON.parse(personFlat));

}
```

# 5 convert FormData (HTML5 object) to JSON

https://stackoverflow.com/questions/41431322/how-to-convert-formdata-html5-object-to-json

```js
    formPersonalInfo.addEventListener("formdata", (e) => {
        console.log("formdata fired");
        let data = e.formData;

        let simpleFormularFlat = JSON.stringify(Object.fromEntries(data));   // bringen formData in JSON.
        console.log(simpleFormularFlat); 

        for (let value of data.entries()) {
            console.log(value);
        }
    }, false);
```

1
use forEach on the FormData object
```js
1
var object = {};
formData.forEach(function(value, key){
    object[key] = value;
});
var json = JSON.stringify(object);


2 with ES6 arrow functions:
var object = {};
formData.forEach((value, key) => object[key] = value);
var json = JSON.stringify(object);
```


2 Object.fromEntrie
JSON.stringify(Object.fromEntries(formData));
