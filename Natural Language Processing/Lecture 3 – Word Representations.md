# 🧠 Lecture 3 – Word Representations
**Course:** Deep Learning and Natural Language Processing  
**Lecturer:** Prof. Dr. Alan Akbik  
**Topic:** Representing words as numerical vectors for machine learning and NLP tasks  
**Tags:** #NLP #WordEmbeddings #DeepLearning #Word2Vec #FastText #LexicalSemantics #DistributionalSemantics  

---

## 🧩 Recap and Motivation

Machine learning models require **numerical input**, so text must be converted into numbers.  
The key question:  
> How can we represent the *meaning* of words numerically?

Early approaches focused on **syntactic encoding** (e.g., one-hot), while modern methods aim to capture **semantic similarity**.

---

## ⚙️ One-Hot Encoding

### Concept
Each word (or label) is represented as a **vector of zeros** with a single **1** in one position.

Example (sentiment labels):
```
POSITIVE = [1, 0, 0]
NEUTRAL  = [0, 1, 0]
NEGATIVE = [0, 0, 1]
```

**Orthogonal vectors:**  
Each label is independent — no information about similarity or order (e.g., “neutral” isn’t between “positive” and “negative”).

So if we would plot the vectors (if we could) all vectors would be #orthogonal

### Limitations
- Doesn’t encode **semantic relationships** between words  
- Vectors grow large as vocabulary increases  
- Unseen words → model cannot generalize  

---

## 📊 Count Vectorization

### Idea
Represent a text by **counting** how often each word appears (bag-of-words).

Example:  
```
“great just great!”
→ great: 2, just: 1
```

Yields a vector like `[2, 1, 0, 0, ...]`.

### Problem
- Ignores word order (“great movie” vs. “movie great”)
- Vocabulary still huge (unlimited amount of words)
- No semantics (only frequency)

---

## 🤖 Text Classification with 1-Layer NN

A **single-layer neural network** can take these count vectors as input to predict sentiment labels.

But…  
If a new word appears in test data (e.g. “baaaad”), the model fails — it has never seen that word during training.

---

## 🚫 Generalization & Infinite Words

- Infinite possible words and variants (“greatttt”, “awesommmmme”)  
- Long-tail distribution — many rare words  (A lot of common words but alos a lot of rare/domain specific words)
- Too costly to label enough data for all variants  

➡️ We need a **representation that generalizes** to unseen but related words.

---

## 🧠 Prior Knowledge on Word Semantics

We know intuitively:
- “great” and “good” are both positive
- “movie” and “film” are synonyms

The goal: **embed such relationships** into vector space representations.

---

## 📚 Lexical Semantics: WordNet

### WordNet Overview
A **manually built lexical database** (Miller, 1995):
- Groups words into **synsets** (sets of synonyms)
- Defines relationships like:
  - **Synonymy:** tie ↔ necktie  
  - **Hypernymy:** tie → neckwear (category)  
  - **Hyponymy:** neckwear → tie  

### Example Code (NLTK)
```python
from nltk.corpus import wordnet
wordnet.synsets('tie')
```

### Strengths
- Captures rich **hierarchical relationships**
- Useful for semantic reasoning

### Limitations
1. **Manual construction:** time-consuming, incomplete
2. **Discrete senses:** difficult to define “what is a sense?”
3. **Not vectorized:** can’t directly use in neural networks
4. **Coverage issues:** new words, domains, and languages

---

## 🔁 Distributional Semantics

> “The meaning of a word is determined by the company it keeps.” — *J.R. Firth (1957)*  
> “Difference of meaning correlates with difference of distribution.” — *Zellig Harris (1954)*  

### Motivation
- Manual encoding is impossible at scale  
- Derive meaning **automatically** from usage patterns in text  

---

## 🧮 Word-Word Co-occurrence Matrix

### Step-by-Step
1. **Build vocabulary** of unique words  
2. **Count co-occurrences** within a context window  
   - E.g. window size = 2 or 5  
3. **Matrix entry (i, j)** = number of times word *i* appears near word *j*

### Example
```
         ate restaurant fly air
pizza     2     1        0   0
pasta     1     1        0   0
bird      0     0        1   1
airplane  0     0        1   1
```
→ “pizza” and “pasta” have similar rows → similar meaning.

### Problem
Very large and sparse matrix (n×n where n = vocabulary size).

---

## 🧭 Cosine Similarity

Measures **similarity** between word vectors:
$$
\text{sim}(A,B) = \frac{A \cdot B}{||A|| \, ||B||}
$$
- Range: [-1, 1]
- Normalizes for vector length

Example:  
- sim(pizza, pasta) ≈ 0.9 → similar
- sim(pizza, airplane) ≈ 0.1 → unrelated  

---

## ⚠️ Problems with Raw Co-occurrence

### 1. Frequent Words
Words like “the”, “is”, “and” co-occur with everything and everywhere → dominate counts.

### 2. Huge Vocabulary
> 100,000+ words → extremely high-dimensional and memory heavy.

---

## 🧠 Pointwise Mutual Information (PMI)

Statistische Signifikanz messen
Measures **how much more often** two words co-occur than expected by chance:
$$
PMI(x, y) = \log \frac{P(x, y)}{P(x)P(y)}
$$

- Positive PMI → strong association  
- Negative PMI → rare or independent  

### Example:
Replacing raw counts with PMI highlights **meaningful** relationships instead of frequency artifacts.

---

## 🔽 Dimensionality Reduction: SVD

So that we don't have infinite number of dimensions in our vector
### Singular Value Decomposition
Compresses high-dimensional data (e.g. 100k→300 Dimensions)  
Keeps **most informative patterns** (latent semantics).

Benefits:
- Reduces sparsity  
- Captures higher-order co-occurrences  
- Smooths noisy relationships  

### Analogy Discovery
SVD uncovers semantic patterns like:
- “Swim” → “swimmer”
- “Drive” → “driver”
- “King” - “man” + “woman” = “queen”

---

## 🧭 Distributional Patterns and Analogies

Low-dimensional embeddings encode:
- Semantic relations (Paris : France :: Tokyo : Japan)
- Syntactic patterns (good : better :: fast : faster)
- Gender, role, and domain analogies  

### Libraries
**Gensim** enables easy exploration of such embeddings:
```python
import gensim.downloader as api
model = api.load("glove-wiki-gigaword-100")
model.most_similar("pizza")
model.doesnt_match("lunch breakfast dinner cereal".split())
```

---

## ⚡ Word2Vec – Prediction-Based Approach

[Mikolov et al., 2013]

### Core Idea
Instead of counting co-occurrences, **predict** them.

Two architectures:
- **CBOW (Continuous Bag of Words):** predict center word from context. Like: I ate __ in Italy
- **Skip-Gram:** predict context words from center word. Like __ __ pasta __ __   

### Skip-Gram Example
Sentence: “I ate great pasta in Italy”  
Context window (size 2):
```
(pasta, ate), (pasta, great), (pasta, in), (pasta, Italy)
```

Each pair becomes a training example.

---

## 🧩 Skip-Gram Model Architecture

- Input: one-hot encoded center word  
- Hidden layer: **embedding layer** (learned word vector)  
- Output: softmax predicting context word  

After training, we **discard the output layer** and **keep embeddings**.

### Advantages
- Learns dense semantic vectors
- Efficient with large corpora
- Encodes both syntactic and semantic regularities

---

## 🧪 Evaluation of Word Embeddings

### Intrinsic Evaluation
Tests embedding properties directly:
- **Word similarity** (e.g. WordSim353 dataset)
- **Analogies** (“Paris is to France as Tokyo is to ?”)

### Extrinsic Evaluation
Tests performance on downstream tasks:
- Sentiment analysis
- NER, translation, etc.  

---

## 🆚 Count-based vs Prediction-based

| Aspect | Count-based (PMI+SVD)       | Prediction-based (Word2Vec) |     |
| ------ | --------------------------- | --------------------------- | --- |
| Method | Matrix factorization        | Neural prediction           |     |
| Pros   | Theoretically interpretable | Scalable, efficient         |     |
| Cons   | Computationally heavy       | Hyperparameter sensitive    |     |
| Signal | Co-occurrence               | Co-occurrence (implicitly)  |     |

Both use the **same statistical signal**—they just process it differently.

---

## ⚡ FastText Classifier (Facebook, 2016)

### Goal
A fast, simple baseline for text classification using embeddings.

### Architecture
1. **Embedding layer** – maps one-hot words to dense vectors  
2. **Pooling layer** – averages embeddings over the text (mean/max)  
3. **Softmax classifier** – predicts label

Example:
```
“not good” → [embedding(not), embedding(good)] → mean → sentiment
```

### Limitation
Bag-of-words approach loses order information:
- “Not bad” vs. “Not good” → different meanings, same average.

---

## 🧩 N-gram Extensions

FastText adds **n-gram embeddings** (e.g. bigrams, trigrams)  
→ captures local order and short dependencies.

Example:
```
“Not bad at all” → ["not", "bad", "not bad", "bad at", "at all"]
```

This helps distinguish between subtle sentiment differences.

---

## ⚙️ Hyperparameters
- **Embedding dimension (h):** 50–300 typical  
- **N-grams:** 1–3 for text classification  
- Tradeoff between expressiveness and speed  

---

## 🎯 Task-Specific Embeddings

- **Word2Vec:** general-purpose embeddings (trained unsupervised on large corpora)  
- **FastText (classifier):** task-specific embeddings (fine-tuned for one task like sentiment)

---

## 🧩 Summary

| Concept | Description |
|----------|--------------|
| **One-hot encoding** | Simple, orthogonal, no semantics |
| **WordNet** | Manual lexical knowledge, not scalable |
| **Distributional semantics** | Meaning from context |
| **PMI + SVD** | Count-based latent semantics |
| **Word2Vec** | Prediction-based word embeddings |
| **FastText** | Efficient classifier using embeddings + pooling + n-grams |

**Takeaway:**  
Word representations are the foundation of NLP — they allow models to capture **meaning**, **similarity**, and **context** in a mathematically useful form.
