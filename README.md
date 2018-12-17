# Protokoll 5 <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/HTL_Kaindorf_Logo.svg/300px-HTL_Kaindorf_Logo.svg.png" alt="">  
  
Professor: SX  
Übungsort: Kaindorf   
Übungsdatum: 11.12.2018  
Anwesend: Vollmaier Alois, Vezonik Sarah, Wegl Patrick, Wesonig Mercedes, Winter Matthias, Winter Thomas

## Makefile  
Zur Ergänzung der letzten Einheit wurden in dieser Einheit noch das "-"(Minus) und das "@"(At-Zeichen) als Operanten erklärt. Das Minus vor einer Anweisung bewirkt, dass, auch wenn ein Fehler auftritt, die Anweisung immer ausgeführt wird. Das "@"-Zeichen bewirkt, dass die Anweisung nicht am Bildschirm angezeigt wird. Folgendes Beispiel wird also immer ausgeführt jedoch nicht auf dem Bildschirm angezeigt:  
```- @rm```  
Weiters wurde Erklärt, dass man ein Komentar mit einem Kanalgitter(#) beginnt:  
```# Das ist ein Komentar```  
Das Dollarzeichen ```$``` kennzeichnet in makefiles Variablen:  
```$(variable1)```  


## Schnitstellen  
  
### USB (Universal Serial Bus) 
Die USB-Schnittstelle ist sehr gut geeignet um vom PC aus mit dem Arduino zu komunizieren, da auf der Platine bereits ein UART auf USB Konverter integriert ist.  
  
### RS-232 Schnitstelle (RS = Recommended Standard, EIA-232, EIA = Electronic Industries Alliance)  
Diese Schnitstelle Existiert seit 1960, ist eine Punkt zu Punkt Schnitstelle und arbeitet mit Differenzspannungssignalen zwischen +15V und -15V. Ansonsten sehen die Signale sehr ähnlich aus wie bei einem UART-Signal. Dank der höheren Spannungspegeln der Signale ist es möglich über sehr große Distanzen Signale zu übertragen. Nachteile dieser Schnitstelle sind die hohe Rechenleistung welche zum Datentransfer benötigt wird und das System ist nicht Bus fähig.  
  
### RS-485 Schnitstelle  
Trotz geringerer Spannungspegel als bei einer RS-232 Schnitstelle wirt mit der RS-485 Schnitstelle, hinsichtlich der Fehlerrate, ein besseres Ergebnis erzielt. Diese Technologie ermöglicht es Buslängen von bis zu 1200m mit einer Übertragungsgeschwindigkeit von bis zu 90kBit/s zu errichten. Ermöglicht wird dies mit zwei Leitungen A(nicht invertiertes Signal) und B(invertiertes Signal) zum Datentransfer bei lediglich -6V bis +6V.  
Diese Schnitstelle ermöglicht es erstmals einen Datenbus (oder RS-485 Bus) mit bis zu 32 Komunikationsteilnehmer zu Errichten.  
  
### Ethernet (TCP/IP)/ Echtzeit(Industrial) Ethernet
Eine weitere und bis jetzt auch leistungsstärkste Schnitstelle ist die Ethernet Schnitstell mit dem TCP/IP Protokoll. Da dies jedoch nicht Echtzeitfähig ist, gibt es von diversen Herstellern modifizierte Ethernet lösungen für die Industri. Eine lösung entwickelte B&R Automation mit Powerlink. Powerlink wird heute von der offenen Anwender- und Anbietergruppe EPSG (Ethernet Powerlink Standardization Group) als offener Standard weiterentwickelt und spezifiziert.

### Feldbus  
Ein Feldbus ist ein Bussystem welches in der Automatisierungstechnik Feldgeräte wie Sensoren und Aktoren mit einer Steuereinheit verbinden. Diese Methode ersetzt die bis dahin verwendete parallele Verdrahtung da diese viel teurer hinsichtlich materialverbrauch(Kabel) und finanzieller Mittel war.
Für Feldbus gib es **verschiedene Standards** für die einzelnen Automatisierungsbereiche:  
  * **Industrie**  
        - Profibus, Powerlink, Interbus-5  
  * **Automobiel**  
        - LIN, CAN, Flexray, (Mosi)
  * **Gebäudetechnik**  
        - KNX, Homematic, LON, CAN, Modbus
  * **Industrie 4.0**  
        - (Webdienst, http-Protokoll, Rest-Server)  
  
## ModBus  
