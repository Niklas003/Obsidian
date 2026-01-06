# 🧠 Lecture 6 – Recurrent Neural Networks (RNNs)

**Course:** Deep Learning and Natural Language Processing  
**Lecturer:** Prof. Dr. Alan Akbik  
**Topic:** Sequential Models – RNNs, LSTMs, and BiLSTMs  
**Tags:** #NLP #DeepLearning #RNN #LSTM #BiLSTM #SequenceModeling #PyTorch

---

## 🧩 Motivation: From Classic NLP to Deep Learning

In previous lectures, we built models that treated words **independently** (e.g., PoS taggers with context windows).  
However, **language is sequential** — the meaning of a word often depends on what comes before or after it.

Examples:

- “The bank raised interest rates.” → _bank = financial institution_
    
- “He sat on the bank of the river.” → _bank = riverside_
    

➡️ We need **models that handle sequential dependencies**.

---

## 🧭 Sequential Data and Tasks

### Sequential Inputs

Data where **order matters**:

- Text (words, characters)
    
- Speech (acoustic frames)
    
- Time series (stock prices, EEG signals)
    

### Sequential Tasks in NLP

|Task|Input|Output|
|---|---|---|
|**Sequence Labeling**|Word sequence|Label per token (e.g., PoS tagging, NER)|
|**Sequence Classification**|Word sequence|Single label (e.g., sentiment)|
|**Sequence Generation**|Word sequence|Output sequence (e.g., translation, summarization)|

---

## 🧠 Feedforward Networks vs RNNs

### Feedforward Network Limitation

A feedforward network assumes **fixed-size inputs** and **no notion of sequence**.

Example:  
You can encode context using a fixed window (e.g., 3-gram), but **it doesn’t generalize to longer contexts**.

### Need for Recurrence

We want the model to:

- Process variable-length sequences
    
- Retain information about previous inputs
    

➡️ Introduce **Recurrent Neural Networks (RNNs)**.

---

## 🔁 Recurrent Neural Networks (RNNs)

### Intuition

An RNN processes one input at a time while maintaining a **hidden state** that carries information from previous steps.

Formally:

$$ 
ht=f(Wxhxt+Whhht−1+bh)
h_t = f(W_{xh}x_t + W_{hh}h_{t-1} + b_h)
ht​=f(Wxh​xt​+Whh​ht−1​+bh​) 
yt=Whyht+byy_t = W_{hy}h_t + b_yyt​=Why​ht​+by 
$$​

Where:
$$
xtx_txt​: input at time _t_
hth_tht​: hidden state at time _t_
yty_tyt​: output at time _t_
Wxh,Whh,WhyW_{xh}, W_{hh}, W_{hy}Wxh​,Whh​,Why​: weight matrices
$$
### Diagram (text form)

`x1 → [h1] → y1       ↑ x2 → [h2] → y2       ↑ x3 → [h3] → y3`

Each hidden state receives input from both **xₜ** and **hₜ₋₁**.

---

## ⚙️ RNN Forward Computation

`import torch import torch.nn as nn  rnn = nn.RNN(input_size=10, hidden_size=20, batch_first=True) x = torch.randn(5, 3, 10)   # batch=5, sequence_len=3, input_dim=10 out, h_n = rnn(x)  print(out.shape)  # (5, 3, 20) - output for each time step print(h_n.shape)  # (1, 5, 20) - final hidden state`

- **out** → sequence of hidden states (for tagging tasks)
    
- **hₙ** → final hidden state (for classification)
    

---

## 🧱 Sequence Classification with RNNs

To classify an entire sequence (e.g. sentiment analysis):

- Feed a sequence of embeddings into the RNN
    
- Use the **last hidden state** as sentence representation
    


```python
class RNNClassifier(nn.Module):     
	def __init__(self, vocab_size, embed_dim, hidden_dim, num_classes):                super().__init__()         
	self.embedding = nn.Embedding(vocab_size, embed_dim)         
	self.rnn = nn.RNN(embed_dim, hidden_dim, batch_first=True)         
	self.fc = nn.Linear(hidden_dim, num_classes)
	          
def forward(self, x):         
	x = self.embedding(x)        
	 _, h_n = self.rnn(x)         
	 return self.fc(h_n.squeeze(0))`
```

---

## 🧩 Backpropagation Through Time (BPTT)

RNNs share parameters across time steps — gradients must be **backpropagated through all steps**.

### Problem: Vanishing & Exploding Gradients

- Long sequences → gradients shrink or blow up exponentially
    
- Network forgets long-term dependencies
    

**Solutions:**

1. Gradient clipping (to prevent explosion)
    
2. Specialized architectures (LSTM, GRU)
    

---

## ⚠️ The Vanishing Gradient Problem

The derivative of the activation function (e.g., tanh, sigmoid) is < 1.  
Repeated multiplication across time steps causes gradients → 0.

Effect:

- RNN remembers only **recent** information
    
- Fails on **long-range dependencies**
    

---

## 🧠 Long Short-Term Memory (LSTM)

_Hochreiter & Schmidhuber (1997)_

LSTMs solve vanishing gradients using **gates** to regulate information flow.

Each LSTM cell maintains:

- **Hidden state (hₜ)** → short-term memory
    
- **Cell state (cₜ)** → long-term memory
	- element wise multiplication e.g. forget a bit, a lot etc. je nachdem was der output vector aus der sigmoid function für values hat -> sigmoid vector hat values zw. 0 und 1

---

## ⚙️ LSTM Cell Computation

At each time step:

ft=σ(Wf[ht−1,xt]+bf)(forget gate)f_t = σ(W_f [h_{t-1}, x_t] + b_f) \quad \text{(forget gate)}ft​=σ(Wf​[ht−1​,xt​]+bf​)(forget gate) it=σ(Wi[ht−1,xt]+bi)(input gate)i_t = σ(W_i [h_{t-1}, x_t] + b_i) \quad \text{(input gate)}it​=σ(Wi​[ht−1​,xt​]+bi​)(input gate) c~t=tanh⁡(Wc[ht−1,xt]+bc)(candidate state)\tilde{c}_t = \tanh(W_c [h_{t-1}, x_t] + b_c) \quad \text{(candidate state)}c~t​=tanh(Wc​[ht−1​,xt​]+bc​)(candidate state) ct=ft∗ct−1+it∗c~tc_t = f_t * c_{t-1} + i_t * \tilde{c}_tct​=ft​∗ct−1​+it​∗c~t​ ot=σ(Wo[ht−1,xt]+bo)o_t = σ(W_o [h_{t-1}, x_t] + b_o)ot​=σ(Wo​[ht−1​,xt​]+bo​) ht=ot∗tanh⁡(ct)h_t = o_t * \tanh(c_t)ht​=ot​∗tanh(ct​)

---

### Explanation of Gates

|Gate|Role|Analogy|
|---|---|---|
|Forget Gate|Decides what to discard from memory|“Forget irrelevant past”|
|Input Gate|Decides what to store|“Add new info”|
|Output Gate|Controls what to expose|“Expose relevant memory”|

---

## 🧮 LSTM in PyTorch

```python
import torch import torch.nn as nn  

lstm = nn.LSTM(input_size=10, hidden_size=20, batch_first=True) 
x = torch.randn(5, 3, 10) out, (h_n, c_n) = lstm(x)  
print(out.shape)  # (5, 3, 20) print(h_n.shape)  # (1, 5, 20)`
```

---

## 🔄 Bidirectional LSTMs (BiLSTMs)

Language context comes from both **past** and **future** words.

**Bidirectional LSTMs** process sequences in both directions and concatenate their outputs.

`→ (forward LSTM) ← (backward LSTM) Output = [h_forward; h_backward]`

---

## ⚙️ BiLSTM in PyTorch

```python 
class BiLSTMTagger(nn.Module):     
	def __init__(self, vocab_size, embed_dim, hidden_dim, num_tags):                    super().__init__()         
		self.embedding = nn.Embedding(vocab_size, embed_dim)         
		self.lstm = nn.LSTM(embed_dim, hidden_dim, batch_first=True, bidirectional=True)         
		self.fc = nn.Linear(hidden_dim * 2, num_tags)          
	def forward(self, x):         
		x = self.embedding(x)         
		out, _ = self.lstm(x)         
		out = self.fc(out)         
		return out`
```
---

## 🧠 Intuition Summary

|Model|Captures|Problems|Notes|
|---|---|---|---|
|**Vanilla RNN**|Short-term dependencies|Vanishing gradients|Simple but limited|
|**LSTM**|Long-term dependencies|Computationally heavier|Gating mechanism|
|**BiLSTM**|Both directions|Doubled parameters|Superior context understanding|

---

## ⚡ Applications of RNNs in NLP

|Task|Model|Description|
|---|---|---|
|**PoS Tagging**|BiLSTM|Label per token|
|**NER**|BiLSTM + CRF|Detect named entities|
|**Language Modeling**|LSTM|Predict next word|
|**Machine Translation**|Seq2Seq|Encode-decode sequences|
|**Speech Recognition**|LSTM/GRU|Map audio → text|

---

## 🧱 Summary Table

|Model|Key Mechanism|Pros|Cons|
|---|---|---|---|
|**RNN**|Recurrence|Simple, fast|Vanishing gradients|
|**LSTM**|Memory cell + 3 gates|Handles long dependencies|Complex, slower|
|**GRU**|2 gates|Efficient, simpler|Slightly less expressive|
|**BiLSTM**|Bidirectional|Context from both sides|Doubles parameters|

---

## 🧩 Key Takeaways

- RNNs process **sequential data** with shared weights across time.
    
- LSTMs and GRUs solve **long-term dependency** problems via gating.
    
- BiLSTMs capture **contextual information** from both directions.
    
- Foundation for modern **Transformer** models (replaced recurrence with attention).
    

---

## 📘 **End of Lecture 6 – Recurrent Neural Networks (RNNs)**





