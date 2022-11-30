
# 1 Zugriff auf die DOM Elemente

Einzelne Elemente (object):
- getElementById()
- getElementByQuerySelector()

Listen von Elementen:
- getElementsByTagName()
- getElementsByClassName()
- getElementsByName()
- getElementsByQuerySelectorAll()

HTML Collections
- collection

# 2 Einzelne Elemente (object)

## 2.1 Die id finden Sie im HTML-Dokument
```js
const inc = document.getElementById("include");
console.log(inc);
console.log(typeof inc);
console.log(inc.id);
console.log(inc.innerHTML);
console.log(inc.childNodes);
```


## 2.2 Für den QuerySelector 
kann man jeden gültigen CSS-Selektor einsetzen.
```js
const code = document.querySelector("article:first-of-type code");
console.log(code, typeof code);
// ginge auch einfacher, hier nur "code" :-)
```

    

# 3 Listen von Elementen
```js
 const h2 = document.getElementsByTagName("h2");
    console.log(h2);
    const heading = document.getElementsByClassName("heading");
    console.log(heading[0].innerHTML);
    const allP = document.querySelectorAll("p");
    console.log(allP);
    const allRadio = document.getElementsByName("comprehension");
    console.log(allRadio);
    for(let i=0; i<allRadio.length; i++){
        console.log(allRadio[i].checked);
    }
```
   

# 4 HTML Collections
```js
    const form = document.forms[0];
    console.log(form);
```
