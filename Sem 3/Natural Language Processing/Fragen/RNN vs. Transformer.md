
## Jetzt zum Unterschied RNN und Transformer ein RNN arbeitet ja sequentiell ein Transformer parrallell ich wie kann der denn Parallel arbeiten? 

## 1️⃣ RNNs: sequentiell

- Jedes Token wird **nacheinander** verarbeitet.
    
- Hidden State $h_t$ hängt vom vorherigen $h_{t-1}$ ab:  
    $$ 
    h_t = f(x_t, h_{t-1})  
    $$
- Vorteil: natürliche Modellierung von zeitlicher Abhängigkeit.
- Nachteil: **keine Parallelisierung möglich**, da $h_t$ erst berechnet werden kann, wenn $h_{t-1}$ fertig ist → Training langsam.
    

---

## 2️⃣ Transformer: parallel

- Transformer nutzt **Attention statt sequentieller Hidden States**.
    
- Jeder Token sieht **alle anderen Tokens gleichzeitig**, und die Berechnung hängt **nicht sequentiell** von vorherigen Tokens ab.
    

### Schlüsselidee: Self-Attention

1. Jedes Token $(x_i)$ wird auf **Query, Key, Value** projiziert:  $$ 
    Q = X W_Q, \quad K = X W_K, \quad V = X W_V  
    $$
    
    - (X) = Input-Embeddings der Länge $(d_{model})$
    - Alle Tokens $X = [x_1, x_2, ..., x_n]$
    - werden gleichzeitig verarbeitet → **Matrixmultiplikation**
2. Attention Scores:  $$  
    \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) V  
    $$
    - Hier siehst du: keine sequentielle Abhängigkeit.
    - **Alle Token-Interaktionen** werden **parallel** berechnet.
3. Ergebnis: **kontextualisierte Hidden States** für alle Tokens gleichzeitig.
    

---

## 3️⃣ Warum das schneller geht

- In RNN: $(h_1 → h_2 → h_3 → ... → h_n)$ → **O(n) sequentiell**
    
- In Transformer: Matrixmultiplikation über alle Tokens → **alles gleichzeitig** → GPU-optimiert, stark parallelisierbar
    

💡 **Merke:** Transformer ersetzt die „Gedächtnisketten“ der RNNs durch **parallele Aufmerksamkeit auf alle Tokens**, daher kann alles gleichzeitig berechnet werden.


## Ok wenn wir im Transformer Attention nutzen dann werden die Token Embeddings geupdatet und werden zu den hidden Staates richtig? Und was passiert nach der Attention? 

## 1️⃣ Von Embeddings zu Hidden States

1. **Input Embeddings**: $X = [x_1, x_2, ..., x_n]$, plus Positionsinformationen.
    
2. **Self-Attention**:
    - Jedes Token schaut sich alle anderen Tokens an (Query-Key-Value).
    - Ergebnis: **kontextualisierte Token-Repräsentationen**.
    - Diese neuen Vektoren sind quasi die **Hidden States nach der Attention**.

💡 **Merke:** Hidden States = Embeddings + Kontextinformationen.

---

## 2️⃣ Nach der Attention

In einem Transformer Layer passiert typischerweise Folgendes **nacheinander**:

1. **Residual Connection + LayerNorm**
    
    - Die ursprünglichen Embeddings werden **hinzuaddiert** (residual connection)
        
    - Dann wird normalisiert (LayerNorm) → stabilisiert das Training.  $$  
        Z = \text{LayerNorm}(X + \text{Attention}(X))  
        $$
1. **Feed-Forward Network (FFN)**
    
    - Jeder Token wird **individuell durch ein kleines neuronales Netz** geschickt:  $$ 
        \text{FFN}(z_i) = W_2 \cdot \text{ReLU}(W_1 z_i + b_1) + b_2  
        $$
    - Das FFN erweitert die Repräsentation, fügt nicht-lineare Features hinzu.
    - Wieder: **Residual + LayerNorm** danach.
2. **Output des Layers**
    
    - Am Ende des Layers haben wir **aktualisierte Hidden States** für alle Tokens, bereit für den nächsten Layer.
---

## 3️⃣ Zusammenfassung

**Flow eines Transformer-Layers pro Token:**

```
Input Embedding → Self-Attention → Add & Norm → Feed-Forward → Add & Norm → Hidden State
```

- **Hidden States** sind also **kontextualisierte Embeddings**, die durch Attention + FFN angereichert werden.
- Jeder Layer baut auf den Hidden States des vorherigen Layers auf.
