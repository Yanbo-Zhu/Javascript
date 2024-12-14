
- XMLHttpRequest ist ein Objekt zur Kommunikation zwischen Browser und Server mittels HTTP
- Entwickelt von Microsoft, später von Google, Apple und Mozilla übernommen
- Standardisierung durch W3C 
- Eignet sich für den Austausch jeder Art von Daten (trotz seines Namens)


![](image/Pasted%20image%2020241214140133.png)


![](image/Pasted%20image%2020241214140139.png)



![](image/Pasted%20image%2020241214140144.png)



# 1 Verwendung des XMLHttpRequest-Objekts

Synchrone Anfrage
```js
let xhr=new XMLHttpRequest();
xhr.open("GET", "https://dummyjson.com/products", false);
xhr.send();
console.log(JSON.parse(xhr.response));
```



ASynchrone Anfrage
```js
let xhr=new XMLHttpRequest();
xhr.open("GET", "https://dummyjson.com/products", true);
xhr.onreadystatechange=function() {
  if (xhr.readyState==4 && xhr.status==200) {
    console.log(JSON.parse(xhr.response));
  };
};
xhr.send();
```



![](image/Pasted%20image%2020241214141333.png)


# 2 Die neuen Ereignisse load und error 



- Anstelle von readystatechange können Event Handler auch an die Ereignisse load und error gebunden werden
- load wird ausgelöst wenn eine HTTP-Antwort vollständig geladen wird
- error wird bei einem Fehler auf Netzwerkebene ausgelöst, d.h. wenn keine Anfrage gesendet werden konnte oder keine Anfrage kommt


readystatechange
```js
let xhr=new XMLHttpRequest();
xhr.open("GET", "https://dummyjson.com/products", true);
xhr.onreadystatechange=function() {
  if (xhr.readyState==4 && xhr.status==200) {
    console.log(JSON.parse(xhr.response));
  };
};
xhr.send();
```


load und error
```js
let xhr=new XMLHttpRequest();
xhr.open("GET", "https://dummyjson.com/products", true);
xhr.onload=function() {
  console.log(JSON.parse(xhr.response));
};
xhr.onerror=function() {
  console.error("Netzwerkfehler");
};
xhr.send();
```


