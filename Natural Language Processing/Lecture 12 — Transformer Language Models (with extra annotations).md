![[Lecture 12_ Transformer Language Models - no Notes.pdf]]

_Deep Learning and Natural Language Processing — Prof. Dr. Alan Akbik_  
**Topic:** Transfer Learning, GPT, BERT, Fine-Tuning  
**Tags:** #NLP #Transformers #GPT #BERT #TransferLearning #LanguageModeling

---

## **1. Why Transfer Learning Matters**

Modern NLP models no longer train from scratch.  
Instead, they **start from pre-trained language models** that already encode:

- syntax
- semantics
- world knowledge

This drastically reduces labeled data requirements.

**Key idea:**  
You first train on a _huge_ unsupervised text corpus, then _fine-tune_ for a specific task.

---

## **2. Word Embeddings → Contextual Embeddings**

Old approach:

- Word2Vec, GloVe (General Language Understanding...)
- Each word = 1 fixed vector
- "bank" always has one vector → fails for polysemy
    

Limitations:

- Not contextual
- No sentence-level meaning
- Not enough for complicated tasks like NLI

Transformers solve this:

- Every token gets a **context-dependent vector**.
---

## **3. Natural Language Inference (NLI)**

Given **premise** + **hypothesis**, classify:

- entailment
- contradiction
- neutral

Example (Winograd style):

- Premise: _The trophy doesn’t fit into the suitcase._
- Hypothesis: _The trophy is too large._ → entailment

NLI is harder than sentiment because:

- Requires _world knowledge_
- Requires _reasoning_    
- Cannot be solved by simple keywords

- Is Similar to Sentiment Classification
- But here we have two Inputs and one of 3 Output Classes
- (positive/neutral/negative)
---

## **4. Architectures for NLI**

### **Old: Dual Encoder (2018 style)**

Encode premise and hypothesis separately → combine.  
Problem: no cross-sentence interaction.

- Premise encoder 
- Hypothesis encoder
- cat both output vectors
- then softmax classifier

> Also called **cross encoder**
#### Problem
- Both encoders act too independently
- 
### **Modern: Single Sequence Input**

`premise [SEP] hypothesis`  
Add `[CLS]`, use its final hidden state for classification.
-  Make asindgle string out of string and hypothesis
-  Place special seperator token
Allows:

- Cross-attention between sentences
- Richer interactions
- Better performance (especially with transformers)

---

## **5. Transfer Learning Pipeline -- super Important** 

>Idea: we do not want to start from scratch. Use the existing training data to learn new skills. Use a network that is already existend

1. **Pre-train** on a general text prediction task
2. **Load model** for new task
3. **Attach classification head**
4. **Fine-tune** with small LR, few epochs

>We use training data for new task to slightly modyfiy weights of pre-trained model

### How similiar should the tasks be?
- the similar they are the better they work

---

## **6. Pre-Training Tasks in NLP**

![[Pasted image 20251205115348.png]]
We need tasks that are:

- Hard
- Require full sentence understanding
- Have unlimited training data

Answer: **Language Modeling** - the task of predicting what comes next

---
## **LSTM**

![[Pasted image 20251205115731.png]]

---
## **7. Causal Language Modeling (GPT)**

GPT uses **decoder-only transformer** with **causal masking**:

- Each token attends only to previous tokens
- Predict next token:  
$$
    P(w_t | w_{<t})  
    $$

### **GPT Architecture**

- Only the _decoder_ blocks
- Masked self-attention
- Excellent for text generation

### **GPT-1**
- 12 layers
- 768 hidden size
- 12 heads
- Trained on BookCorpus -- 7000 unique books

### **GPT-2**

- 1.5B parameters
- Produces fluent text
- Shows emergent behavior (zero-shot abilities)

---

## **8. GPT for Downstream Tasks (Fine-Tuning)**

Procedure:

- Feed `premise [SEP] hypothesis` into the decoder
- Add classifier head
- Fine-tune entire model

GPT achieved **state-of-the-art** results on NLI at the time.

---

## **9. Masked Language Modeling (BERT)**

BERT uses **encoder-only transformer** with full bidirectional attention.

### **Why not causal LM?**

Causal LM only sees the left context → cannot fully exploit bidirectionality.

BERT’s solution:

- Mask random tokens (15%)
- Predict them
- Allows full left-right context

### **Masking strategy (important!)**

Why use making: because the model should not look at future words
Of the masked tokens:

- 80% → replace with `[MASK]`
- 10% → replace with a random token
- 10% → keep unchanged

Why?  
So model can’t rely on always seeing `[MASK]` during training.

---

## **10. Next Sentence Prediction (NSP)**

BERT also predicts whether sentence B follows sentence A.  
Helps with tasks involving sentence relations (e.g., NLI).

Examples:

- _the duck sang_ → _it sounded beautiful_ → TRUE
- _the duck sang_ → _I poured water_ → FALSE

---

## **11. Fine-Tuning BERT**

Steps:

1. Add classification head on top of `[CLS]`
2. Fine-tune entire model
3. Use small learning rate (AdamW)
4. 2–4 epochs

Result:

- #BERT dominated GLUE benchmark
- Became the standard model for NLP    

---

## **12. BERT Model Sizes**

- **BERT-base:**  
    12 layers, 768 hidden dims, 12 heads → 110M params

- **BERT-large:**  
    24 layers, 1024 hidden dims, 16 heads → 340M params

Training data:
- BooksCorpus (800M words)
- Wikipedia (2.5B words)

---

## **13. Huggingface Transformers**

Transformer models made easily accessible:

- #BERT
- GPT-2
- RoBERTa
- T5
- DistilBERT

You do **not** need to pre-train transformers — only fine-tune them.

---

## **14. Training vs Fine-Funing**

### **Training from scratch**

- Random initialization
- Large LR
- Many epochs
- Huge labeled dataset
- Computationally expensive

### **Fine-tuning**

- Pretrained model
- Small LR
- Few epochs
- Works with small datasets

Fine-tuning = small “task-specific adjustment”.

---

## **15. Key Takeaways**

- Transformers revolutionized transfer learning with GPT + BERT.
- GPT = causal LM (decoder-only) → great for generation.
- #BERT = masked LM (encoder-only) → great for understanding.
- Fine-tuning pre-trained transformers beats training from scratch.
- Huggingface makes it accessible to everyone.