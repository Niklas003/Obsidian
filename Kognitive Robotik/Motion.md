> Veränderung der Position durch verschiedene Aktionen/Skills

# Locomotion 🚂

> Bewegung im Raum.. Man kann sich also von seinem Ort weg bewegen deshalb ***Loco***motion

# Degrees of Freedom #DOF 

> Ein **Freiheitsgrad** ist eine **unabhängige Bewegungsmöglichkeit**, die ein System (z. B. ein Roboter) hat.

## 📦 Beispiele zur Veranschaulichung:

### 🔹 1. Ein Punkt in der Ebene (2D):

Ein Punkt kann sich in der Ebene bewegen:

- nach **links/rechts** (x-Achse)
- nach **oben/unten** (y-Achse)

➡️ **2 DOFs**

---

### 🔹 2. Ein starres Objekt in der Ebene (z. B. ein Roboterarm-Endeffektor in 2D):

Es kann:

- sich auf x-Achse verschieben ✅
- sich auf y-Achse verschieben ✅
- sich um die z-Achse (senkrecht zur Ebene) **drehen** ✅

➡️ **3 DOFs in 2D**

---

### 🔹 3. Ein Objekt im Raum (3D):

Ein Körper im Raum kann:

- sich entlang **x, y, z** bewegen (Translation) ✅✅✅
- sich um **x, y, z** rotieren (Rotation) ✅✅✅

➡️ **6 DOFs in 3D**

---

## 🦾 Bei Robotern:

Ein Roboterarm hat so viele DOFs, wie **unabhängige Gelenkbewegungen** möglich sind.

- Jedes **Rotationsgelenk**: 1 DOF (Drehung um eine Achse)
- Jedes **Schiebegelenk (prismatisch)**: 1 DOF (Verschiebung entlang einer Achse)

Ein Roboter mit:

- 3 Rotationsgelenken → 3 DOFs
- 6 Gelenken → 6 DOFs
- usw.

Aber: Nicht alle DOFs sind für die Positionierung des **Endeffektors** notwendig – sie können auch für Flexibilität und Redundanz sorgen.

# Serieller Roboter 🤖

> Ein serieller Roboter Rn ist eine kinematische Kette mit (n + 1) Systemen Σ0,...,Σn und n Gelenken G1,...,Gn, wobei Gi die Systeme Σ(i−1) und Σi verbindet. Jedes der Gelenke Gi ist entweder ein Dreh- oder ein Schubgelenk. Das System Σ0 bzw. Σn heißt Basis bzw. Endeffektor des seriellen Roboters

# Kinematik

>Die Kinematik beschreibt den mechanischen Aufbau des Roboters, d.h. die räumliche Zuordnung der Bewegungsachsen nach Folge und Aufbau. Sie beschäftigt sich mit der Geometrie und den zeitabhängigen Aspekten der Bewegung.

## Vorwärtskinematik

Lineares Problem mit **genau einer Lösung**

**Gesucht:** Pose/Position des Endeffektors Σn

> vom #Konfigurationsraum in den #Arbeitsraum

### Kurzgesagt 🦆

Setzte die Pose aus der Konfiguration. Die Konfiguration beschreibt diese Pose **eindeutig**

## Inverse Kinematik

Problem mit mehreren Lösungen oder **gar keinen Lösung**

**Gesucht:** eine Konfiguration für eine bestimmte Pose

> vom #Konfigurationsraum in den #Arbeitsraum 

### Kurzgesagt 🦆

Finde eine Konfiguration für die gewünschte Pose.