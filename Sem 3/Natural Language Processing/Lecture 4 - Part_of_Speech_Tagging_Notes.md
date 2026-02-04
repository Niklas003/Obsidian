# 🧠 Lecture 4 – Part-of-Speech Tagging
**Course:** Deep Learning and Natural Language Processing  
**Lecturer:** Prof. Dr. Alan Akbik  
**Topic:** Syntax, Part-of-Speech Tagging, and Evaluation of Word Embeddings  
**Tags:** #NLP #POS #DeepLearning #WordEmbeddings #Syntax #PyTorch #Word2Vec  

---

## 🧩 Recap and Motivation

In the last lecture, we explored **word representations** — how to encode semantic meaning using numerical vectors.  
We saw:  
- One-hot encodings lack semantics  
- Word embeddings capture **latent meaning** via context  

Now, we move to **syntax** — the structure and grammatical roles of words in sentences.  
We’ll build a **Part-of-Speech (PoS) tagger**, step by step.

---

## 🧠 From Semantics to Syntax

### Word Semantics Recap
- “great” and “good” → similar meaning  
- “movie” and “film” → synonyms  
- Word embeddings (Word2Vec, SVD) represent words in continuous vector space

However — **semantic similarity ≠ syntactic understanding**.  
A model must also understand *how words function grammatically*.

---

## 🧮 Word Representations Review

### One-Hot Encoding of Words
Each unique word is assigned a vector of zeros with a single 1.  
Problem: It doesn’t encode relationships or meaning.

### WordNet
A **manually constructed lexical database** [Miller, 1995]:  
- Groups words into *synsets* (sets of synonyms)  
- Defines relationships like synonymy, hypernymy, hyponymy  
Limitation: manually built, discrete, not scalable.

### Distributional Hypothesis
> “You shall know a word by the company it keeps.”  
   Words with similar meaning occur in similar contexts.

Example corpus co-occurrence:  
```
pizza   pasta   bird   airplane
ate     2       1      0      0
restaurant  1   1      0      0
fly     0       0      1      1
air     0       0      1      1
```

Low-dimensional approximations (via **SVD** or **Word2Vec**) yield **dense embeddings**.

---

## ⚙️ Word2Vec: Skip-Gram Model

Neural model with two linear layers:  
- Input: word (one-hot encoded)  
- Output: predicted context word (one-hot encoded)  

Architecture:
```
Input → Embedding Layer → Linear Layer + Softmax → Output Word
```

After training, we **discard the classifier** and keep the learned embeddings.

These embeddings capture both **semantic** and **syntactic** information (e.g., “king” - “man” + “woman” ≈ “queen”).

---

## 💡 Discrete vs Latent Representations

- **Discrete (symbol-based):** e.g. WordNet → explicit, interpretable, but inflexible 
	- you can not do operations like in the latent representation
	- one can better debug, maintain but it still has these scalability issues
- **Latent (vector-based):** e.g. Word2Vec → captures patterns, **scalable**, but abstract  

Next: Evaluate whether embeddings *actually help* with NLP tasks.

---

## 🧪 Evaluation of Word Embeddings

### Two Evaluation Types

| Type          | Focus                                                                                       | Pros                | Cons                                   |
| ------------- | ------------------------------------------------------------------------------------------- | ------------------- | -------------------------------------- |
| **Intrinsic** | Do embeddings have specific props?<br><br>Embeddings themselves (e.g., similarity, analogy) | Fast to test        | May not reflect downstream performance |
| **Extrinsic** | Are embeddings useful?<br><br>Task-based evaluation (e.g., PoS tagging)                     | Measures usefulness | Slower to test, dependent on task      |

### Intrinsic Evaluation Examples

#### Word Similarity
- Dataset: *WordSim353*
- Compare cosine similarity between embeddings with human judgments.
- Human judgements of similarities

#### Word Analogies
- Example: *MEDICINE : ILLNESS :: LAW : ?*
- Model performs vector arithmetic:  
  `A - B + C ≈ D`  
  Example: `Paris - France + Japan ≈ Tokyo`

**Limitations:** Evaluations depend on dataset biases and linearity assumptions.

---

## ⚔️ Comparison of Embedding Approaches

| Approach | Principle | Pros | Cons |
|-----------|------------|------|------|
| **Count-based** | Word-word PMI + SVD | Theoretically grounded | Expensive to compute |
| **Prediction-based (Word2Vec)** | Predict surrounding words | Scalable, robust | Sensitive to hyperparameters |

→ No universally best method — both exploit *word co-occurrence signals*.
- Look at the Paper results
- Why then SVD? B.C. Comutation complexety

---
## Summary: Word Embeddings

- Limitations:
	- Frequent words co-occur
	- different words have different meaning

---
## 📘 Syntax: Structure of Sentences

**Syntax:** study of how words combine into phrases and sentences.  
It defines **grammatical structure**, not meaning.

Example:  
> “Colorless green ideas sleep furiously.”  
   → Grammatically correct (syntactically valid) but semantically nonsensical.
   **BRO IT MAKES NO SENSE BUT IT IS GRAMMATICALLY CORRECT**
### Syntax vs Semantics
| Syntax                | Semantics           |
| --------------------- | ------------------- |
| Structure of language | Meaning of language |
| Governed by rules     | Governed by context |

---

## 🌍 Multilinguality

There are over **7,000 human languages**, each with its own syntactic structure.  
While syntax differs, **syntactic categories** (nouns, verbs, etc.) are universal.

---

## 🧠 Levels of Syntactic Analysis

| Type | Description | Example |
|-------|--------------|----------|
| **Shallow Syntax** | Classify each word’s grammatical category | “run” → Verb |
| **Deep Syntax** | Capture phrase structure and dependencies | “The dog runs” → Subject-Verb structure |

---

## 🧩 Parts-of-Speech (PoS)

A **Part of Speech (PoS)** is a category of words with similar grammatical roles.

### Examples
- **Noun**: “dog”, “city”, “love”  
- **Verb**: “run”, “is”, “eat”  
- **Adjective**: “happy”, “red”  
- **Adverb**: “quickly”, “very”  
- **Pronoun**, **Preposition**, **Conjunction**, etc.

Automatic PoS tagging = predict the grammatical category for each word in a text.

---

## 🔒 Open-Class vs Closed-Class Words

| Type             | Description                           | Examples                         |
| ---------------- | ------------------------------------- | -------------------------------- |
| **Open Class**   | New words can be added; carry meaning | Nouns, verbs, adjectives         |
| **Closed Class** | Fixed set; functional roles           | Pronouns, prepositions, articles |

Open classes = content words - words classes that can be extended  z.B. Wortneuschöpfungen
Closed classes = grammatical glue

---

## 🧾 PoS Tagsets

### Penn Treebank (English)
- 36 tags + 12 punctuation tags  
- Verb tags include tense and aspect (all start with “VB”)

| Tag | Description | Example |
|------|--------------|----------|
| VB | Base form | *sing* |
| VBZ | 3rd person present | *sings* |
| VBD | Past tense | *sang* |
| VBG | Gerund | *singing* |
| VBN | Past participle | *sung* |
| VBP | Non-3rd person present | *sing* |

### STTS (German)
Large set covering adjectives, verbs, pronouns, etc.  
Includes distinctions between **modal**, **auxiliary**, and **full verbs**.

---

## 🌐 Universal PoS Tags

To compare across languages, **Petrov et al. (2011)** introduced *Universal PoS Tags*  
→ 12 coarse tags (later 18) covering >100 languages [Nivre et al., 2016].

Applications:
- Multilingual PoS tagging
- Cross-lingual NLP
- Low-resource languages

---

## 🧭 Applications of PoS Tagging

- **Text analytics:** Identify adjectives describing brands (“tasty”, “cheap”)  
- **Preprocessing:** Filter function words (stopwords)  
- **Linguistic research:** Analyze syntactic patterns across corpora  

Example: [Nickl et al., 2024] analyzed how news headlines evolved —  
Clickbait uses more **pronouns**, **wh-words**, and **demonstratives**.

---

## 🧩 Syntax-Aware Word Embeddings (Sense2Vec)

Train embeddings *after* PoS tagging a corpus → differentiate meanings based on syntax.

Example:  
“I can open the can.” →  
`I.p can.v open.v the.d can.n`

Thus, `can.v` (verb) ≠ `can.n` (noun).  
Improves contextual understanding in downstream tasks.

---

## ⚙️ Building a Simple PoS Tagger

Goal: Predict a PoS tag for each word in a sentence.

### Naive Approach
Each word is embedded and classified independently:
```
Input word → Embedding → Linear Layer + Softmax → PoS tag
```
→ No context awareness.

### Implementation in PyTorch

```python
class SingleWordTagger(torch.nn.Module):
    def __init__(self, vocab_size, num_tags, embedding_dim):
        super().__init__()
        self.embedding = torch.nn.Embedding(vocab_size, embedding_dim) #embedding layer
        self.linear = torch.nn.Linear(embedding_dim, num_tags) #linear layer
        self.loss_function = torch.nn.NLLLoss()

    def forward(self, tokens, pos_tags=None):
        embeddings = [self.embedding(torch.tensor([t])) for t in tokens]
        features = [self.linear(e) for e in embeddings]
        log_probs = torch.cat([torch.nn.functional.log_softmax(f, dim=-1) for f in features])
        result = {"log_probs": log_probs}
        if pos_tags is not None:
            result["loss"] = self.loss_function(log_probs, torch.tensor(pos_tags))
        return result
```

### Limitation
- Each word is tagged **independently** — no context from neighboring words.
- Limited to classify only words that we have in our training data.

Accuracy: ~0.76  

---

## 🧠 Improvement 1 – Use Pretrained Word Embeddings

Initialize the embedding layer with **Word2Vec** or **GloVe** weights.

Benefits:
- Pre-trained on massive text data  
- Captures general word semantics  
- Reduces need for large labeled datasets

Result: Accuracy improves to **0.84**

---

## 🧠 Improvement 2 – Add Context Window

Words depend on their **context** (“can” = noun or verb?).  
→ Include neighboring words in classification.
Introduce a "window"
### Idea
Concatenate embeddings of current word + its neighbors:
```
window = [word_{i-1}, word_i, word_{i+1}]
x = concat(embeddings(window))
```
Feed `x` into the classifier.

### Implementation
```python
class FixedContextWordTagger(torch.nn.Module):
    def __init__(self, vocab_size, num_tags, embedding_dim, context_size):
        super().__init__()
        self.embedding = torch.nn.Embedding(vocab_size, embedding_dim)
        self.linear = torch.nn.Linear(embedding_dim * (1 + 2 * context_size), num_tags)

    def forward(self, tokens):
        # Pad and concatenate context embeddings
        # Example: context_size = 1 → left, center, right
        pass
```

Padding with zero vectors ensures consistent window size at sentence boundaries.

### Performance
| Model | Context | Pretrained | Accuracy |
|--------|----------|------------|-----------|
| Naive | ✗ | ✗ | 0.76 |
| Naive | ✗ | ✓ | 0.84 |
| Context Window (3) | ✓ | ✗ | 0.79 |
| Context + Embeddings | ✓ | ✓ | **0.88** |

---

## 🧩 Summary

| Concept | Description |
|----------|--------------|
| **PoS Tagging** | Assign grammatical classes to words |
| **Naive Tagger** | Word-level classification, no context |
| **Word Embeddings** | Improves representation and generalization |
| **Context Window** | Captures local syntactic dependencies |
| **Universal PoS Tags** | Enables multilingual tagging |

### Takeaway
> Combining **word embeddings** and **context modeling** dramatically improves syntactic tagging accuracy.

---

## 🧱 Homework / Next Steps
- Implement the naive and context-based PoS taggers in PyTorch  
- Use pretrained embeddings (Word2Vec or GloVe)  
- Compare accuracy and analyze confusion between tags  

---

📘 **End of Lecture 4 – Part-of-Speech Tagging**
