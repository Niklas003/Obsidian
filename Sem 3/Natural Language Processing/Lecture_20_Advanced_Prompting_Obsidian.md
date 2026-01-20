# Lecture 20 – Advanced LLM Prompting Techniques
#nlp #llm #prompting #in-context-learning #evaluation

> Obsidian-ready notes explaining **how prompting replaces fine-tuning, why it is brittle, and how advanced prompting techniques mitigate this**.

---

## 1. From Fine-Tuning to Prompting

Old paradigm:
- Pre-train → Fine-tune
- Weights mutable
- High cost, best raw performance

New paradigm:
- Pre-train → Prompt
- Weights frozen
- Fast iteration, no training

🧠 Prompting controls *behavior*, not *knowledge*.

---

## 2. Why Prompting Works

LLMs learn:
- statistical patterns of tasks
- input/output formats
- latent instructions

Prompts activate these patterns via **in-context learning**.

---

## 3. Zero-, One-, and Few-Shot Prompting

- Zero-shot: task description only
- One-shot: one example
- Few-shot: multiple examples

Few-shot usually performs best, but is sensitive to order and balance.

---

## 4. Evaluation Is Non-Trivial

Classic metrics (BLEU, ROUGE):
- penalize paraphrases
- fail for creative reasoning

LLM outputs are **non-deterministic**.

---

## 5. Human Evaluation Pitfalls

Humans prefer:
- verbosity
- confidence

Even if reasoning is wrong → *reasoning gap problem*.

---

## 6. Prompt Failure Modes

- Instruction-following failures
- Format violations
- Hallucinations
- Over-refusals

---

## 7. Prompt Robustness

LLMs are stochastic:
- temperature = 0 ≠ deterministic

Best practices:
- multi-seed testing
- prompt paraphrasing
- example shuffling

---

## 8. Sensitivity & Calibration

LLMs exhibit:
- majority label bias
- recency bias
- common token bias

Contextual calibration corrects these biases.

---

## 9. Chain-of-Thought (CoT)

Forces step-by-step reasoning.

Benefits:
- improves math & logic
- increases effective depth

---

## 10. Self-Consistency

- Sample multiple CoTs
- Majority vote

Acts as **decoding ensemble**.

---

## 11. Least-to-Most Decomposition

Break complex problems into sub-problems.

Keeps reasoning in-distribution.

---

## 12. Optimizing Few-Shot Context

Dynamic kNN selection:
- embed query
- retrieve relevant examples
- insert selectively

---

## 13. Context Optimization Tricks

- Explicit definitions
- Negative constraints
- Output skeletons

---

## 14. LLM-as-a-Judge

Use strong models to evaluate weaker ones.

Scales evaluation but introduces judge bias.

---

## 15. Automatic Prompt Engineering (APE)

Treat prompts as a search problem:
- generate variants
- evaluate
- select best

---

## 16. Prompt Programming (DSPy)

Abstract prompt logic into modules.

Prompts become trainable components.

---

## 17. Exam Takeaway

> Prompting is powerful but fragile—robustness, calibration, and evaluation are the core challenges.
