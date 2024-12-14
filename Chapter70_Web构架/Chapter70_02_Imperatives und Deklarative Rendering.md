

# 1 Imperatives Rendering MVC

![](image/Pasted%20image%2020241214164354.png)


- Problem: Komplexität moderner Webanwendungen
- Im Frontend: Präsentation und Darstellung, d.h. Manipulation des DOM in Abhängigkeit von Daten und Erfassung von Daten in Abhängigkeit von externen Quellen (Nutzereingaben, Antworten vom Server,...)
- Das MVC-Pattern ist eine funktionale Aufteilung einer Webanwendung in die Module View, Controller und Model

![](image/Pasted%20image%2020241214164451.png)

- **_Imperatives Rendering_** bezeichnet das explizite Auslesen, Manipulieren, Hinzufügen und Löschen von HTML-Elementen mit JS-Anweisungen
- Auswirkungen von Ereignissen auf den DOM müssen explizit programmiert werden
- Controller ist im MVC-Pattern die Komponente, welche imperatives Rendering durchführt
- Beispiele: JavaScript-Manipulationen auf dem `**document**`-Objekt, jQuery
- Problem: aufwändige Programmierung, da Abhängigkeiten zwischen dem View und dem Model "manuell" abgebildet werden müssen



# 2 Deklaratives Rendering

![](image/Pasted%20image%2020241214164935.png)

- **_Deklaratives Rendering_** definiert Abhängigkeiten zwischen den Elementen und Attributen des DOM und den Daten der Geschäftslogik
- **_Zwei-Wege-Data-Binding_**: Nutzereingaben im View werden automatisch auf die Datenstruktur der Geschäftslogik abgebildet und Änderungen an diesen Daten automatisch in den View übernommen 
- Beispiele: Vue.js, Angular.js und React
- Vorteil: keine explizite und aufwändige Programmierung der DOM-Manipulation, sondern Fokus auf Beschreibung der Abhängigkeiten zwischen DOM und Geschäftslogik
