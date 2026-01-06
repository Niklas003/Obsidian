### Lecture 7: Language Modeling

**Professor:** Alan Akbik  
**Course:** Deep Learning and Natural Language Processing

---

#### 1. What is a Language Model?

A **language model (LM)** predicts the probability of the next word given previous words in a sequence:

$$  P(w_t | w_1, w_2, …, w_{t-1})  $$

It assigns high probability to natural, grammatical sentences and low probability to unlikely ones.

**Applications:**

- Text generation
    
- Machine translation
    
- Speech recognition
    
- Autocomplete / next-word prediction
    
- Spelling correction
    

---

#### 2. Sentence Probability

The probability of an entire sentence is computed using the chain rule:

$$  
P(w_1, …, w_T) = \prod_{t=1}^{T} P(w_t | w_1, …, w_{t-1})  
$$

This means the probability of each word depends on its context.

---

#### 3. N-Gram Models

An **n-gram model** simplifies this by assuming that a word depends only on the last _n–1_ words.

Examples:

- Unigram: P(w_t)
    
- Bigram: P(w_t | w_{t–1})
    
- Trigram: P(w_t | w_{t–2}, w_{t–1})
    

To estimate probabilities, count frequencies from a corpus:

$$  
P(w_t | w_{t–2}, w_{t–1}) = \frac{C(w_{t–2}, w_{t–1}, w_t)}{C(w_{t–2}, w_{t–1})}  
$$

---

#### 4. Perplexity

**Perplexity** measures how well a model predicts unseen data:

$$  
PP = \exp\left(-\frac{1}{T} \sum_t \log P(w_t | w_{<t})\right)  
$$

Lower perplexity = better model.

---

#### 5. Problems with N-Grams

- **Data sparsity:** many word combinations never appear in training
    
- **Fixed context:** can’t model long dependencies
    
- **Vocabulary explosion:** too many parameters for large vocabularies
    

These motivate **neural language models**.

**Limitations:**
	- limited by the training data
	- would  ot work good with long text sequences

---

#### 6. Neural Language Models (Bengio et al., 2003)

Neural models represent words as **embeddings** and use a **feed-forward neural network** to predict the next word.

- Input: embeddings of previous words
    
- Hidden layer: non-linear combination of context
    
- Output: softmax over the vocabulary
    

This allows generalization — similar contexts produce similar predictions.

---

#### 7. RNN-Based Language Models

Feedforward networks only look at a fixed context window.  
**Recurrent Neural Networks (RNNs)** process sequences word by word and retain a **hidden state** that encodes previous information.

At each time step:  
$$  
h_t = f(W_{xh}x_t + W_{hh}h_{t-1})  
$$  
$$  
P(w_t | w_{<t}) = \text{softmax}(W_{hy}h_t)  
$$

This allows the model to capture longer dependencies in text.

---

#### 8. Text Generation

After training, an RNN language model can **generate text** by:

1. Starting with a seed word or sequence.
    
2. Predicting the next word’s probability distribution.
    
3. Sampling from it (optionally adjusting randomness using **temperature**).
    
4. Repeating to form sentences.
    

**Temperature:**

- Low (<1.0): more deterministic and repetitive.
    
- High (>1.0): more diverse and creative.
    

---

#### 9. Units of Modeling

Different LMs operate at different levels:

- **Word-level:** simplest, but large vocabularies
    
- **Subword-level:** balances flexibility and efficiency (e.g., BPE, SentencePiece)
    
- **Character-level:** handles any input but requires long sequences
    
- **Byte-level:** universal representation, used in GPT models
    

---

#### 10. Evaluating Models

The standard evaluation metric is **perplexity**, which measures how surprised the model is by test data.  
A lower perplexity indicates a better, more confident model.

---

#### 11. Comparison of Models

|Model|Context|Advantages|Disadvantages|
|---|---|---|---|
|N-Gram|Fixed window|Simple, interpretable|Sparse, limited memory|
|Neural (Feedforward)|Fixed window|Learns embeddings|Still limited context|
|RNN|Variable|Handles long dependencies|Sequential, harder to train|

---

#### 12. From RNNs to Transformers

RNNs process tokens sequentially, which is slow and difficult to parallelize.  
**Transformers** replace recurrence with **self-attention**, allowing parallel processing and modeling global dependencies.  
Modern models like **GPT** and **BERT** build on this evolution.

---

#### 13. Key Takeaways

- Language modeling = predicting the next token.
    
- Perplexity is the main evaluation metric.
    
- N-Gram → Neural → RNN → Transformer is the evolutionary path.
    
- RNN-based models bridge traditional statistical models and modern Transformers.
    

---

**End of Lecture 7 – Language Modeling**

---

Would you like me to summarize Lecture 8 (likely about “Sequence-to-Sequence Models” or “Attention”) next in the same format?