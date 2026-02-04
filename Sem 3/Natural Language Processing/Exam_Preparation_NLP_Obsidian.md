
# 🧠 Exam Preparation – Deep Learning & NLP (Lecture 24)

> **Quelle:** Lecture *Exam Preparation and Research Overview* fileciteturn0file0  
> **Ziel dieser Note:** Klausur-orientierte Lernnotiz mit Fokus auf **Beispielaufgaben**, **Pseudocode** und **Hyperparameter-Vergleiche**.

---

## 🎯 Klausur-Setup (Wichtig!)

- **90 Minuten**, schriftlich
- **Fragetypen**:
  - Pseudocode
  - Demonstration (Annotation, Preprocessing)
  - Mathe / Formeln
  - Vergleich zweier Modelle
  - Transfer-Fragen

👉 Alles aus Vorlesung + Übungen ist relevant (Übungen besonders!).

---

## 1️⃣ Pseudocode-Fragen (Kernkompetenz)

### Erwartet:
- Constructor-Argumente (**Hyperparameter!**)
- Initialisierte Layer
- Aktivierungen
- Forward-Reihenfolge

### Beispiel: Seq2Seq mit RNN (ohne Attention)

```text
init(src_vocab, tgt_vocab, emb_dim, h_enc, h_dec):
    src_emb = Embedding(src_vocab, emb_dim)
    enc_rnn = LSTM(emb_dim, h_enc)

    tgt_emb = Embedding(tgt_vocab, emb_dim)
    dec_rnn = LSTM(emb_dim, h_dec)

    out = Linear(h_dec, tgt_vocab)
```

Hyperparameter:
- emb_dim
- h_enc, h_dec

---

## 2️⃣ Demonstration: BIO / BIOES

```text
Bill    B-PER
likes   O
New     B-LOC
York    I-LOC
```

Verwendet bei:
- NER
- Chunking

---

## 3️⃣ Vergleichsfragen & Hyperparameter ⭐

### Word Window vs RNN (POS)

| Aspekt | Window | RNN |
|---|---|---|
| Kontext | Fix | Global |
| Haupt-HP | Window Size | Hidden Size |
| Parallel | Ja | Nein |

**Effekt Window Size:**
- hoch → mehr Kontext, Overfitting
- niedrig → wenig Kontext

---

## 4️⃣ Hyperparameter nach Architektur

### Bag of Words
- Vocabulary Size
- UNK Threshold
- n-grams

### RNN / LSTM / GRU
- Hidden Size
- Layers
- Dropout

### Transformer
- d_model
- num_heads
- num_layers
- d_ff
- max_seq_len

### Language Modeling
- Context Length
- Temperature
- Top-k / Top-p
- Beam Width

---

## 5️⃣ Transfer: Word Sense Disambiguation

- Architektur: BiLSTM / Transformer Encoder
- Task: Klassifikation pro Token
- Output: WordNet Sense ID

Wichtige Hyperparameter:
- Hidden Size
- Kontextfenster

---

## 6️⃣ Evaluation

| Task | Metric |
|---|---|
| Classification | Accuracy / F1 |
| NER / POS | Token-F1 |
| LM | Perplexity |
| MT | BLEU (mit Limits) |

Intrinsic vs Extrinsic:
- Direkt vs Downstream

---

## 🧠 Klausur-Merksätze

- Vergleich = Hyperparameter nennen
- Pseudocode = Init + Forward
- Transformer = parallel
- RNN = sequentiell

---

## 📚 Lernstrategie

1. Jede Architektur einmal aus dem Kopf schreiben
2. Pro Architektur 2–3 Hyperparameter erklären
3. Vergleichsfragen üben
4. Annotation einmal manuell machen
