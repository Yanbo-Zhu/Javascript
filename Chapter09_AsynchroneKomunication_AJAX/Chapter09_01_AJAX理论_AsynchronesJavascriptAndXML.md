
- AJAX (Asynchrones Javascript and XML) für die asynchrone Datenübertragung zwischen Browser und Server
- Dies ist allerdings recht ungewöhnlich, da Ajax nicht zwangsläufig asynchron sein muss und XML darin meist gar nicht eingesetzt wird. Lediglich das J für JavaScript passt.
- Durchführung von HTTP-Anfragen während der Anzeige einer HTML-Seite und Veränderung dieser Seite im Hintergrund, d.h. ohne Nutzerinteraktion


Durch Ajax ist es möglich, Seiteninhalte vom Webserver nachzuladen, ohne dass hierzu ein Reload der Webseite notwendig ist. Heutzutage ist dies "normal", aber im Jahr 2005 war es ein nahezu revolutionäres Konzept, bestehend aus: 
- Begriff bezeichnet nicht eine einzelne, sondern eine Gruppe von Technologien
    - HTML： dient der Browserdarstellung
    - DOM： wird verwendet, um HTML-Dokumente zu strukturieren und zu verändern.
    - JavaScript： steuert die Interaktivität bzw. das Verhalten der Seite.
    - XMLHttpRequest-Object: API, um Daten auf asynchroner Basis mit dem Webbrowser austauschen zu können
	    - wird im Hintergrund der Webseite zum Abrufen von weiteren "dynamischen" Daten verwendet
    - XML oder JSON als Datenaustauschformate

Mit Hilfe des **XMLHttpRequest**-Objekts kann JavaScript eine (XHR-)Anfrage an einen Server senden und die Daten aus der Antwort dynamisch in die Seite einbauen. Diese Anfragen werden oft durch Benutzerinteraktion auf der Webseite ausgelöst, wie z.B. im oben genannten Beispiel mit Google-Suggest durch die Eingabe einiger Buchstaben in das Suchfeld. Hier wird durch die Eingabe des Suchbegriffs eine solche XHR-Anfrage gesendet und der Server liefert die Liste mit Suchvorschlägen, die dynamisch in die Seite eingefügt wird.



![](image/Pasted%20image%2020241214140014.png)

# **Vorteile und Nachteile von Ajax**  

Die großen Vorteile von Ajax sind die **verbesserte Usability' _und_** _höhere Interaktvität_,' ohne die komplette Seite neu laden zu müssen und die sich daraus ergebende **geringere Ladezeit** sowie die **verminderte Serverauslastung**, da nur Teile der Webanwendung aktualisiert werden.

Es gibt aber auch kleinere Nachteile:
- **Lesezeichen-Problem**: Ajax gibt oft keine vollständigen „Seiten“ zurück, sondern nur einzelne Teile. Diese Teile können Sie mit Ihrem Browser natürlich nicht als Bookmark setzen, sodass Sie beim Aufrufen immer die ursprüngliche Seite aufrufen. Dies ist ärgerlich, vor allem dann, wenn Sie schon mehrere Eingaben getätigt haben. Vermeiden können Sie dies, indem Sie die Textmarke _„location.hash“_ verwenden, die dem Attribut den Seitenstatus hinzufügt.
- **Navigations-Problem**: Ähnlich wie bei den Lesezeichen haben Sie auch beim Vor- und Zurück-Button das Problem, dass Sie die aktuellen Eingaben bei der Navigation verlieren. Sie gelangen immer wieder auf die Startseite, denn der Browser speichert nur statische Seiten in seiner History. Er speichert also keine Anfragen über das _XMLHttpRequest_-Objekt, denn die Attribut ändert sich dabei meist nicht.

