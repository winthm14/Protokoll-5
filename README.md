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
  
## Modbus  
Das Modbus-Protokoll wurde 1979 zur Komunizierung mit SPS Geräten entwickelt. In der Automatisierungstechnik wird dieses Protokoll sehr gerne verwendet da es sich um einen offenen Standard handelt, welcher lösungen mit RS-232, RS-485 Busse und TCP/IP-Netzwerke Ermöglicht. Weiters ist Modbus ein zustandsloses Protokoll.  
  
Der Kommunikationsablauf beruht auf einem Server/Client Prinzip. Der Client (zum Beispiel ein PC) sendet einen Request zum Server (zum Beispiel ein Aktor oder Sensor). Dieser antworter mit einer Response.  
<img src="https://www.researchgate.net/profile/Seema_Vora2/publication/317561641/figure/fig3/AS:669285907181576@1536581603644/MODBUS-Transaction-Error-Free.png" alt="">  
  
Bei der eigentlichen Datenübertragung werden drei Varianten unterschieden:  
 * **Modbus ASCII**  
    - Rein Textuelle byteweise Übertragung von Daten. Frames beginnen mit einem Doppelpunkt.  
 * **Modbus RTU**  
    - Binäre byteweise Übertragung von Daten.  
 * **Modbus TCP**  
    - Übertragung der Daten in TCP Paketen
### Modbus-Gateway  
Ein Modbus-Gateway ist in der Lage verschiedene Modbus-Varianten miteinander zu verbinden, also zum Beispiel die Verbindung eines über die UART-Schnittstelle erreichbaren Sensors mit einem über TCP/IP erreichbaren PC.  
Das Modbus Application Layer Protocol definiert dabei als Frame sogenannte **Protocol Data Units (PDU)**. Diese enthalten noch kein Adressierungsschema, da unterschiedliche Varianten (UART, TCP, ...) auch unterschiedliche Adressierungsarten verwenden.  
Die zusätzlichen Spezifikationen für die jeweiligen Varianten definieren dann auch zusätzliche Frame-Felder für die Adressierung und Fehlererkennung, wodurch dann die **Application Data Unit (ADU)** entsteht.  
  
<img src="https://www.researchgate.net/profile/Naixue_Xiong3/publication/281692567/figure/fig2/AS:331936288526339@1456151186841/MODBUS-Protocol-PDU-and-ADU.png" alt="">   
  
### Daten-Modell  
Das Modbus Daten-Modell unterscheidet vier Tabellen (Adressräume) für:  
* **Discrete Inputs**: Einzelnes Bit, kann nur gelesen werden. **Beispiele**: Taster, Endschalter,...  
* **Coils**: Einzelnes Bit, kann geleschen und beschrieben werden. **Beispiele**: LED, Relais,...  
* **Input Registers**: 16-Bit Wert, kann nur gelesen werden. **Beispiele**: Temperatursensor, ADC,...  
* **Hold-Registers**: 16-Bit Wert, kann beschrieben und gelesen werden. **Beispiele**: PWM-Einheit, DAC,...  
  
### Function-Codes
Der Function-Code in einem Modbus-Frame definiert die Bedeutung des Frames.  
Für Requests und Non-Error-Responses sind Werte zwischen 1 und 127 zulässig. Dieser Bereich ist in drei Kategorien unterteilt:  
* **User defined Function Codes (65-72, 100-110)**
  Das sind Werte die individuell verwenden dürfen.
* **Reserved Function Codes**
  8 (19,21-65535), 9, 10, 13, 14, 41, 42, 90, 91, 125, 126, 127
  Das sind Werte die von einigen Unternehmen für Produkte verwendete wurden.
* **Public Function Codes**
  Alle übrigen Werte. Hier definierte Funktionen werden eindeutig von der Modbus.org community festgelegt.  
    
Bei manchen Function-Codes ist zusätzlich ein Subcode definiert, dessen Wert dann im Daten-Bereich der PDU zu finden ist.
Folgende Public Function Codes sind definiert:  
<img src="https://www.picotech.com/images/uploads/library/topics/_med/modbus-function-codes-examples.png" alt="">   
  
### Modbus ASCII  
In der Folgenden Grafik ist nur die Obere Tabelle Relevant, da jeder Modbus Serial Line ASCII Frame den selben aufbau hat. In der Spalte Data werden für einen ASCII Frame 0 bis 2x252 char(s) benötigt.
  
<img src="http://4.bp.blogspot.com/-ANsoUFQoxr4/Vk919TXOV6I/AAAAAAAACs4/FjL86tlqVok/s1600/MODBUS_RTU_ASCII.png" alt="">   
  
Jeder Byte-Wert wird als Hex-Zahl-Text angegeben. Dabei sind nur die Zeichen 0 bis 9 und A bis F erlaubt.  
  
### Unterrichtsbeispiel Modbus ASCII Frame  
Die im Unterricht als Beispiel gebrachte ADU ist die Request um einen Sensor auszlesen.  
```
:010400000001BA<CR><LF>
```  
Die PDU für dieses Beispiel sieht wie folgt aus:  
```  
0400000001  
```  
**Beschreibung des Modbus ASCII Frame's**  
  
:|01|04|0000|0001|BA|<CR><LF>
  
```:``` -> Start Frame  
```01``` -> Adresse des Geräts am Bus  
```04``` -> Read Input Register  
```0000``` -> Inputregister 1 für die Temperatur  
```0001``` -> Anzahl der Gewählten Input Register  
```BA``` -> LRC/Prüfsumme
```<CR><LF>``` -> End-Frame
