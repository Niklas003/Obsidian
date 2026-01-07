# Lecture 9 — The Transformer  
Comprehensive Obsidian Notes with Explanations

---
## 0. Recap - What have we RNN's used for
- Sequence Labelling
- Text Classification
- Sequence to Sequence
## 1. Limitations of RNNs

### ❗ Why Replace RNNs?
RNNs process sequences step‑by‑step, creating several bottlenecks:

### **1.1 Unparallelizable Operations**
- Each hidden state depends on the previous one → cannot compute all steps at once.
	- we have to compute the hidden states one by one
- GPUs excel at parallel computation, so RNNs **underuse** hardware. bc. we do in sequentially
- Long sequences cause very slow training.

### **1.2 Unidirectionality**
- Standard RNNs only propagate information in one direction.
- Even bidirectional RNNs aren’t *deeply* bidirectional → they don’t allow rich interactions across
	- in the end we just have two RNN's
- the full sequence at every layer.
- very limited in their direction -> only one direction per RNN

### **1.3 Linear Interaction Distance**
- For word A to influence word B, whose distance is *k*, information requires *k* steps.
- Leads to difficulty learning long‑range dependencies (vanishing gradients).
- the hidden states getting overwritten at each timestep
	- a solution for this would be #attention

---

## 2. #Attention in Sequence‑to‑Sequence Models

### ❗ The Information Bottleneck Problem
In standard Seq2Seq:
- The entire input sentence must be encoded into **one** vector.
- Hard for long or complex sentences → leads to poor translations.

### **2.1 Attention Mechanism**
Instead of compressing everything:
- At each decoding step, the model looks back (“attends”) to all encoder states.
- Gives a **soft alignment** between input and output words.
- Dramatically improves translation, especially for long sentences.

**Key Idea**  
Each encoder hidden state becomes:
- **Key (K)**: What this position *offers*
- **Value (V)**: The actual information
- **Query (Q)**: What the decoder *is looking for*

Attention computes:  
$$
	ext{Attention}(Q,K,V) = \mathrm{softmax}(QK^T)V
$$
> The question is not do we need a replacement for RNN's. But more do we need a replacement for RNN + Attention.

---

## 3. Self‑Attention

### ❗ What is Self‑Attention?
Attention, but within the same sequence:
- Each word attends to *all other words* in the sentence. (including the own word)
- Produces contextualized embeddings.

- Take embedding vectors 
- Compute Attention

## Query, Key and Value Maps

- Three linear layers to transform hidden state into keys, queries and values
- In each layer we have different linear transformation for Q _(uery)_ , K _(ey)_ , and V _(alue)_

### **Advantages Over RNNs**
- **O(1) interaction distance** → any position can access any other instantly.
- **Fully parallelizable**
- **Deep bidirectionality**

Example:  
The word *"chef"* can consider *"who"* or *"was"* directly in one layer.

---

## 4. Positional Encodings

### ❗ Problem
Self‑attention treats input as a bag‑of‑words → no word order. 
- we lost the sequential information

### **Solution: Positional Encodings**
Add a vector to each input that encodes position.

Two common types:
1. **Learned positional embeddings**
2. **Sinusoidal positional encodings** (can extrapolate to longer sequences)

---

## 5. Feed‑Forward Networks (FFN)

After each self‑attention layer:
- Apply a position‑wise FFN:  
  $$
  	ext{FFN}(x) = W_2(	ext{ReLU}(W_1 x + b_1)) + b_2
  $$
- Provides nonlinearity → essential for modeling power.

---

## 6. Transformer Architecture

### **6.1 Encoder**
Each encoder layer contains:
1. Multi‑head self‑attention  
2. Feed‑forward network  
3. Add & Norm residual connections  

### **6.2 Decoder**
Each decoder layer contains:
1. **Masked self‑attention** (prevents peeking ahead)
2. **Cross‑attention** (attends to encoder)
3. FFN
4. Add & Norm

### **Why Masking?**
Prevents cheating during training → ensures autoregressive generation.

![[Pasted image 20260106180219.png]]

---

## 7. Multi‑Head Attention (MHA)

### ❗ Why Multiple Heads?
Each head learns different relationships:
- One head may track grammar
- Another may track semantic similarity
- Another may track long‑distance dependencies

**Implementation**  
Just run several attention heads in parallel and concatenate outputs.

---

## 8. Training Improvements

### **Residual Connections**
- Solve vanishing gradient issues  
- Help training deeper models

### **Layer Normalization**
- Stabilizes training  
- Normalizes each layer’s activations  

---

## 9. Results & Impact

- Transformers significantly outperform RNNs + attention.
- Became state‑of‑the‑art in machine translation.
- Foundation for modern LLMs including BERT, GPT, T5, etc.

---

## 10. Summary

✔ RNNs too slow and weak for modeling long sequences  
✔ Attention removes bottlenecks  
✔ Self‑attention enables full parallelization and deep context modeling  
✔ Transformers dominate NLP because they scale extremely well  


![[Q15-1016.pdf]]