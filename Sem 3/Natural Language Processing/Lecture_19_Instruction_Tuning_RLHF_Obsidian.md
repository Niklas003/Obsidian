# Lecture 19 – Instruction Tuning & RLHF
#nlp #llm #instruction-tuning #rlhf #alignment #transformers

> These notes explain **why GPT-3-style models evolved into ChatGPT-style assistants**.
> Written for **Obsidian** with conceptual depth and exam focus.

---

## 1. Why Instruction Tuning Is Needed

### From Lecture 18
Large Language Models (LLMs):
- learn via next-token prediction
- excel at in-context learning
- improve with scale

But two core issues remained:

### Problem 1: Poor Zero-Shot Performance
Even very large models:
- underperform in zero-shot settings
- rely heavily on examples

Scaling helps, but does not solve this.

---

### Problem 2: No Instruction Following
Pre-trained LMs:
- are not trained to follow commands
- treat instructions as text to continue

They lack an internal concept of *user intent*.

---

## 2. Instruction Tuning (IT)

### Core Concept
Fine-tune a pre-trained LM on:
```
Instruction → Desired Answer
```

Goal:
> Teach the model **how to respond**, not what to know.

---

## 3. FLAN: Fine-tuned LMs Are Zero-Shot Learners

### Method
1. Convert many NLP datasets into natural-language instructions
2. Use multiple prompt templates per task
3. Fine-tune on instruction–output pairs
4. Evaluate on unseen tasks

---

### Why This Works
Instruction tuning:
- does NOT add new knowledge
- improves *expression* of existing knowledge
- reduces zero-shot vs few-shot gap

Prompt diversity is critical.

---

## 4. Scaling Instruction Tuning

Key insight:
- Only ~0.2% instruction data relative to pre-training
- Massive behavior change

Instruction tuning teaches **format, reasoning style, and intent recognition**.

---

## 5. Chain-of-Thought (CoT)

### Idea
Train or prompt models to reason step-by-step.

Benefits:
- Large gains on reasoning tasks
- Especially effective for large models

Limitations:
- Expensive
- Not always helpful

---

## 6. Self-Instruct

### Motivation
Human-written instructions do not scale.

Solution:
- Use strong LLMs to generate instruction–answer pairs
- Filter and fine-tune smaller models

This is *instruction distillation*.

---

## 7. Alpaca

- Teacher: InstructGPT
- Student: LLaMA-7B
- Very low cost
- Strong instruction-following ability

Key lesson:
> Alignment can be distilled cheaply.

---

## 8. Why IT Is Not Enough

Instruction tuning:
- optimizes likelihood
- cannot choose between equally valid answers
- does not encode preferences or safety

→ Need human feedback.

---

## 9. Reinforcement Learning with Human Feedback (RLHF)

### Goal
Align model behavior with:
- helpfulness
- safety
- human values

Approach:
- learn a reward function from human preferences

---

## 10. RLHF Pipeline

1. Pre-training
2. Instruction tuning (SFT)
3. Collect human preference comparisons
4. Train reward model
5. Optimize LM using RL

---

## 11. PPO (Proximal Policy Optimization)

Why PPO:
- prevents catastrophic drift
- constrains updates

Components:
- policy model
- reference model
- reward model
- value model

---

## 12. Limitations of PPO

- Expensive
- Complex
- Sensitive to hyperparameters
- Hard to reproduce

---

## 13. Alternatives

### GRPO
- Group-based rewards
- More stable

### DPO
- Directly optimizes preferences
- Simpler but fragile

---

## 14. Alignment & Bias

RLHF introduces:
- demographic bias
- implicit persona
- value judgments

Alignment ≠ neutrality.

---

## 15. OpinionGPT

Demonstrates:
- bias learned from training data
- difficulty of representing demographics
- importance of data quality

---

## 16. Key Mental Model

- Pre-training: knowledge
- Instruction tuning: usability
- RLHF: alignment
- Scaling amplifies everything

---

## 17. Exam Tips

Be able to explain:
- Why GPT-3 fails at instruction following
- What instruction tuning changes
- Why RLHF is required
- PPO vs DPO vs GRPO

---

## 18. One-Sentence Summary

> Instruction tuning teaches LLMs to follow commands, and RLHF aligns them with human preferences—at the cost of complexity and bias.
