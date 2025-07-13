# Licht 🌈
Licht ist Elektromagnetische Strahlung. Oh Boy
## Licht als Welle 🌊
Strahlungsquellen strahlen fast immer eine Mischung verschiedener Frequenzen aus.

Das von Körpern reflektierte Licht hängt immer von eingestrahltem Licht und von den Absorbationseigenschaften ab

# Das Auge 👀
## Anatomie🧑‍⚕️
- Stäbchen - Schwarz Weiß sehen
- Zäpfchen - Farbsehen
	- #RGB Sehen
- Dämmerungssehen in der Peripherie auf der Netzhaut besser als im Zentrum
- Es gibt nen Blinden Fleck 😶
## Farbwahrnehmung
Wird bestimmt durch die Rezeptoren für rot, grün, blau
Reizung wird im Gehirn weiterverarbeitet und führt zu unterschiedlichen #Wahrnehmungen

Es gibt ,,Ergänzungen" (die können zu Farbillusionen führen)

# Subjektive Farbmerkmale
- Helligkeit
- Farbton #Hue 
	- Begriff zur Unterscheidung verschiedener charakteristischer Farbmuster
- Sättigung #Saturation
	>Maß für den Grad, in dem der Farbton eines gegebenen Lichtes von dem Farbton eines weißen Lichtes gleicher Intensität abweicht. Gesättigte Farbe enthält maximal 2 Grundfarben: Hinzufügen der dritten Farbe bewirkt (zusammen mit den anderen beiden Farben) einen Unbunt-Anteil: schwarz bzw. grau bzw. weiß.
	

## Menschliche Farbempfinden 🎨
Farben werden im #Gehirn🧠  unter Einfluss von Erfahrung/Kultur und unterschiedlichen Namensvorrat in verschiedenen Sprachen verarbeitet.

# Farbmodellierung

## Wahrnehmbare Farben
Unterschiedliches Licht kann gleiche Wahrnehmung hervorrufen
- Mensch kann insgesamt 380.000 #over9000 verschiedene Farben wahrnehmen 
## Farbmischungen
- Additive Farbmischungen (Strahlungsquellen)
- Subtraktive Farbmischungen (Absorbtion, Filter)

## Farbmodelle
Ein Farbmodell muss nicht alle wahrnehmbaren Farben enthalten. 

Die Kombination von Farben soll dem Mischen von Farben entsprechen.
### Allgemeine Farbmodelle
- CIE-Farbraum, CIE-L* a * b
### Hardwarebezogene Farbmodelle
- #RGB
	- Additives Modell
	- oft verwendetes Modell für aktiv licht erzeugende Ausgabemedien
	- Bestimmte Farben im RGB-Modell nicht darstellbar
- CMY(K)
	- Subtraktives Modell
	- oft verwendet bei reflektierenden Ausgabemedien -> z.B. Druckern
	- Das K steht für **blacK**
		Konvertierung #RGB <-> CMY
		![[Pasted image 20250712133652.png]]
- YUV
	- Darstellung von #Luminanz (Lichtstärke pro Fläche) und  #Chrominanz (Farbanteil)
	- Abgeleitet aus #RGB 
- YIQ
### Physiologisch orientierte Farbmodelle
- HLS 
- HSV #⚽
- HSI
	- **Hue**, **Saturation**, **Intensity**
# Erzeugung digitaler Bilder 🖼️
## 1. Räumliche Abtastung
Sensorelemente erhalten Licht aus bestimmten Bereichen gemäß Kamera System
## 2. Zeitliche Abtastung
Sensorelement erhält Licht während einer bestimmten Zeit
- Framerate
- Sequentielle Abtastung
## 3. #Quantisierung
- A/D Wandler
- transformiert Intensitätswerte
- z.B. 8-bit in 16-bit-Werte

- Grauwerte bei schwarz/weiß Kanal
- Farbewerte in Farbkanälen

![[Pasted image 20250712134252.png]]

## Weitere Aufarbeitung 💄
- Verbesserung des Bildes
- Kompressionsalgorithmen
	- Speicherersparnis z.T. mit Kompressionsverlusten 
# Digitale Bilder (1-Kanal-Bilder) ◼️◻️

- Felder von „Pixeln“ („picture elements“), jeweils x-y-Position, „Grauwert“
- Darstellung als Matrix
# Histogramme
Häufigkeiten für #Grauwerte als Abszissen. Maximum bei hohem Weißanteil.

Relative Häufigkeit im Bild z.B. anwendbar für
- #Quantisierung
- Schwellwertverfahren

- Relative Häufigkeit für Zeilen bzw. Spalten
- Position von Bildinhalten
- Ähnlichkeit von Bildern

# Bildqualität

>Bei ungenügender Rastergröße entstehen neue Muster: „Alias“

bestimmt durch
- Wertebereiche der Intensitätswerte
	- z.B. Anzahl der Grauwert Töne
- Rastergröße bzgl. korrekter Wiedergabe
- Nur an bestimmten Stellen wird gemessen
- Die Rastergröße muss ausreichen, um insbesondere kleine Strukturen korrekt wiederzugeben. bzgl. menschlicher Wahrnehmung
- Rasterpunkte kleiner als Unterscheidungsfähigkeit (abhängig von Entfernung des Betrachters)

# Abtasttheorem 
- Abtastrate `A`
- muss größer sein als 2x Frequenz `f`
- `A > 2*f`
- Also -> Pro Wellenlänge mehr als 2 Abtastpunkte
---
- Die Bedingung muss in jede Richtung des Bildes gelten. Wenn bedingung nicht erfüllt passiert 
	- Korrekte Bildinhalte werden nicht übermittelt
	- Es entstehen störende Muster
- Störende Muster könne durch vorherige Tiefpassfilterung verhindert werden

## Aniti-Aliasing

>Auch "Treppenglättung" genannt werden Signalteile oberhalb der Nyquist-Frequenz durch Tiefpass Filterung gedämpft.

# Kameramodelle 📷
**Voraussetzung für scharfe Darstellung:** Jeder Bildpunkt wird wird nur von **einem** Lichtstrahl aus der Umgebung getroffen

Kann erreicht werden durch:
- Lochkamera
- Kollimator _(Bündel von Röhren)_
- Linsensystemen _(Bündelung von Lichtstrahlen)_
## Vorwärtsmodell 

> Projektion Raum -> Bildebene
> 
> Berechnung der Bildobjekte zu den Weltobjekten bei gegebener Kameramatrix

Reduktion der 3D Welt auf 2D Abbildung mit räumlicher Information bzgl.

- Orientierung d. Objekte
- Lichtverhältnisse
- Relative Größe der Objekte
- Beziehung zw. den Objekten
![[Pasted image 20250712160724.png]]
### Extrinsische Parameter
- Pose im Raum
	- Lage des Brennpunktes (3 #DOF)
	- Orientierung (3 #DOF)
		- Kamerakoordinaten X, Y, Z mit Ursprung im Brennpunkt und in Richtung Z optische Achse
### Intrinsische Parameter
- Lage der Bildebene
	- Koordinate auf Z-Achse (1 #DOF)
	- Durchstoßpunkt der optischen Achse (2 #DOF)
		- Bildkoordinaten x,y mit Ursprung auf Z-Achse und Orientierung parallel zu X-Y-Ebene

## Rückwärtsmodelle

> Rekonstruktion des 3D Raumes aus 2D Bild. Ist Teil der Bildinterpretation

1. Als Teil der Bildinterpretation
	1. Berechnung der Weltobjekte zu Bildobjekten bei gegebener Kameramatrix
2. Kamerakalibrierung
	1. Berechnung der Kameramatrix bei gegebenen Weltobjekten und Bildobjekten
3. Selbstlokalisierung
	1. Berechnung der extrinsischen Kameraparameter bei gegebenen Weltobjekten und Bildobjekten und gegebenen intrinsischen Kameraparametern

**Stereo-Sehen:**
- 2 Kamerabilder aus unterschiedlichen Positionen ermöglichen verbesserte Rückrechnung auf die Tiefe im Raum

### weitere Möglichkeiten

- Kombination mit Entfernungsmessung z.B. Laser misst exakte Entfernung liefert aber keine Farbwerte
- Bildfolgen/Bewegung
- Zusatzwissen nutzen (Größe/Umfeld/räumliche Beziehungen)

### Selbstlokalisierung

**Gesucht:** Extrinsische Parameter

- Pose im Raum bzgl. Weltkoordinaten (X,Y,Z)
- Lage des Brennpunktes (3 #DOF)
- Orientierung (3 #DOF )
bekannte intrinsische Parameter

#### Constraints zur Bestimmung

- Objektpunkt mit bekannten Koordinaten und den zugeordnetem Bildpunkt
- durch unterscheidbare Objekt Punkte mit zugehörigen Bildpunkten (z.B. der Winkel in zwei Objekte gesehen werden)
- Winkel zwischen Geraden
- Größenverhältnisse

> Im Grunde Reichen drei Constraints aus um die Pose im Raum zu bestimmen. Bessere Genauigkeit bei mehr Constraints

## Kamerakalibrierung

### bzgl. Projektion

**Ziel:** Verzerrungen ausgleichen

**Methode:** Abbildungsparameter bestimmen mittels zugeordneter vermessener Punkte im Raum und im Bild
![[Pasted image 20250712170127.png]]
### bzgl. Farbe
**Ziel:** Farbkorrekturen

- Optik bedingt: insbesondere am Bildrand
- Sensor bedingt: unterschiedliche Empfindlichkeit

**Methode:** Soll/Ist Zustand vermessen

> Farbkalibrierung wichtig, da Farben oft genutzt werden um Objekte in Bildern zu erkennen (farbcodierte Objekte)

### bzgl. Farbe der Umgebung

- Farbtabelle enthält Zuordnung von Farbwerten zu Farbklassen -> Look-up-table
- Farbklasse komplexerer Ausschnitt des entsprechenden Farbraumes
- Konkreter Bereich abhängig von Reflexion, Schatten, Beleuchtung etc.

# Bildbearbeitung klassisch vs. Deep NN 🤖

## Warum ersetzten Deep NNs alte Methoden?
- lernen Merkmale automatisch statt sie manuell zu definieren
- generalisieren oft besser
- oft robuster gegenüber Rauschen
## Warum klassisch trotzdem sinnvoll
- brauchen weniger Ressourcen
- in Echtzeit in eingebetteten Systemen
- wenn erklärbarkeit/Determinismus wichtig ist
- Verständnis der Prinzipien

# Objekterkennung 🌳

**Problem:**
Objekte erscheinen unterschiedlich
- gedreht
- skaliert
- orientiert
- Größe

# Transformationen

## Arten
### Geometrische Ortsabhängigkeit
- Punktbezogen
- lokale Nachbarschaft
- Global (Fouriertransformation)

### Inhaltliche Ortsabhängigkeit
- Homogen: unabhängig v. Bildkoordinate
- Inhomogen: abhängig von Bildkoordinate
- Linearität: linear/nicht-linear 

## Faltungsoperation

Beschreibung der Transformation durch #Matrix (Kern, Maske)

**Randpixelbehandlung:**
- Unverändert
- Auf ,,konstant" setzten
- Faltungskern anpassen
- Zusätzliche Nachbarn annehmen
- Reflektierte Indizierung (Nachbarn gespiegelt)
- Zyklische Indizierung (Fortsetzung anderer Rand)

### Beispiel: Sobel Filter 
**Nutzung:** Kantenerkennung in Bildern

-1 0 1
-2 0 2
-1 0 1

> Wird als Matrix über die einzelnen Bildpunkte geschoben
> Es existiert Matrix für horizontal und vertikal

### Beispiel: Gaußfilter

Glättung/Deniosining

Mittelwert hat ,,höchste Aussagekraft" -> gewichteter Mittelwert

>Hohe Frequenzen werden eleminiert

## Differenzoperatoren

Hier kommt das ins Spiel, dass die Matritzen auch in x bzw. y Richtung gespiegelt sein können

# Fouriertransformation

## 🧠 Grundidee:

Die **2D-Fouriertransformation** zerlegt ein Bild in **Sinus- und Kosinuswellen unterschiedlicher Frequenzen**.

- **Niedrige Frequenzen** = langsame Helligkeitsänderungen → große Strukturen
- **Hohe Frequenzen** = schnelle Helligkeitswechsel → Kanten, Details, Rauschen

## 📦 Anwendungen in der Bildverarbeitung:

### 1. 🎚 **Filterung (z. B. Tiefpass / Hochpass)**

- **Tiefpassfilter** (Low-pass): Entfernt hohe Frequenzen → Glättet das Bild, reduziert Rauschen
- **Hochpassfilter** (High-pass): Entfernt niedrige Frequenzen → Schärft das Bild, hebt Kanten hervor

🔧 In der Frequenzdomäne ist das oft einfacher als in der Ortsdomäne, weil Filter nur auf bestimmte Frequenzbereiche wirken müssen.

## weitere Anwendungen

- Analyse von Frequenzen
- Bildvergleich durch Vergleich des Spektrums
- Analyse/Vergleich von Texturen

# Hough Transformation 🔁

## 🧠 Grundidee:

> Die Hough-Transformation sucht nach **Formen**, nicht nach Pixeln.

Sie wandelt das Problem um:  
**Statt im Bildraum (x, y) nach Linien zu suchen, sucht man im sogenannten Parameterraum (z. B. für Linien: ρ, θ)**.

## 📏 Beispiel: Linienerkennung

### 1. **Linien im Bildraum** (Ortsdomäne)

Eine **Linie** im 2D-Raum hat in der klassischen Form:

y=mx+by = mx + by=mx+b

→ aber: bei vertikalen Linien wird m=∞m = \inftym=∞, was problematisch ist.

Deshalb verwendet man lieber die **Hough-Form** (Polardarstellung):

ρ=xcos⁡(θ)+ysin⁡(θ)\rho = x \cos(\theta) + y \sin(\theta)ρ=xcos(θ)+ysin(θ)

- ρ\rhoρ: Abstand der Linie vom Ursprung
- θ\thetaθ: Winkel der Normalen zur Linie

### 2. **Idee: Jeder Bildpunkt erzeugt eine Kurve im (ρ, θ)-Raum**

Stell dir einen **Kantenpunkt (x, y)** im Bild vor:  
Er kann zu **vielen Linien gehören**, also zu vielen Kombinationen von ρ\rhoρ und θ\thetaθ.

→ Für jeden solchen Punkt berechnet man:

ρ=xcos⁡(θ)+ysin⁡(θ)\rho = x \cos(\theta) + y \sin(\theta)ρ=xcos(θ)+ysin(θ)

für viele θ\thetaθ-Werte → ergibt eine Sinuskurve im Hough-Raum.

### 3. **Akkumulator: Stimmen zählen im Hough-Raum**

Man erstellt eine **Matrix** (Akkumulator), in der für jedes (ρ, θ) **gezählt wird, wie viele Punkte** auf einer Linie mit diesen Parametern liegen würden.

- Viele Punkte stimmen für die gleiche Linie → großer Wert im Akkumulator
- **Peaks im Akkumulator = Linien im Bild**

# SIFT
**Scale-invariant feature transform**

>Verfahren zur Bestimmung von Merkmalen, unabhängig von #Position, #Rotation, und #Skalierung

### 1. 👋Kandidaten suchen

Extremwerte in einer Laplace-Pyramide bestimmen. Vergleich jedes Punktes mit **26** lokalen Nachbarn in eigener Ebene

### 2. 🗳️Auswahl & lokalisierung Keypoints

Elimination von Kandidaten mit wenig Kontrast oder unklarere Position z.B. Auf einer Kante

Zu jeden Keypoint gehört dann
- seine Skalen Ebene
- seine Position in der Ebene

### 3. 🧭Orientierung der Keypoints bestimmen
### 4. Keypoint Descriptor

### Anwendung

Vergleich von Keypoints eines Templates mit Keypoints eines Bildes

# TTC - Time to Contact 🤯

> Ist die Veränderung der Größe eines Objektes über die Zeit

-> Zeit bis zum Einschlag/Kontakt kann approximiert werden

