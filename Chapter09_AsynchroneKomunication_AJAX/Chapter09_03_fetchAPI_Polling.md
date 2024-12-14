
# 1 fetch API 

XMLHttpRequest
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



fetch
```js
fetch("https://dummyjson.com/products")
  .then(response=>{
    if (response.status==200) 
      console.log(response.json())
  })
  .catch(()=>console.log("Netzwerkfehler"));
```


- `fetch` API als moderne Alternative zu `XMLHttpRequest`
- Basiert auf Promises.
    - fetch is Promises funtion 
- `fetch`-Methode wird aufgerufen mit
    - einer URL oder
    - einer URL und einem Objekt, welches HTTP-Methode, headers, body der Anfrage und weitere Parameter spezifiziert oder
    - einem Request-Objekt
- HTTP-Antwort wird dann von der an `**then**` übergebenen Funktion abgefangen und ausgewertet
- Netzwerkfehler werden den an `**catch**` übergebenen Funktion behandelt


---


fetch wit chained promises 

```js
fetch("https://dummyjson.com/products")
  .then(response=>response.json())
  .then(data=>console.log(data))
  .catch(()=>console.log("Netzwerkfehler"));
```


- Mit Chained Promises kann eine HTTP-Antwort in mehreren asynchronen Schritten bearbeitet werden
- Umwandlung der im Body der HTTP-Antwort enthaltenen Daten im JSON-Format mittels der Methode json() auf response (asynchron)
- Hinweis: im Gegensatz zu JSON.parse() arbeitet response.json() asynchron
- Danach Ausgabe des JSON-Objektes

- **`fetch("https://dummyjson.com/products")`**:
    - Sends an HTTP GET request to the provided URL to fetch data from the API.
- **`.then(response => response.json())`**:
    - The `fetch` API returns a `Response` object. Here, `response.json()` extracts the JSON body content from the response.
- **`.then(data => console.log(data))`**:
    - Once the JSON data is parsed, it logs the resulting JavaScript object (`data`) to the console.
- **`.catch(() => console.log("Netzwerkfehler"))`**:
    - Handles any errors that occur during the fetch operation, such as network issues or a failed request.
    - Logs `"Netzwerkfehler"` (German for "network error") to the console in case of an error.


## 1.1 Anpassung von fetch (I/II)

在 fetch 中使用 specific  request message 

- fetch kann mit einem zweiten Argument, neben der URL, angepasst werden
    - Spezifikation der HTTP-Methode
    - Definition von HTTP-Headers (Achtung: nicht alles Headers sind aus Sicherheitsgründen erlaubt)
    - Spezifikation des HTTP-Body
    - Weitere Parameter, siehe fetch API
- Alternativ können fetch-Argumente mit einem Request-Konstruktor spezifiziert werden





fetch
```js
fetch("https://dummyjson.com/products/add", {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({
    title: 'LG 32-Zoll-Monitor'
  })
})
  .then(res=>res.json())
  .then(console.log)
```

Request
```js
let req=new Request("https://dummyjson.com/products/add", {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({
    title: 'LG 32-Zoll-Monitor'
  })
});

fetch(req)
  .then(res=>res.json())
  .then(console.log);
```


# 2 Polling
隔一阵子 就问一下 server 端

```js
setInterval(()=>{
  fetch("https://dummyjson.com/products")
    .then((response)=>response.json())
    .then(console.log)
}, 1000);
```

- Hoher Bedarf an Webanwendungen mit Push-Funktionalität: Chat, Alarme, Collaborative Office-Umgebungen, etc.
- Problem: Server kann keine Verbindungen zum Client aufbauen

![](image/Pasted%20image%2020241214144954.png)


- Wiederholtes Aufrufen der `**send()**`-Methode in regelmäßigen Abständen von **t** ms
- Nach Erhalt jeder Anfrage prüft der Server ob seit der letzten Anfrage eine Datenaktualisierung aufgetreten ist
- Wenn ja, sendet Server die Daten zum Client
- Wenn nein, wird leere Antwort gesendet
- Steuerung durch `**setInterval()**`-Funktion


## 2.1 Long Polling

```
function longPolling() {
  fetch("https://dummyjson.com/products")
    .then((response)=>response.json())
    .then(console.log)
    .then(()=>longPolling())
};

longPolling();
```

![](image/Pasted%20image%2020241214145154.png)

- Problem von Polling: Tradeoff zwischen dem Aufwand für den Austausch von HTTP-Anfragen und Antworten und der zeitnahen Zustellung von Datenaktualisierungen
- Reduzierung der Aufwands durch Vergrößerung des Anfrageintervalls führt zu verzögerter Zustellung von Daten
- Geringe Verzögerung führt zu häufigen Anfrage/Antwort-Zyklen


Long Polling
- Serverseitige Implementierung des Timeouts
- ==Server beantwortet eine HTTP-Anfrage nicht bis eine Datenaktualisierung oder ein Timeout eintritt==
    - server 收到 http-Anfrage, 在time out 时间内, 如果没有 Datenaktualisierung, 则一直不发出 reponse 给 server. 等到 time out 发生 , 在发送 http response 
    - 在time out 时间内, 如果有 Datenaktualisierung, 则不等到 time out 发生 , 就马上发送  http response 给 clisent 
- Bei Datenaktualisierung wird Antwort mit aktualisierten Daten gesendet
- Nach Eintreffen der Antwort initiiert der Client sofort eine neue HTTP-Anfrage
    - Client收到 任何 http repsonse 就马上在发送一个新的 http anfrage 
- Client und Server verfügen über eine quasi permanent andauernde Verbindung


















