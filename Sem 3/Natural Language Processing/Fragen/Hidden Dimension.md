
## Was ist die Hidden Dimension?

Perfekt, genau in die richtige Richtung! Dann legen wir los mit der Mini-Vorlesung zur **hidden dimension im NLP**. Ich erkläre es Schritt für Schritt auf Master-Level, mit Beispielen aus RNNs, LSTMs und Transformers.

---

## 1️⃣ Was ist die Hidden Dimension?

Die **hidden dimension** (oft (d_{hidden}) genannt) ist die Anzahl der **Features**, die das Modell intern für **jeden Token** berechnet und speichert.

- In einem RNN/LSTM:  
    Jeder Token (x_t) wird in einen Vektor der Länge `hidden_size` transformiert, der den **aktuellen Zustand des Modells** repräsentiert.  
    $$ 
    h_t \in \mathbb{R}^{d_{hidden}}  
    $$
- In einem Transformer:  
    Jeder Token bekommt eine **Embedding-Repräsentation** der Länge `d_model`, und `hidden dimension` beschreibt die Breite dieser Repräsentation.
    

💡 **Merke:** Die hidden dimension ist **nicht die Anzahl der Tokens** und auch nicht die Layer-Tiefe, sondern **wie viel “Information” pro Token intern repräsentiert wird**.

---

## 2️⃣ Warum brauchen wir sie?

Die hidden dimension bestimmt, **wie komplexe Muster das Modell lernen kann**:

1. **Mehr Features → mehr Kapazität:**  
    Ein höherer Wert kann subtilere semantische Beziehungen zwischen Wörtern darstellen.  
    Beispiel: In einem LSTM könnte ein Feature repräsentieren „offene Klammern“, ein anderes „Subjekt-Verb-Kongruenz“, wieder ein anderes „Negation im Satz“.
    
2. **Zu wenige Features → Underfitting:**  
    Wenn die hidden dimension zu klein ist, kann das Modell nicht alle notwendigen Muster erfassen.  
    Beispiel: Ein LSTM mit `hidden_size = 5` kann nicht gleichzeitig Syntax, Semantik und Kontext über längere Abstände repräsentieren.
    
3. **Zu viele Features → Overfitting / Rechenkosten:**  
    Große hidden dimensions erhöhen die Modellgröße quadratisch (weil Gewichtsmatrizen (W \in \mathbb{R}^{d_{hidden} \times d_{hidden}}) wachsen) und das Risiko von Overfitting.
    

---

## 3️⃣ Wie man sie liest und interpretiert

- Angenommen, du hast ein LSTM mit `hidden_size = 128` und einen Satz mit 10 Tokens:  
    $$  
    X = [x_1, x_2, ..., x_{10}], \quad h_t \in \mathbb{R}^{128}  $$
    Dann enthält **jeder Token-Vektor 128 Features**, die den Kontext bis zu diesem Token zusammenfassen.
    
- Der **Vektor (h_t)** ist quasi das „Gedächtnis“ des Modells: er speichert **alles Relevante**, was das Modell über die bisher gesehenen Tokens gelernt hat.
    

---

## 4️⃣ Beispiel: Parentheses Counter

Ein klassisches Master-Level-Beispiel:

- Ziel: Modell lernt, wie viele offene Klammern in einem Ausdruck stehen.
    
- Hidden dimension: mindestens 1 reicht, wenn nur die Anzahl der offenen Klammern gespeichert werden soll.
    
- Wenn du aber zusätzlich die **Position des letzten Operators**, die **Tiefe der Verschachtelung**, oder die **Art des nächsten Tokens** speichern willst, brauchst du **mehr Features → größere hidden dimension**.
    

---

## 5️⃣ Zusammenfassung

| Konzept        | Hidden Dimension                                       |
| -------------- | ------------------------------------------------------ |
| Definition     | Anzahl der Features pro Token im Modell                |
| Rolle          | Repräsentation von Kontext und Muster                  |
| RNN / LSTM     | $$(h_t \in \mathbb{R}^{d_{hidden}})$$                  |
| Transformer    | `d_model` entspricht der Hidden Dimension pro Token    |
| Wahl der Größe | Trade-off: Kapazität vs. Rechenaufwand vs. Overfitting |

💡 **Merke:** Die hidden dimension ist quasi der „Arbeitsgedächtnis-Platz“ des Modells für jeden Token.

---

Wenn du willst, kann ich als Nächstes noch **eine kleine Visualisierung** machen, wie ein Satz durch die hidden dimension eines LSTMs fließt, damit das Ganze noch anschaulicher wird.

Willst du, dass ich das mache?