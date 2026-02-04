# 🧠 Lecture 5 – The Classic NLP Pipeline
**Course:** Deep Learning and Natural Language Processing  
**Lecturer:** Prof. Dr. Alan Akbik  
**Topic:** The Classic NLP Pipeline: Segmentation, Morphology, and Parsing  
**Tags:** #NLP #Syntax #Parsing #Tokenization #Lemmatization #Morphology #DependencyParsing #Treebanks  

---

## 🧩 Recap and Motivation

In the previous lecture, we built a **Part-of-Speech (PoS) Tagger**, learning how to classify each token’s grammatical category using word embeddings and context.  

Now we’ll go deeper into **syntactic analysis** — examining how text is processed and structured in traditional NLP before deep learning.

---

## ⚙️ The Classic NLP Pipeline

The **Classic NLP Pipeline** consists of a sequence (series of steps) of preprocessing steps that transform **raw text** into **structured linguistic data** for machine learning and linguistic analysis.

### Pipeline Steps
1. **Sentence Splitting** – Identify sentence boundaries  
2. **Tokenization** – Split sentences into individual tokens (what are individual words in the text) 
3. **PoS Tagging** – Assign grammatical tags to tokens  
4. **Lemmatization** – Normalize words to their dictionary form ->  **Lexical normalisation** 
5. **Dependency Parsing** – Model grammatical relations between tokens  

```
Raw Text → [Segmentation → Normalization → Syntax Analysis] → Parsed Text
```

Goal: Obtain a **parsed text representation** that serves as a strong foundation for downstream NLP tasks (e.g., information extraction, translation, sentiment analysis).

---
## Vauquois Triangle

![[Pasted image 20251028112424.png]]

---

## 🧠 Why Pipelines Matter

- Early NLP systems relied heavily on **linguistic rules** and **structured representations**
- Understanding the pipeline is essential for **hybrid** (symbolic + neural) NLP approaches
- Many **modern libraries (SpaCy, Stanza, Flair)** still internally follow this structure

---

## 🧩 Sentence Splitting

### Definition
The task of **segmenting raw text into sentences**.

**Input:** Plain text  
**Output:** List of sentences  

### Simple Heuristic
Sentences typically end with punctuation (`.`, `!`, `?`).

Example:
```
Input: "This is a sentence. This is another sentence."
Output: ["This is a sentence.", "This is another sentence."]
```

### ❌ Problem
Heuristic fails with:
- Abbreviations (“e.g.”, “Dr.”, “Prof.”)
- Names (“Avram N. Chomsky”)
- Ellipses and dialogue punctuation

---

## 🔧 Approaches to Sentence Splitting

| Type                 | Description                                                                               | Example Tool |
| -------------------- | ----------------------------------------------------------------------------------------- | ------------ |
| **Rule-based**       | Handcrafted punctuation rules; exceptions for abbreviations like from known abberviations | `SegTok`     |
| **Prediction-based** | Train model to classify if a punctuation ends a sentence                                  | `SpaCy`      |

### Example – SegTok (Rule-based)
```python
from segtok.segmenter import split_single
text = "Prof. Chomsky gave a talk. It was inspiring."
sentences = list(split_single(text))
print(sentences)
```

### Example – SpaCy (ML-based)
```python
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp("Prof. Chomsky gave a talk. It was inspiring.")
print([sent.text for sent in doc.sents])
```

SpaCy learns exceptions statistically rather than relying on manual rules.

---

## 🧱 Tokenization

**Tokenization** splits text into **tokens** — atomic units such as words, punctuation, or subwords.

### Example
```
Input: "Interesting talk by Prof. Chomsky."
Output: ["Interesting", "talk", "by", "Prof.", "Chomsky", "."]
```

### Challenges
- Apostrophes and contractions (`aren’t`, `O’Neill`)  
- Clitics (e.g., *dámelo* in Spanish)  
- Multiword expressions (“San Francisco”, “by and large”)  
- Compounds (“skyscraper”, “Abwasserbehandlungsanlage”)

---

## 🧩 Apostrophes and Clitics

**Apostrophes** cause tokenization ambiguity:  
- "aren’t" → “are”, “n’t” or “aren’t”?  
- "O’Neill" → “O”, “Neill” or “O’Neill”?

**Clitics** are syntactically independent but phonologically dependent:  
- Spanish: *dámelo* = *da me lo* ("give me it")  
- French: *au revoir* = *à le revoir* ("to the seeing again")

Tokenizers must handle these language-specific contractions correctly.

---

## 🏗️ Compound Words

Compounds combine multiple words into one concept:

| Language                 | Example                   | Tokenization Challenge         |
| ------------------------ | ------------------------- | ------------------------------ |
| **German**               | Abwasserbehandlungsanlage | Often needs splitting          |
| **English (open)**       | "high school"             | Split                          |
| **English (hyphenated)** | "must-have"               | Ambiguous, depend on tokenizer |
| **English (closed)**     | "skyscraper"              | Not split                      |

Classic tokenizers typically **don’t split closed compounds**.  
Advanced German NLP tools perform **compound decomposition**.

---

## 🧩 Multiword Units (MWUs)

Multiword units act as **single syntactic units**:  
- “New York”  
- “by and large”  _(mamals have, by and large, bigger brains then reptiles)_
- “machine learning”  

Classic tokenizers **split** MWUs, but syntactic chunking or NER later re-links them.

---

## 🧾 Tokenization in Treebanks

### Treebanks and Tokenization
Treebanks typically assume **pre-tokenized text**.  
For example, the **OntoNotes** corpus uses simple whitespace-based tokenization.  

However, **Universal Dependency (UD)** treebanks perform **token transformation** for accurate syntactic annotation.

---

## ⚙️ Morphological Specification

Each word is described by three components (in UD formalism):

1. **Lemma** – canonical dictionary form  
2. **PoS tag** – abstract lexical category  
3. **Morphological features** – grammatical details (tense, number, gender, etc.)

### Example
| Text | Lemma | PoS | Features |
|------|--------|------|-----------|
| Solutions were found | solution | NOUN | plural |
| were | be | AUX | past tense |
| found | find | VERB | past participle |

---

## 🧠 Lemmatization

### Definition
The task of mapping inflected or derived words to their **dictionary form (lemma)**.

| Word | Lemma |
|-------|--------|
| houses | house |
| mice | mouse |
| found | find |
| finding | find |

**Applications:**
- Search normalization (query for “mouse” finds “mice”)
- Morphological analysis
- Data sparsity reduction

### Example (SpaCy)
```python
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp("The mice found some houses.")
print([(token.text, token.lemma_) for token in doc])
```

---

## 🧩 Lexical & Grammatical Features

- **Nouns:** number (singular/plural), gender, case  
- **Verbs:** tense, voice, aspect, person  
- **Languages differ:** some have extra cases or tenses (e.g., Finnish, Arabic)

Example:  
- “found” → `Tense=Past|Voice=Active`  
- “mice” → `Number=Plur`

---

## ⚖️ Morphological Tagging

Similar to PoS tagging, but with **finer-grained labels** combining PoS and features.

Example:

| Token | PoS | Morphology |
|--------|------|-------------|
| chairs | NOUN | Number=Plur |
| a | DET | Number=Sing |
| table | NOUN | Number=Sing |

---

## 🔁 Lemmatization via Edit Rules

Instead of predicting the lemma directly, models often predict **edit rules**.

| Rule                                                 | Example                 |
| ---------------------------------------------------- | ----------------------- |
| Do nothing                                           | “positive” → “positive” |
| Remove last “s”                                      | “things” → “thing”      |
| Replace ending, Remove last 3 chars and add "e", ... | “driving” → “drive”     |

---

## 🧠 Applications of Morphology

- **Search & IR:** normalization improves recall  
- **Lexicography:** linguistic analysis of inflectional systems  
- **Limited industry use**, except in high-precision linguistic systems (translation, education).

---

## 🧩 Dependency Parsing

While PoS tagging labels each word individually, **dependency parsing** models the **syntactic relationships** between words.

### Example
> “The cats sing a happy song.”

- Head of “cats” → “sing” (subject)  
- Head of “song” → “sing” (object)  
- Head of “the” → “cats” (determiner)  
- Head of “happy” → “song” (adjective)

Each word has **one head** (except the root).

---

## 🌳 Dependency Trees

Dependency parses form **trees**: hierarchical relationships between words.

```
sing
├── cats (nsubj)
│   └── the (det)
└── song (obj)
    └── a (det)
    └── happy (amod)
```

---

## 🧠 Ambiguity in Syntax

### Prepositional Phrase Attachment
> “Scientists count whales from space.”  
    vs.  
> “Scientists count whales from space.”  

Same words, different parse structures.

### Coordination Scope Ambiguity
> “No heart, cognitive issues.”  
    vs.  
> “No [heart, cognitive] issues.”  

---

## 🧾 Dependency Grammar vs Constituency Grammar

| Grammar Type | Description | Example Corpus |
|---------------|--------------|----------------|
| **Constituency (Phrase Structure)** | Hierarchical phrase composition | Penn Treebank |
| **Dependency Grammar** | Head-dependent relations between words | Universal Dependencies |

**Dependency Grammar** dominates modern NLP — works better for **free word order** languages and multilingual consistency.

---

## 🌐 Universal Dependencies (UD)

A **universal formalism** for cross-lingual syntactic annotation.

Goals:
- Consistent syntactic representation across >100 languages  
- Common tagsets and features  
- Open-source, community-driven project ([universaldependencies.org](https://universaldependencies.org/))

### Key Components
- **Universal PoS tags** (UPOS)  
- **Morphological features**  
- **Dependency relations**

---

## 🧱 CoNLL-U Format

Treebanks distributed in **CoNLL-U** text files.  
Each token occupies one line; each sentence separated by an empty line.

| Column | Description |
|----------|--------------|
| ID | Word index |
| FORM | Token |
| LEMMA | Lemma |
| UPOS | Universal PoS |
| FEATS | Morphological features |
| HEAD | Head word ID |
| DEPREL | Dependency relation |

Example:
```
1   The     the     DET  _  _  2  det
2   cats    cat     NOUN _  _  3  nsubj
3   sing    sing    VERB _  _  0  root
4   .       .       PUNCT _  _  3  punct
```

---

## 🌍 Treebanks and Multilinguality

**Treebanks** = syntactically annotated corpora used to train/evaluate parsers.

| Language | Notable Treebanks |
|-----------|------------------|
| **English** | Penn Treebank, OntoNotes, English Web Treebank |
| **German** | TIGER, TüBa-D/Z, Hamburg Dependency Treebank |

### Universal Dependency Treebanks
- Cover 100+ languages  
- 200+ treebanks (community-maintained)  
- Released regularly via GitHub  

---

## ⚙️ Practical Example – Dependency Parsing with SpaCy

```python
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp("The happy cats sing songs.")

for token in doc:
    print(f"{token.text:10} → head: {token.head.text:10} | dep: {token.dep_}")
```

### Output
```
The        → cats       | det
happy      → cats       | amod
cats       → sing       | nsubj
sing       → sing       | ROOT
songs      → sing       | dobj
.          → sing       | punct
```

---

## 🧩 Summary

| Step | Purpose | Key Challenge | Example Tool |
|-------|-----------|----------------|---------------|
| Sentence Splitting | Divide text into sentences | Abbreviations, punctuation | SegTok, SpaCy |
| Tokenization | Split into tokens | Apostrophes, compounds | NLTK, SpaCy |
| PoS Tagging | Label word categories | Ambiguity | Flair, SpaCy |
| Lemmatization | Normalize to dictionary form | Irregular forms | SpaCy, WordNetLemmatizer |
| Dependency Parsing | Model syntax tree | Ambiguity, complexity | SpaCy, Stanza |

**Takeaway:**  
> The classic NLP pipeline builds structured linguistic understanding from raw text — the foundation of all modern NLP systems.

---

📘 **End of Lecture 5 – The Classic NLP Pipeline**
