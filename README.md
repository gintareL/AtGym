#Dokumentation
         
http://mygym.herokuapp.com       
**@Gym** ist eine Webaplikation, die bei der Sportroutine unterstützt. Sie erlaubt dem User seinen persönlichen Trainingsplan zu erstellen, sein Training zu dokumentieren 
und die Trainingserfolge zu errechnen.




##Die ersten Ideen und ihre Realisierung
Um das Design und die Struktur der Webapplikation zu erstellen, wurden am Anfang vom Projekt Mockups entwickelt. Einige sind in der folgenden Tabelle zu sehen. 
Während der Entwicklung mussten ein Paar Änderungen vorgenommen werden, die Hauptidee ist aber erhalten geblieben. 
#
Die Benutzung der Seite ist erst nach der Registrierung möglich. Die Webapplikation wird in zwei Bereiche geteilt: der private Bereich *myGym* und der 
öffentliche Bereich *ourGym*. Im öffentlichen Bereich werden Übungen aufgelistet, die nach Muskelgruppen sortiert sind. Man kann sie auswählen und so 
Fitnesspläne erstellen. Im privaten Bereich werden persönliche Daten vom User gezeigt: Daten über die Person, zusammengestellte Pläne, Routinen und die Entwicklung.
#
Um das Design ansprechend zu halten, werden viele Bilder eingesetzt. Damit die Seite seriös und nicht überladen wirkt, sind als herrschende Farben schwarz, grau, 
weiss und neongrün ausgwählt worden.
#
Mockups | Realisierung
------------ | -------------
![GitHub login](mockups/logIn.jpg) | ![GitHub loginUmsetzung](mockups/loginUmsetzung.jpg)
![GitHub home](mockups/home.jpg) | ![GitHub homeUmsetzung](mockups/homeUmsetzung.jpg)
![GitHub ourgym](mockups/ourgym.jpg) | ![GitHub ourgymUmsetzung](mockups/ourgymUmsetzung.jpg)
![GitHub mygym](mockups/mygym.jpg) | ![GitHub mygymUmsetzung](mockups/mygymUmsetzung.jpg)
![GitHub uebungen](mockups/uebungen.jpg) | ![GitHub uebungenUmsetzung](mockups/uebungenUmsetzung.jpg)          
##Funktionale Anforderungen
Die funktionalen Anforderungen der Webapplikation *@Gym* werden im folgenden Use Cases Diagramm präsentiert:
![GitHub useCases](useCases.png)
Um die Webapplikation zu nutzen, muss der User sich registrieren bzw. anmelden. Nachdem er sich angemeldet hat, kann er Übungen anschauen, sie auswählen und so seine 
Fitnesspläne erstellen. Wenn der User mindestens einen Plan erstellt hat, kann er seine Routine durchführen und die Daten eingeben. Der User kann Bilder hochladen und
persönliche Daten aktualisieren. Wenn die Daten aktualisiert wurden, oder wenn die Routine durchgeführt wurde, kann er die Historie anschauen. Der User kann die Pläne ändern,
indem er Übungen aus dem Plan löscht oder neue Übungen hinzufügt. Er kann aber auch den gesamten Plan löschen. Wenn eine Übung dem User gut gefällt, hat er die Möglichkeit, 
das den Anderen mitzuteilen, indem er die Übung liked.
##Nicht-funktionale Anforderungen
* Ansprechendes und seriöses Design
* Kundenfreundlichkeit
* Sicherheit
* Performanz          
                  
##Architektur
###Model View Controller
Die Webapplikation ist nach dem Schema *Model View Controller* aufgebaut, das auf dem folgenden Bild dargestellt ist. 
![GitHub mvc](mvc.png)                   
View beinhaltet alle HTML Seiten. Im Model befindet sich die Logik und die Datenbank. 
Model und View können nicht direkt miteinander kommunizieren. Die Kommunikation erfolgt über den Controller. Er hat Zugriff sowohl auf das Model, als auch auf die View.
Ein in der View ausgelöstes Event wird sofort dem Controller mitgeteilt. Dann kann der Controller reagieren und die Aktion vom Model holen.       
                  
Die Klassen *Application* und *GymObserver* sind Controllers. Die anderen Klassen gehören zu Model. Zugriff von *Application* auf Model geschieht über die Klasse *Models*.
Die Klassen der Webapplikation werden im folgenden Kapitel ausführlicher erklärt.               
###Klassendiagramm
Wie schon erwähnt wurde, gehören zwei Klassen zum Controller: *Application* und *GymObserver*. Model enthält 23 Klassen. *Models*, *User* und *Uebungen* sind die Wichtigsten. 
Diese Klassen sind im folgenden Klassendiagramm präsentiert.
![GitHub Klassendiagramm](Klassendiagramm.jpg)
*Application* kommuniziert mit Model über die Klasse *Models*. Diese Klasse verwaltet alle anderen Klassen des Models und greift auf die Datenbank zu.                
###Observer und Observable
Um die Websockets zu realisieren, wurden Observer und Observable verwendet. Wie man im Klassendiagramm erkennen kann, ist die Klasse *GymObserver* Observer und *Models* Observable. 
Wenn die Methode *like(int uebung)* in *Models* aufgerufen wird, werden die Observers über den Aufruf der Methode notifyObservers() über die Änderungen informiert. Dadurch können 
die angemeldeten User immer die aktuelle Anzahl von Likes sehen.       
##Datenbank      
Für die Webapplikation wurde eine SQLite Datenbank benutzt. Damit die Datenbank leicht zu pflegen und zu erweitern ist, wurde sie in der 3. Normalform entwickelt. 
Zugriff auf die Datenbank wird über JDBC realisiert. Um die Sicherheit der Webapplikation zu erhöhen, wurden PreparedStatements benutzt.
Passwörter von Usern sind ebenfalls geschützt und werden in der Datenbank verschlüßelt gespeichert. Für die Verschlüsselung wurde der Secure Hash Algorithm benutzt.
![GitHub atGymDB](atGymDB.jpg)                                     
##Technologien
###HTML 5
HTML 5 wird verwendet, um die Grundstruktur der Website aufzubauen. Das bei HTML 5 neu eingeführte Tag 'section' gibt der Website eine Struktur. 
Außerhalb der 'section' befindet sich das Hintergrundbild und die Navigationsleiste, sowie der Footer. Der eigentliche Inhalt der einzelnen HTML-Seiten wird innerhalb der 'section'
abgebildet. Die Navigation befindet sich in dem dafür vorgesehenen Tag 'nav' und der Footer in 'footer'.
Für die Validierung von Inputfelder wird der Typ 'number' verwendet, um sicherzustellen, dass in bestimmten 'input' Tags, wie z.B. in "myRoutine.html" nur Zahlen eingegeben werden.
In den HTML-Seiten für die Übungen, wird mithilfe von 'select' und 'option' eine 'drop-down list' erzeugt, um beim Hinzufügen von Übungen ein Wochentag auswählen zu können.
Ab HTML 5 muss nicht zwingend Flash verwendet werden, sondern kann auf GIF's zurückgreifen, was in diesem Projekt auch umgesetzt wurde.

###CSS3
CSS3 stellt neben Bootstrap das Design der HTML-Seiten dar. Für Elemente, die sich wiederholen, wurden Klassen verwendet. Für einzelne Tags eine ID. Das Design für die Klassen und 
ID's wird in der Datei "style.css" beschrieben.
Alle Größenangaben in CSS werden relativ (in Prozent) angegeben und das Attribut 'float' verwendet, sowie ein Media Query, um ein Responsive Web Design zu ermöglichen. Das Media Query
entfernt ab einer bestimmten Fenstergroesse das Bild auf der Anmeldeseite, so dass nur noch das Login Feld sichtbar ist. In der Menüführung werden Menübilder farbig, wenn man mit der
Maus darüber fährt. Auch das wurde mithilfe von CSS3 realisiert.

###Bootstrap
Bootstrap bietet eine Auswahl an Designelementen. Verwendet werden diese für die Navigationsleiste, Buttons, sowie Icons, wie z.B. der Stift-Icon in "aboutMe.html", um Daten zu 
bearbeiten.
Auch für die ausklappbaren Panels, in denen die Übungen aufgelistet werden, stellt Bootstrap eine Design Klasse zur Verfügung.
Um Bootstrap zu integrieren, muss zunächst die "bootstrap.js" Datei eingebunden werden. In dieser werden alle Bootstrap Komponente mit Javascript realisiert. 
Dadurch genügt es in den HTML-Seiten nur die benötigte Klasse anzugeben. Zusätzlich wurde die Farbe von einzelnen Bootstrap Elementen angepasst, um ein stimmiges Design zu kreieren.

###JavaScript
JavaScript ist ein Skriptsprache, die im Webbrowser interpretiert wird. Sie ist dazu da, um Interaktionen zu erstellen, Validierung festzulegen oder Kommunikation zum Server
aufzubauen.
Im Projekt wurde Javascript z.B. für den Zufallsgenerator der Bilder auf der Home Seite verwendet. Außerdem noch für WebSockets und Ajax.
JavaScript kann sich entweder im Header, in einer ausgelagerten .js Datei oder mitten im HTML Body befinden. In diesem Projekt steht JavaScript im HTML Body. Dafür setzt man 
"script" Tags ein.

###JQuery
JQuery ist eine kleine JavaScript Bibliothek, die unteranderem Funktionen für die DOM Manipulation, Events, Animationen und Ajax zur Verfügung stellt. Dadurch, dass JQuery 
Funktionen kompakt gehalten werden, ist es einfacher sie zu benutzen als JavaScript.
Auf der Website wurden vor allem alle aufklappbaren Chronikanzeigen über die toggle() Funktion realisiert. Vorraussetzung dafür ist das Einbinden der "jquery.js" Datei.

###Ajax
Ajax wird genutzt, um vom Server Inhalte nachzuladen, ohne die Website zu aktualisieren. In diesem Projekt, wird Ajax benutzt, um beim Hinzufügen von Plannamen eine Auswahl
an bereits erestellten Plänen anzuzeigen. Dabei werden nur die Namen angezeigt, die mit den, vom Benutzer bereits eingegebenen, Buchstaben übereinstimmen. Die Auswahlmöglichkeiten
werden unterhalb des Inputfeldes als Buttons angezeigt, was nicht der klassischen Ajax Autovervollständigung entspricht. Dies ist eine schöne Alternative, die dem intuitiven Nutzen
der Website keineswegs schadet.
Im jeweiligen Inputfeld wird die JavaScript Funktion "Ajaxaufruf(eingabe)". Der Übergabewert  'eingbabe' beinhaltet die eingegebenen Buchstaben. Damit startet die Ajax-Anfrage.

###WebSockets
Websockets werden in der Web-Entwicklung für alle Bereiche angewandt, in denen es wichtig ist sofort eine Veränderung zu sehen, ohne den Browser zu aktualisieren. Beispiele dafür 
wären Chats, Kommentare oder wie in diesem Projekt für Likes, die die Benutzer für Übungen vergeben können und diese in Echtzeit bei allen angemeldeten Nutzern inkrementiert werden.

###JSON
JSON steht für JavaScript Object Notation und kann mit XML verglichen werden. Verwendet wird es in Zusammenhang mit WebSockets. Darin ist die jeweilige UebungsID enthalten, deren 
Übung gelikt wird. Diese JSON Datei kann dann an alle Webbrowser verschickt werden, um die Erhöhung der Likes mitzuteilen.

##Schwierigkeiten, Probleme und weitere Ideen
Während der Entwicklung sind einige Schwierigkeiten und Probleme aufgetreten. 
Zu den Schwierigkeiten gehört hauptsächlich die Listenstruktur. Ein User hat z.B. viele Pläne mit vielen Übungen darin, Körpermass-Listen wie z.B. Armunfang und eine Gewichtsliste.
Übungen wiederrum beinhalten ein Enum mit Muskelgruppen. Diese verschachtelte Struktur erforderte viel Konzentration, um nicht den Überblick zu verlieren.
Probleme gibt es auf der Seite "myAnalyse.scala.html". Hier wurde versucht Daten aus der Gewichtsliste herauszulesen und in ein JSON Array einzufügen. Allerdings scheiterte es im
Gegensatz zu dem Gewicht am Auslesen des Datums. Die Werte wurden zwar von der JavaScript Konsole richtig erkannt, aber im JSON Array nicht richtig angezeigt.
Geplant war einen Gewichtsverlauf, sowie alle Körpergrößen in einer Statistik darzustellen, um einen Gesamtüberblick über die Entwicklung des Körpers zu erhalten. Diese Grafiken
sollten dann in einer Slideshow gezeigt werden. Aktuell ist "myAnalyse" so gestaltet, dass beim Nutzer "chris@bale.com" mit dem Passwort "hallo" eine hart codierte Grafik zu sehen ist.
Alle anderen Nutzer bekommen eine Meldung, dass sich die Seite noch in Bearbeitung befindet.
Als weiteres Problem haben sich die for-Schleifen in den Views herausgestellt. Die Übungen werden nach jedem Refresh der Seite in einer anderen Reihenfolge angezeigt, obwohl sie
aus einer sortierten Listen ausgelesen werden.
Weitere Erweiterungen auf der Website können eine Messengerfunktion sein, eigene Pläne mit anderen Nutzern teilen und auch VIP Pläne anzubieten, die die Trainingseinheiten von 
Prominenten enthalten.
