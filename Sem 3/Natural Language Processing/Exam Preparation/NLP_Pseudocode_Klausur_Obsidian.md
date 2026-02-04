
# 🧠 NLP Architectures – Constructor & Forward Pass (Klausur Notes)

> Lernziel: In der Klausur **Constructor (Init)** und **Forward Pass** verschiedener NLP-Architekturen sicher in **Pseudocode** darstellen und erklären können.

---

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
