
# 🧠 NLP Architectures – Constructor & Forward Pass (Klausur Notes)

> Lernziel: In der Klausur **Constructor (Init)** und **Forward Pass** verschiedener NLP-Architekturen sicher in **Pseudocode** darstellen und erklären können.
---

# 🧠 Hyperparameter in NLP-Architekturen – Übersicht & Erklärung

---

## 1️⃣ Bag of Words (BoW)

👉 **Idee:**  
Text = Zählvektor von Wörtern, **keine Reihenfolge**, **kein Kontext**

### Typische Hyperparameter

|Hyperparameter|Erklärung|Warum wichtig?|
|---|---|---|
|**Vocab Size**|Anzahl der Wörter im Wörterbuch|Größer = mehr Info, aber mehr Sparsity|
|**n-gram Größe**|Unigram, Bigram, Trigram|Erlaubt minimalen Kontext|
|**Binary vs Count vs TF-IDF**|Präsenz, Häufigkeit oder gewichtete Häufigkeit|Beeinflusst Skalierung & Aussagekraft|
|**Min / Max DF**|Filtert seltene oder zu häufige Wörter|Reduziert Rauschen|
|**Stopword Removal**|Entfernt häufige Funktionswörter|Kann helfen oder schaden|

🧩 **Klausur-Merksatz:**

> BoW hat **kaum Hyperparameter**, aber **keine Reihenfolge & kein semantisches Verständnis**

---

## 2️⃣ Word Embeddings (Word2Vec, GloVe)

👉 **Idee:**  
Wörter → dichte Vektoren mit semantischer Bedeutung

### Typische Hyperparameter

|Hyperparameter|Erklärung|
|---|---|
|**Embedding Dimension (d)**|Größe des Wortvektors|
|**Window Size**|Kontextfenster links/rechts|
|**Negative Samples**|Anzahl negativer Beispiele|
|**Min Count**|Seltene Wörter ignorieren|
|**Learning Rate**|Trainingsgeschwindigkeit|

🧠 **Wichtig:**

- Größere Dimension = mehr Ausdruckskraft
- Aber: Overfitting + mehr Rechenkosten

---

## 3️⃣ RNN (Recurrent Neural Network)

👉 **Idee:**  
Sequenzen **tokenweise**, Zustand wird weitergereicht

### Zentrale Hyperparameter

|Hyperparameter|Erklärung|Klausur-Bedeutung|
|---|---|---|
|**Hidden Size**|Dimension des Hidden States|„Gedächtnisgröße“|
|**Number of Layers**|Tiefe des RNN|Mehr Abstraktion|
|**Sequence Length**|Wie viele Tokens verarbeitet|Begrenzt Kontext|
|**Dropout**|Regularisierung|Gegen Overfitting|
|**Activation**|tanh / ReLU|Stabilität|

⚠️ **Problem:**

> Vanishing / Exploding Gradients ❌

---

## 4️⃣ LSTM (Long Short-Term Memory)

👉 **Idee:**  
RNN + **Gates** → besseres Langzeitgedächtnis

### Zusätzliche / wichtige Hyperparameter

|Hyperparameter|Erklärung|
|---|---|
|**Hidden Size**|Zellzustands-Dimension|
|**Number of Layers**|Mehrere LSTM-Schichten|
|**Dropout (recurrent)**|Auch auf rekurrente Verbindungen|
|**Bidirectional**|Vorwärts + Rückwärts|
|**Sequence Length**|Maximale Abhängigkeit|

🧠 **Klausur-Insight:**

> LSTM löst **Vanishing Gradient**, aber bleibt **sequentiell** → langsam

---

## 5️⃣ GRU (Gated Recurrent Unit)

👉 **Idee:**  
Vereinfachtes LSTM (weniger Gates)

### Unterschiede zu LSTM

|Punkt|LSTM|GRU|
|---|---|---|
|Gates|3|2|
|Parameter|mehr|weniger|
|Training|stabil|schneller|
|Performance|ähnlich|oft gleich gut|

🎯 **Merksatz:**

> GRU = „leichteres LSTM“

---

## 6️⃣ Transformer ⭐ (SEHR klausurrelevant)

👉 **Idee:**  
Keine Rekurrenz – **Self-Attention**, alles parallel 🚀

---

### 🔹 Zentrale Hyperparameter

#### 🔸 Modellgröße

|Hyperparameter|Erklärung|
|---|---|
|**d_model**|Dimension der Token-Repräsentation|
|**num_layers**|Anzahl Transformer-Blöcke|
|**num_heads**|Anzahl Attention-Köpfe|
|**d_ff**|Größe des Feed-Forward-Layers|

---

#### 🔸 Attention-spezifisch

|Hyperparameter|Erklärung|
|---|---|
|**Key / Query / Value Dim**|Projektionen für Attention|
|**Attention Dropout**|Regularisierung|
|**Masking**|Causal / Padding Mask|

---

#### 🔸 Training & Regularisierung

|Hyperparameter|Erklärung|
|---|---|
|**Dropout**|In Attention & FFN|
|**LayerNorm ε**|Numerische Stabilität|
|**Learning Rate Schedule**|z.B. Warmup|
|**Max Sequence Length**|Kontextfenster|

🧠 **Extrem wichtiger Klausur-Vergleich:**

|Eigenschaft|RNN / LSTM|Transformer|
|---|---|---|
|Parallelisierbar|❌|✅|
|Langzeitkontext|schwierig|sehr gut|
|Training Speed|langsam|schnell|
|Positionsinfo|implizit|explizit (Positional Encoding)|

---

## 7️⃣ Decoder-only Modelle (GPT-Style)

👉 **Idee:**  
Nur **Decoder**, autoregressiv

### Spezifische Hyperparameter

|Hyperparameter|Erklärung|
|---|---|
|**Causal Mask**|Keine Zukunft sehen|
|**Context Length**|Maximale Tokens|
|**Temperature**|Sampling-Stochastik|
|**Top-k / Top-p**|Sampling-Strategien|

---

# 🧠 Große Klausur-Zusammenfassung (SEHR MERKENSWERT)

> **Hyperparameter steuern:**
> 
> - **Kapazität** (Hidden Size, d_model)
>     
> - **Kontext** (Sequence Length, Window Size)
>     
> - **Komplexität** (Layers, Heads)
>     
> - **Regularisierung** (Dropout)
>     
> - **Training** (Learning Rate)
>     

---

## 🎓 Typische Klausurfragen (mit Antwort-Hinweis)

❓ _Warum braucht der Transformer Positional Encoding?_  
👉 Keine Rekurrenz → Reihenfolge fehlt

❓ _Was macht die Hidden Dimension?_  
👉 Speichert Features pro Token

❓ _Warum sind mehr Attention Heads sinnvoll?_  
👉 Verschiedene Subräume / Relationen

❓ _Warum ist BoW schlecht für Sprache?_  
👉 Kein Kontext, keine Reihenfolge

# Pseudocode
## 1️⃣ Bag of Words (BoW)

### Idee
- Text = Zählvektor
- Keine Reihenfolge, kein Kontext

### Constructor
```text
init(vocab_size V, num_classes C):
    W ∈ R^(C×V)
    b ∈ R^C
```

### Forward Pass
```text
forward(tokens):
    x = bow_vector(tokens)
    logits = W x + b
    return softmax(logits)
```

🔑 Merke:
- Sehr einfach
- Keine Sequenzinformation

---

## 2️⃣ Embedding + Pooling

### Constructor
```text
init(V, d, C):
    E ∈ R^(V×d)
    W ∈ R^(C×d)
    b ∈ R^C
```

### Forward
```text
forward(tokens):
    H = [E[t] for t in tokens]
    h = mean(H)
    logits = W h + b
    return softmax(logits)
```

🧠 Tipp:
- Pooling ersetzt Reihenfolge nur sehr grob

---

## 3️⃣ RNN

### Constructor
```text
init(V, d, h, C):
    E ∈ R^(V×d)
    W_xh ∈ R^(h×d)
    W_hh ∈ R^(h×h)
    W_out ∈ R^(C×h)
```

### Forward
```text
h = 0
for t in 1..T:
    x = E[token_t]
    h = tanh(W_xh x + W_hh h)
logits = W_out h
return softmax(logits)
```

⚠️ Problem:
- Vanishing Gradient

---

## 4️⃣ LSTM

### Idee
- Memory Cell + Gates

### Forward (Klausurversion)
```text
h, c = 0, 0
for t in 1..T:
    x = E[token_t]

    i = sigmoid(W_i x + U_i h)
    f = sigmoid(W_f x + U_f h)
    o = sigmoid(W_o x + U_o h)
    g = tanh(W_g x + U_g h)

    c = f ⊙ c + i ⊙ g
    h = o ⊙ tanh(c)
```

🎯 Merke:
- c = Langzeitgedächtnis

---

## 5️⃣ GRU

### Forward
```text
h = 0
for t in 1..T:
    x = E[token_t]

    z = sigmoid(W_z x + U_z h)
    r = sigmoid(W_r x + U_r h)
    n = tanh(W_n x + U_n (r ⊙ h))

    h = (1 - z) ⊙ h + z ⊙ n
```

🧠 Vergleich:
- Weniger Parameter als LSTM

---

## 6️⃣ Transformer Encoder

### Bausteine
- Embedding + Positional Encoding
- Multi-Head Self-Attention
- Feed-Forward Network

### Forward (1 Block)
```text
X = E_tok + E_pos

A = MHA(X, X, X)
X = LayerNorm(X + A)

F = FFN(X)
X = LayerNorm(X + F)
```

🔑 Wichtig:
- Voll parallelisierbar
- Bidirektionaler Kontext

---

## 7️⃣ Transformer Decoder-only (GPT)

### Besonderheit
- Causal Mask

### Forward
```text
X = E_tok + E_pos
mask = causal_mask()

A = MHA(X, X, X, mask)
X = LayerNorm(X + A)

F = FFN(X)
X = LayerNorm(X + F)

logits = X W_vocab^T
```

🚀 Merke:
- Autoregressiv
- Next-token prediction

---

## 🧾 Klausur-Merksätze

- RNN/LSTM/GRU → **sequentiell**
- Transformer → **parallel**
- GPT → **Decoder-only + Causal Mask**
- Hidden Dimension = Feature-Repräsentation pro Token

---

✨ Lerntipp:
> Versuche jede Architektur **einmal aus dem Kopf** in Pseudocode aufzuschreiben – genau das ist Klausurniveau!
