
# ✍️ Pseudocode Training – Lückenblatt

## Aufgabe 1: LSTM (Forward)

```text
h, c = 0, 0
for t in 1..T:
    x = _________

    i = sigmoid(_________)
    f = sigmoid(_________)
    o = sigmoid(_________)
    g = tanh(_________)

    c = _________
    h = _________
```

---

## Aufgabe 2: Transformer Encoder Block

```text
X = E_tok + _________

A = MHA(Q=____, K=____, V=____)
X = LayerNorm(____ + ____)

F = FFN(____)
X = LayerNorm(____ + ____)
```

---

## Aufgabe 3: GPT – warum Mask?

**Antwort (1 Satz):**
______________________________________
