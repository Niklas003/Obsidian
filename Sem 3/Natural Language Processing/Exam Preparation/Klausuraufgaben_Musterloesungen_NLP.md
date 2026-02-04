
# 🧪 Klausuraufgaben – Musterlösungen (DL & NLP)

## Aufgabe 1: RNN für Textklassifikation
**Aufgabe:** Definieren Sie ein RNN-Modell (Init + Forward).

### Musterlösung (Pseudocode)
```text
init(V, d, h, C):
    E = Embedding(V, d)
    RNN = RNNCell(d, h)
    W = Linear(h, C)

forward(tokens):
    h_t = 0
    for t in 1..T:
        x_t = E[tokens[t]]
        h_t = tanh(RNN(x_t, h_t))
    logits = W(h_t)
    return softmax(logits)
```

**Wichtige Hyperparameter:** hidden size, embedding dim

---

## Aufgabe 2: Vergleich Word Window vs RNN
**Frage:** Nennen Sie je einen spezifischen Hyperparameter und erklären Sie dessen Einfluss.

**Antwort:**
- Word Window: Window Size → bestimmt Kontextgröße
- RNN: Hidden Size → bestimmt Gedächtniskapazität

---

## Aufgabe 3: Transfer – Word Sense Disambiguation
**Modell:** BiLSTM / Transformer Encoder  
**Prediction:** Sense-ID pro Token  
**Loss:** Cross-Entropy pro Token  
**Metrik:** Accuracy / Macro-F1
