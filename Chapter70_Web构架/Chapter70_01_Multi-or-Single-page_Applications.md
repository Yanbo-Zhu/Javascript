

# 1 Multi page Applications

![](image/Pasted%20image%2020241214163444.png)

Webbrowser  -> Webserver (Apache or Nginx) -> Anwendung Server (tomcat or node.js)  -> Datei system Appserver (Html-templates) -> DB Server 

- Webapplikation besteht aus _dynamisch_ erzeugten Webseiten, die beim Aufruf durch den Webserver zusammengestellt werden
- Erzeugung der Webseiten erfolgt durch einen Applikationsserver 
- Daten der dynamischen Webseiten liegen in angeschlossenen Datenbanken
- Erzeugung der Webseiten wird durch vorgefertigte **_HTML-Schablonen_** (**_Templates_**), in welche die Daten durch den Applikationsserver eingefügt werden, vereinfacht
- Vorteil: Webseiten können für den Nutzer maßgeschneidert werden


# 2 Single page Applications (SPAs) 

![](image/Pasted%20image%2020241214164133.png)


Webserver 用的是 Request antworten entgegengenommen 

- Single Page Applications (SPAs) sind Webapplikationen, die aus einer einzigen Webseite bestehen
- JavaScript Engine im Browser lädt bei Nutzerinteraktion oder asynchron im Hintergrund Daten im JSON- oder XML-Format und fügt die Daten in das Document Object Model (DOM) der geladenen Webseite ein
- Präsentationslogik wird komplett im Browser ausgeführt, Applikationsserver macht die Verarbeitung und Lieferung von Daten



# 3 Grundarchitekturen

![](image/Pasted%20image%2020250217200014.png)



# 4 LAMP versus MEAN


![](image/Pasted%20image%2020250217200044.png)

- LAMP: Linux, Apache, MySQL, PHP
- Seit 10 Jahren Standardkonfiguration für Webapplikationen
- Zunehmend veraltet und Anforderungen moderner Webapplikationen nicht mehr gewachsen
- PHP gilt als umständlich und erfordert Integration in Apache
- Apache genügt häufig nicht mehr Leistungsanforderungen
- Viele Übersetzungen: XML to HTML to PHP to SQL
- Frontend arbeitet mit anderen Technologien als Backend
- SQL skaliert nicht gut (und gehört nun zu Oracle ;-)




![](image/Pasted%20image%2020250217200100.png)

- MEAN: MongoDB, Express, AngularJS, NodeJS
- 100% free und Open Source
- Durchgängig JavaScript (Basis für AngularJS und NodeJS/Express)
- Durchgängig JSON als Austauschformat
- MongoDB als dokumentenorientierte Datenbank mit einfacher Übersetzung zu JSON
- Event-basierte, asynchrone Umsetzung von JSON -> sehr schnell und sehr wenig Overhead

