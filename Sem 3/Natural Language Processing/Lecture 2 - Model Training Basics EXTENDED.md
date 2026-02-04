# Lecture 2 – Model Training Basics 🧠⚙️
#nlp #deep-learning #training #sgd #loss #gradients #backprop

> 📘 **Obsidian notes based directly on Lecture 2 slides**,  
> extended with intuition, examples, exam hints, and emojis 😄

---

## 1. Problem Setup: Sentiment Analysis 🎬😊😡

**Task:**
- Input: movie review text
- Output: POSITIVE or NEGATIVE
- Binary classification

Text must be converted to numbers 🔢 before learning.

---

## 2. Machine Learning as Vector Transformation 🔁

ML maps an input vector to an output vector:

```
ŷ = W x + b
```

Everything starts with linear algebra ✨.

---

## 3. One-Layer Neural Network 🧩

Components:
- Weight matrix W
- Bias b
- Activation ϕ

Bias is crucial – without it many problems are unsolvable ⚠️.

---

## 4. Learnable Parameters 🎯

Only weights and biases are learned.
Training = finding good numerical values.

---

## 5. Forward Pass ➡️

Input → layers → logits → probabilities.

Model makes a guess 🎯.

---

## 6. Training vs Evaluation 🎓🧪

- Training set: learn weights
- Validation set: tune hyperparameters
- Test set: final evaluation

Never train on test data 🚨.

---

## 7. Stochastic Gradient Descent (SGD) 🏃‍♂️

Training loop:
1. Forward pass
2. Compute loss
3. Backward pass
4. Update parameters

Repeat 🔁.

---

## 8. Loss Function 📉

Loss measures how wrong a prediction is.
Lower loss = better model 😎.

---

## 9. Loss for Regression 📐

Mean Squared Error:
```
(ŷ − y)²
```

Large errors are punished strongly.

---

## 10. Loss for Classification 🎯

Cross-Entropy Loss:
- Looks at probability of true class
- Confident mistakes hurt 😵

---

## 11. Loss Landscape 🗺️

Loss depends on all parameters.
Goal: find a low valley ⛰️.

---

## 12. Gradients ⛰️

Gradient = slope of loss.
- Positive → decrease parameter
- Negative → increase parameter

---

## 13. Backpropagation 🔙

Chain rule computes gradients for all parameters.

---

## 14. Hyperparameters ⚙️

- Learning rate 👣
- Mini-batch size 📦
- Epochs ⏱️

Chosen by you, not learned.

---

## 15. Learning Rate 🚨

Too big → divergence 💥  
Too small → slow 🐌.

---

## 16. Mini-Batches 📦

Small batch:
- Noisy but generalizes well

Large batch:
- Smooth but less robust

---

## 17. Epochs & Early Stopping ⏱️🛑

Stop when validation loss stops improving.

---

## 18. Loss Curves 📈

Training ↓ and validation ↓ → good  
Training ↓ and validation ↑ → overfitting

---

## 19. Deep Neural Networks 🧬

Multiple layers = more expressive models.
Harder optimization.

---

## 20. Activation Functions ⚡

ReLU 🚀 is default.
Sigmoid 😴 is outdated.

---

## 21. Key Mental Model 🧠

Forward = predict  
Loss = error  
Backward = blame  
SGD = improvement

---

## 22. Exam Tip 🎓

If you can explain SGD and cross-entropy in words, you’re good 💡.

---

## 23. One-Sentence Summary 🧾

> Training minimizes loss via gradients so parameters generalize to new data.
