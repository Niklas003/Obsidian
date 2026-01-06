## Definition - auf Maschinen übertragen

>Prozesse der **Signalaufnahme und -verarbeitung** zur Erstellung einer Repräsentation der Umwelt. Sie ermöglicht angepasstes Verhalten und Lernen.

## Bewusstsein
Besitz und Empfindung mentaler Zustände z.B. Gedanken
## Qualia

>Unter Qualia versteht man den **subjektiven Erlebnisgehalts eines mentalen Zustandes**

Verständnis von Qualia - zentrales Problem der Philosophie des Geistes.

### #Qualia Problem in der KI
Können Maschinen wirklich fühlen?

## Wahrnehmung beim Menschen

>Wahrnehmung ist ein Prozess zur Erstellung einer **adäquaten Repräsentation** der Umwelt mittels **Selektion, Organisation und Interpretation** sensorischer Eindrücke. Diese Repräsentation stellt die Basis für alle Entscheidungen dar

### Aktive Wahrnehmung
man versucht aktiv etwas in etwas anderem wahrzunehmen und auch damit zu interagieren

**Beispiel:** Ich schaue mir die Geschenke unter dem Weihnachtsbaum nicht nur an, sondern interagiere auch mit diesen

**Merkmale:**
- Bewusst gesteuert
- Aufmerksamkeit ist fokussiert
- Zielorientiert, oft mit Handlung verbunden

### Passive Wahrnehmung
**Definition:** Wahrnehmung, die automatisch und ohne bewusste Steuerung abläuft.
Daten kommen einfach nur herein und man versucht Datenende zu finden

**Merkmale:**
- Unbewusst, zufällig, beiläufig
- Reaktion ohne Absicht oder gezielte Aufmerksamkeit
- Wird oft vom Gehirn „gefiltert“, ohne dass du es aktiv merkst

### Kombination von Informationen

Wahrnehmungen entstehen durch Kombination von
- Informationen aus verschiedenen Sensoren
- parallel empfangener Informationen 
	- z.B. einer Bewegung, eines gesprochenen Satzes
- Wissens

### Hilfsmittel für die Wahrnehmung
### In der Umwelt 
- Orientierungspunkte schaffen
- Verkehrsleitungseinrichtungen
- Markeirungen, Symbole
- Referenzsymbole
### Interne Hilfsmittel
- Karten
- Pläne 
- Routen

## Signale/Reize 🚦

- vermitteln auf Grund ihrer Entstehung Informationen über die Umwelt
- werden über Sensoren bzw. Rezeptoren aufgenommen
- werden verarbeitet
- können mit Kopplung mit Aktuatoren direkte Handlungen auslösen

>Oft interessiert einen das Signal an selbst nicht, sondern die Botschaft die es vermittelt

**Maschinelle Sensoren:** viele
**Menschliche Sensoren:** 5 Sinne

## Wahrnehmungsprozess

**Erstellung eines Weltmodells**

Strukturierung des Prozesses:
- Vertikal
	- Wahrnehmungsprozess über verschiedene Ebenen (Vorverarbeitung, Zwischenresultate, ...)
- Horizontal
	- Integration von Daten aus unterschiedlichen Quellen
	- bzw. von Daten unterschiedlicher Art
- Zeitlich
	- Integration von Daten aus unterschiedlichen Zeitpunkten

### Body Babbling 👄

- Einfach alle Gelenke ansteuern und schauen was passiert
- Dadurch entsteht eine veränderte Wahrnehmung
- **Ergebnis:** sind meist Body Maps -- mentale Repräsentation des Körpers
- Roboter entwickeln Body Maps um mit der Umwelt zu interagieren

>Durch spontane und explorative Bewegungen entsteht Körperschema und motorische Kontrolle

## Affordances

>Interaktionsmöglichkeiten um miteinander zu interagieren.
>Die Möglichkeiten mit seiner Umwelt zu interagieren um Aktionen auszuführen

- Roboter sollen mit ungewohnten Situationen zurecht kommen
- Menschen berauen ein System um mit den Robotern zu interagieren
## Lichtpunktläufer

- Modellierung von menschlichen Bewegungen
- Datensparsam
- Messpunkte an kritischen Stellen am Körper angebracht
## Maschinelle Wahrnehmungsprozesse

- #parallel und #sequentiell
### Parallel
![[Pasted image 20250712113913.png]]

### Sequentiell

Wäre z.B. Hören des Wortes **"Apfel"**
### Waltz Algorithmus 🏠

>Algorithmus zur Erkennung und Beschriftung verschiedener Kantenformen in 3D Objekten und 2D Bildern. Er soll Linienformern finden welche im 3D Raum physikalisch Möglich sind.

![[Pasted image 20250712114837.png]]
#### Vorwärtsmodell
- Charakteristika bekannter Objekte ermitteln

Kantenbeschriftung mit 
- Begrenzungslinien mit `->`
- Konkave Innenlinien mit `+`
- Konvexe Innenlinien mit `-`

#### Rückwärtsmodell
- Charakteristika eines neuen Objektes bestimmen
- Objekt wird mit bereits bekannten Objekten verglichen

#### Beschriftete Schnittpunkte
- insgesamt vier Möglichkeiten `->` `<-`  `+` `-`
- insgesamt 208 Möglichkeiten der Beschriftung
- Davon aber nur 18 pyhs. Möglich

An jedem **Eckpunkt**, wo mehrere Linien zusammenlaufen (meist 3), gibt es nur bestimmte **physikalisch mögliche Kombinationen** von Kantenlabeln.

👉 Waltz hat eine Tabelle erstellt, die zeigt, welche Kombinationen an so einem Punkt erlaubt sind.  
Diese nennt man **"legal junctions"** (z. B. L-Ecke, T-Ecke, Y-Ecke).
### Erwartungen
#### Erwartungsbasiertes Vorgehen
- Einordnung und Identifikation von Informationen
- Ergänzung fehlender Informationen
- Fixierung auf erwartenden Kontext
#### Beschränkung durch Erwartungen
- Man kann nur wahrnehmen was man erkennen kann
- Maschine: 
	- Kreis nur erkennbar mit bestimmten Algorithmus
	- es können nur Elemente erkannt werden die auch "gelernt" wurden
- Mensch:
	- Angeborenes Wissen + Erfahrungen
- Philosophisch Probleme:
	- Was ist überhaupt erkennbar
	- (Sinne + Interpretation, Weltbild)

![[Pasted image 20250712122005.png]]
**Bild:** Man erwartet eigentlich was anderes _(also dass bei den Bohnen z.B. kein Kopf drin ist)_

### Optische Illusion 👀
Bei
- Muster und Linien
- Größe von Objekten
- Farben und Kontrasten
#### Bei Maschinen
Wie beim natürlichen sehen sind Ergänzungen, Auswahlen und Interpretationen notwendig

### Mehrdeutigkeiten
- **Beispiel:** 2D-Abbilder der 3D Realität
![[Pasted image 20250712122443.png]]
#### Auflösen
![[Pasted image 20250712122542.png]]
**Aber:** Bei verrauschten Messungen ist die Positionsbestimmung auch unzuverlässig.
![[Pasted image 20250712122633.png]]

## #Aufmerksamkeit

>Ist der Prozess wo ein agent sich auf ein Feature konzentriert, dabei kommt es zum Ausschluss des restlichen Environments

**Im Grunde:** Selektion von Information
- Durch bewusstes und unbewusstes Wahrnehmen
Aufmerksamkeit bezogen auf Erwartungen
- Unaufmerksamkeit für Unerwartetes
	- siehe Video mit dem Affen
### Passive Aufmerksamkeit
Ein plötzlich auftretenden Event z.B. ein lautes Knallen und es wird mittenmal die Aufmerksamkeit getriggert.
- Cocktail Party Effekt
### Aktive Aufmerksamkeit
Der Agent ist aktiv in einem Prozess in welchem er sich auf ein Feature Konzentriert und dabei die restliche Umwelt ausblendet

### partielle Blindheit bei maschinellem Sehen
- Generell:
	- Nur Formen und Objekte identifizierbar die bekannt sind
	- die "gelernt" wurden

### Change Blindness
Wenn sich etwas langsam ändert, dann erkennt man möglicherweise die Veränderungen eher weniger. Besonders wenn man seine Aufmerksamkeit auf das bestimmte Feature lenkt.

## Sailency Maps

(deutsch: **Auffälligkeitskarten**) sind visuelle Darstellungen, die zeigen, **welche Bildbereiche für ein neuronales Netzwerk besonders wichtig** oder "auffällig" sind – z. B. bei einer Bildklassifikation.

---
### 🧠 Definition:

> Eine **Saliency Map** zeigt an, **welche Pixel oder Bildbereiche den größten Einfluss** auf die Entscheidung eines neuronalen Netzwerks hatten.

Man kann sie sich wie eine **Wärmekarte** über dem Originalbild vorstellen:

- **Helle/rote Bereiche** = hoher Einfluss
- **Dunkle/blaue Bereiche** = geringer Einfluss

## Pop-Out Effekt

![[Pasted image 20250712124729.png]]