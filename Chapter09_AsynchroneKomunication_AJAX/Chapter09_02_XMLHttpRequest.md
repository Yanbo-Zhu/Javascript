
- XMLHttpRequest ist ein Objekt zur Kommunikation zwischen Browser und Server mittels HTTP
- Entwickelt von Microsoft, später von Google, Apple und Mozilla übernommen
- Standardisierung durch W3C 
- Eignet sich für den Austausch jeder Art von Daten (trotz seines Namens)


![](image/Pasted%20image%2020241214140133.png)


![](image/Pasted%20image%2020241214140139.png)



![](image/Pasted%20image%2020241214140144.png)



# 1 Verwendung des XMLHttpRequest-Objekts


Die Grundidee von Ajax ist es, Daten nachträglich zu laden und in ein bestehende Seite dynamisch einzubauen. Um dies zu realisieren, wird das **XMLHttpRequest-Objekt** benötigt.

Man benötigt drei Schritte, um eine XHR-Anfrage durchzuführen:

**1. Erzeugung des Objekts**

`var xhttp = new XMLHttpRequest();`

**2. Verbindung zum Ziel herstellen**  
Die generelle Syntax lautet: `open("GET/POST", "Zieladresse", true (=asynchrone Anfrage)/ false (=synchrone Anfrage));`

Meist wird hierfür die asynchrone Kommunikation gewählt, damit nicht die gesamte JavaScript-Anwendung stehen bleibt, wenn der Server langsamer arbeitet.
`xhttp.open("GET", "[Ziel]", true);`




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

Das _XMLHttpRequest_-Objekt vermittelt den Status der Abfrage über eine sogenannte Callbacks (Hier ein kurzes Video wie [Callbacks](https://www.youtube.com/watch?v=pTbSfCT42_M) funktionieren). Die Callback-Funktion wird erst aufgerufen, wenn der Server ein Ergebnis geliefert hat. Die Eigenschaft _onreadystatechange_ muss den Namen dieser Funktion beinhalten:

`xhttp.onreadystatechange = ausgabe();`

... oder die anonyme Funktion selbst:

`xhttp.onreadystatechange = function(){ (...) };`




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


# Status der Anfrage abfragen

Dies ist besonders bei asynchronen Anfragen wichtig, damit sichergestellt ist, dass das Ergebnis der Anfrage vorhanden ist und im weiteren Schritt in die Seite integriert werden kann.

Ändert das Objekt seinen Zustand, wird das Ereignis `readystatechange` ausgelöst, sodass die Eigenschaft `readyState` besitzt, die 5 Werte annehmen kann.
- 0 – nicht initialisiert
- 1 – lädt
- 2 – fertig geladen
- 3 – wartend
- 4 – fertig


# **Methoden und Eigenschaften des Objektes**  

Dies sind die Methoden und Eigenschaften, mit denen das Objekt arbeiten bzw. die es annehmen kann.

| Methode                                                                                                     | Erklärung                                                                    |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `abort();`                                                                                                  | bricht die aktuelle Aktion ab                                                |
| `getAllResponseHeaders();`                                                                                  | gibt die Antwort des Servers komplett als Zeichenkette zurück                |
| `send("[Daten]");`                                                                                          | löst einen Request mit den Attributen aus, die in _open_(); angegeben wurden |
| `open("[_POST_/_GET_]", "[_ZielURL_]", "[_asynchron_? (_true_/_false_)]", "[_Username_]", "[_Passwort_]");` | stellt eine Verbindung zur Zielseite über die gewünschte Request-Methode her |
| `setRequestHeader("[_Name_]", "[_Wert_]");`                                                                 | ermöglicht einen zusätzlichen Header in einem HTTP-Request                   |

|Eigenschaft|Erklärung|
|---|---|
|_onreadystatechange_|verfolgt die Änderung des Status eines Objektes|
|_readyState_|gibt den Zustand der Übertragung an|
|_responseText_|String-Version der Antwort des Servers|
|_responseXML_|ermöglicht den Zugriff auf die XML kompatible Serverantwort|
|_status_|zeigt den Status-Code eines HTTP-Requests|
|_statusText_|liefert den Text zum Status-Code|


# Beispiel 


Wir schauen uns die Funktionsweise von Ajax an einem einfachen Beispiel an. In diesem Beispiel gibt es drei "Ressourcen" (in diesem Fall drei JSON-Dateien), die gemäß der Auswahl durch den Nutzer dynamisch nachgeladen werden.

Entpacken Sie diese Dateien in ein Verzeichnis und öffnen Sie die Datei "index.html" mit dem Browser. Je nach Browser (und Betriebssystem) kann es vorkommen, dass das Beispiel aus Sicherheitsgründen nicht funktioniert und Ihr Browser kein Request auf lokale Inhalte zulässt.


1 
Die JSON-Dateien mit dem nachzuladenden Inhalt heißen: game1.json, game2.json und game3.json.

```
Inhalt der Datei game1.json

{
  "title": "Mau Mau",
  "ref": "https://de.wikipedia.org/wiki/Mau-Mau_(Kartenspiel)",
  "description": "Mau-Mau ist ein Kartenspiel für zwei und mehr Spieler..."
}

Inhalt der Datei game2.json

{
  "title": "Mensch ärgere Dich nicht",
  "ref": "https://de.wikipedia.org/wiki/Mensch_%C3%A4rgere_Dich_nicht",
  "description": "Mensch ärgere Dich nicht ist ein Gesellschaftsspiel für ..."
}

Inhalt der Datei game3.json

{
  "title": "Dame",
  "ref": "https://de.wikipedia.org/wiki/Dame_(Spiel)",
  "description": "Dame ist ein strategisches Brettspiel für zwei Spieler..."
}
```

Alle drei json-Dateien enthalten also ein sehr einfaches JSON-Objekt.

2 
Die Datei index.html enthält nur wenig HTML-Sourcecode. Die wichtigen Stellen wurden in der Abbildung hervorgehoben. 

![[Ajax-html-markiert.png]]



3
Ebenfalls in der Datei index.html befinden sich die JavaScript/Ajax-Anweisungen, um die json-Dateien dynamisch nachzuladen. 

```java
"use strict"; // ältere JavaScript-Syntax verbieten

// select-Element zur Spieleauswahl im DOM finden
var gameSelector = document.querySelector("#game-selector select");

// auf Änderungen des select-Elements reagieren
gameSelector.addEventListener("change", function(event) {
  // Referenz auf select-Elements
  var select = this;
  
  // ausgewählten Wert auslesen
  var gameFileName = select.value;

  // Informationen zum Spiel per AJAX laden.
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
       // Inhalt der Daten von JSON in JavaScript-Objekt wandeln
       var gameData = JSON.parse(this.responseText);
       // Anzeige für das Spiel mit geladeden Daten aktualisieren
       updateGamePanel(gameData);
    }
  };
  
  xhttp.open("GET", "./" + gameFileName, true);
  xhttp.send();
});

var updateGamePanel = function(gameData) {
  // Anzeigebereich für Spieleinformationen im DOM finden
  var gamePanel = document.querySelector("#game-panel");

  // Titel setzen
  var title = gamePanel.querySelector(".title");
  title.innerHTML = gameData.title;

  // Quellenangabe setzen
  var ref = gamePanel.querySelector(".ref");
  var label = ref.querySelector(".label");
  ref.href = gameData.ref;
  label.innerHTML = gameData.ref;

  // Beschreibung setzten
  var description = gamePanel.querySelector(".description");
  description.innerHTML = gameData.description;
}
```