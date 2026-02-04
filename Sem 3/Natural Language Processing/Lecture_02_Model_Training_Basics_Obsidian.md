# Lecture 2 – Model Training Basics 🧠⚙️
#nlp #deep-learning #training #sgd #loss #backprop

> Obsidian-friendly notes with **extra intuition, explanations, and emojis ✨** to make model training really stick.

---

## 1. What Does “Training a Model” Mean? 🤔

Training a neural network means:

> **Automatically learning weights and biases so inputs map to correct outputs.**

In NLP:
- Text → vectors 🔢
- Vectors → predictions 📊

Think of training as tuning knobs 🎛️ until predictions look right.

---

## 2. Running Example: Sentiment Analysis 😊😡

Task:
- Input: movie review
- Output: POSITIVE or NEGATIVE

This is:
- Binary classification
- Supervised learning

---

## 3. ML as Vector Transformation 🔁

Core formula:
```
ŷ = φ(Wx + b)
```

- W = weights
- b = bias
- φ = activation

Everything is linear algebra + non-linearity ✨

---

## 4. Learnable Parameters 🎯

The model learns only:
- Weights
- Biases

⚠️ Bias is crucial – without it, many problems are unsolvable.

---

## 5. Forward Pass ➡️

- Input flows through network
- Prediction is produced

Example:
```
great just great!
→ [0.99, 0.01] → POSITIVE
```

---

## 6. Training vs Evaluation 🎓🧪

- Training set → learn parameters
- Validation set → tune hyperparameters
- Test set → final evaluation

Never train on test data 🚨

---

## 7. Loss Function 📉

Loss measures:
> How wrong the model is

High loss 😬  
Low loss 😎

---

## 8. Loss for Regression 📐

Mean Squared Error (MSE):
```
(ŷ − y)²
```

Large errors are punished strongly.

---

## 9. Loss for Classification 🎯

Cross-Entropy Loss:
- Looks at probability of true class
- Confident mistakes hurt a lot 😵

---

## 10. Stochastic Gradient Descent (SGD) 🏃‍♂️

Training loop:
1. Forward pass
2. Compute loss
3. Backward pass (gradients)
4. Update parameters

Repeat 🔁

---

## 11. Gradients ⛰️

Gradient tells direction of steepest loss increase.

- Positive → decrease weight
- Negative → increase weight

---

## 12. Loss Landscape 🗺️

Loss is a surface:
- Valleys = good solutions
- Hills = bad solutions

Gradients give local direction only.

---

## 13. Learning Rate 👣

Most important hyperparameter ⚠️

- Too big → divergence 💥
- Too small → slow 🐌

---

## 14. Mini-Batches 📦

Small batch:
- Noisy updates
- Better generalization

Large batch:
- Smooth updates
- Faster

---

## 15. Epochs ⏱️

One epoch = seeing all training data once.

Too many → overfitting 😬  
Too few → underfitting 😕

---

## 16. Loss Curves 📈

Healthy:
- Training ↓
- Validation ↓

Overfitting:
- Training ↓
- Validation ↑

---

## 17. Deep Neural Networks 🧬

Multiple layers + activations.

More expressive 💪  
Harder to train 😅

---

## 18. Activation Functions ⚡

Why needed?
- Without them → linear model only

Popular:
- ReLU 🚀
- Sigmoid 😴

---

## 19. Key Mental Model 🧠

- Forward = predict
- Loss = error
- Backward = blame
- SGD = gradual improvement

---

## 20. One-Sentence Summary 🧾

> Training a neural network means minimizing a loss function with gradient-based optimization so it generalizes to unseen data.
