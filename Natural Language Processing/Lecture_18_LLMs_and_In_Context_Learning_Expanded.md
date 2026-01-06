# Lecture 18 – Large Language Models & In-Context Learning
#nlp #llm #transformers #in-context-learning #knowledge-probing

---

## 1. Big Picture: Why This Lecture Matters

This lecture explains **why modern NLP works so well**.

Before Transformers:
- Models were **task-specific**
- Knowledge was stored in **databases or graphs**
- Learning required **explicit supervision**

Now:
- A *single* model can translate, answer questions, and reason
- Knowledge is stored **implicitly** in model weights
- Learning can happen **inside the prompt**

> **Core question of the lecture:**  
> *What happens if we scale language models far enough?*

---

## 2. Recap: Fine-Tuning Era (Pre-LLMs)

### Standard Pipeline (≈2019)
1. Take a **pre-trained Transformer**
2. Add a small prediction head
3. Fine-tune on a downstream task

Why this worked:
- Pre-training learns **general language structure**
- Fine-tuning adapts to **specific tasks**

Limitations:
- One model per task
- Requires labeled data
- Expensive to maintain

---

## 3. Language Modeling Objectives (Very Important)

### 3.1 Masked Language Modeling (BERT-style)
> Fill the Gap

**What it is**
- Random tokens replaced with `[MASK]`
- Model predicts missing tokens using *both directions*

Example:
```
The capital of France is [MASK].
```

**Why this is powerful**
- Model uses *full sentence context*
- Great for understanding relationships

**But…**
- `[MASK]` never appears at test time
- Cannot generate fluent text
- Limited to vocabulary subtokens

> ⚠️ Think of MLM as *fill-in-the-blank comprehension*.

---

### 3.2 Causal Language Modeling (GPT-style)
>predict the next token. so how does this sentence continue

**What it is**
- Predict the **next token**
- Only sees the *past*, never the future

Formula intuition:
```
P(sentence) = P(w1) · P(w2|w1) · P(w3|w1,w2) · ...
```

**Why this matters**
- Enables text generation
- Matches how humans write
- Works naturally with prompts

> 💡 Causal LMs are **completion machines**, not QA systems by default.

---

## 4. Why Scaling Language Models Works

### The Surprising Insight
Predicting the next word requires:
- Grammar
- Semantics
- Facts
- Common sense
- World knowledge

Example:
```
Albert Einstein was born in ___
```
To predict correctly, the model must *know the fact*. Or better: also know the context of the sentence (What does it mean)
### Scaling Hypothesis
If we increase:
- Model size
- Training data
- Compute

→ The model **implicitly learns knowledge**

This leads to two landmark papers:
- *Language Models as Knowledge Bases*
- *Language Models are Few-Shot Learners*

---

## 5. Language Models as Knowledge Bases (Paper) 📃

### Traditional Knowledge Graphs
- Nodes = entities
- Edges = relations
- Example: Wikidata
![[Pasted image 20260106112330.png]]
> NLP Tasks for this: Information Extraction, Entity linking ... Maybe we don't need it. We could use a Language model

➕ Language Model is easy
➖The Answers in a language Model is based in probability. In a knowledge Graph we put the information ourself so we know what we can get
➖ We cannot just go the the LM and say __"Change that info"__

Problems:
- Manual schema design
- Hard to extend
- Expensive to maintain

### Key Research Question
> Do language models store factual knowledge *without explicit structure*?

If yes:
- We could **query LMs instead of databases**
- No schema needed
- Open-ended knowledge

---

## 6. LAMA Probe (Knowledge Probing)

### Idea
Convert facts into **close questions**.

Check if the LM knows a fact or not. Then you can easily check if the LM knows a fact or not

Structured fact:
```
(France, capital, Paris)
```

Close:
```
The capital of France is [MASK].
```

If LM predicts *Paris* → success. ✅

Do it for a lot of facts

### How Evaluation Works
- Thousands of facts
- Precision@1 metric
- Compared across models

- Use Relation Extraction to build a knowledge graph out of the LM knowledge 
- Use different Data sources

### Key Result
- BERT-large performs surprisingly well
- Sometimes rivals classical KB (knowlede base) systems
![[Pasted image 20260106113736.png]]

- Regular relation extraction is super bad
	- but if added with oracle it is somehow OKish

> 💡 This was the first strong evidence that **LMs store factual knowledge**.

---

## 7. Why LAMA Is Problematic

### Core Limitations
- Only **single-token answers** single-sub-token answers
- Only **masked LMs** only predicting masked tokens
- Strong **answer bias** 
- Vocabulary mismatch across models

Example bias:
```
Most places are located on which continent?
→ Antarctica (72% in LAMA)
```
Because the knowledge is from Wikipedia and a lot of Island articles are in Antarctica

![[Pasted image 20260106114449.png]]
### Deeper Issue
Some questions:
- Leak the answer
- Have multiple correct answers
- Distort results

> ⚠️ LAMA measures *something*, but not cleanly factual knowledge.

---

## 8. BEAR Probe (Improved Evaluation)

### Key Idea
Reformulate probing as **multiple choice**.

Instead of:
```
The capital of Uganda is [MASK].
```

Use:
```
The capital of Uganda is Kampala.
The capital of Uganda is Thimphu.
The capital of Uganda is Buenos Aires.
...
```

The model:
- Computes **log-likelihood** for each sentence
- Chooses the most probable one
![[Pasted image 20260106114830.png]]
### Why This Is Better
- Works for *any* LM
- No subtoken restriction
- Reduces bias
- More realistic reasoning

> 💡 BEAR evaluates **sentence plausibility**, not token guessing.

---

## 9. Log-Likelihood Intuition

### Causal LMs
- Sentence probability = product of next-token probabilities
- Longer sentences → lower raw probability
- Must normalize properly

### Masked LMs
- Estimate token likelihood using context
- Less natural for generation
- Still usable for BEAR-style scoring

---

## 10. BEAR Results & Scaling Laws

### Observations
- Larger models usually perform better
- But not always strictly monotonic
- Architecture and data quality matter

Important takeaway:
> **Scale helps, but it’s not the only factor.**

---

## 11. Training Large Language Models

### Data Strategy
- Start with massive web data
- Filter aggressively
- Mix high-quality sources

Key principle:
> **Quality > Quantity**

### Data Mixing
- Small datasets (Wikipedia) seen more often
- Large datasets down-weighted

---

## 12. Evaluation Paradigms

### Supervised Fine-Tuning
- Update all weights
- Task-specific
- Strong but inflexible

### In-Context Learning (ICL)
- No weight updates
- Learning happens in the **prompt**
- Same model, different behavior

---

## 13. In-Context Learning Types


We no longer use ML for the LM to learn but we use prompts (control the behaviour using the prompts)
### Zero-Shot
- Only task description
- Weakest performance

### One-Shot
- One example
- Strong improvement

### Few-Shot
- Multiple examples
- Best performance

![[Pasted image 20260106122115.png]]

> 💡 Prompt examples act like **temporary training data**.

---

## 14. GPT-3: Few-Shot Learning

Main findings:
- Same model
- No fine-tuning
- Competitive with SOTA

Conclusion:
> **Large models can adapt on the fly.**

---

## 15. Limitations of In-Context Learning

- Hard to describe tasks precisely
- Output format ambiguity
- Models trained to *continue text*, not follow commands

→ Leads to **instruction tuning**

---

## 16. Mental Model to Remember

- LMs are **probabilistic text continuers**
- Knowledge is **distributed**, not symbolic
- Prompts = *soft programs*
- Scaling enables emergent behavior

---

## 17. Exam & Learning Tips 🧠

### Understand Deeply
- Why next-token prediction leads to knowledge
- Why probing is difficult
- Why scale changes behavior

### Be Able to Explain
- LAMA vs BEAR (motivation!)
- Fine-tuning vs ICL
- Zero-shot vs Few-shot

### Active Learning
- Rewrite prompts yourself
- Predict LM behavior
- Explain concepts aloud

---

## 18. One-Sentence Summary

> **Large Language Models learn knowledge implicitly through next-token prediction, and scaling enables them to reason, adapt, and learn directly from prompts.**
