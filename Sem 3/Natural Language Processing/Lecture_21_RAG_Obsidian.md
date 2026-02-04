# Lecture 21 – Retrieval-Augmented Generation (RAG)
#nlp #llm #rag #retrieval #generation #grounding

> These notes explain **why RAG exists, how it works internally, where it fails, and how modern systems improve it**.  

---

## 1. Big Picture: Why RAG Is Necessary

Large Language Models (LLMs) are powerful, but they are **closed-book systems**.

### Core Problems of LLMs
- **Hallucinations** – fluent but false answers  
- **Static knowledge** – frozen at training time  
- **Difficult updates** – retraining is expensive  
- **Lack of domain specificity** – weak on private data  
- **No source attribution** – unverifiable answers  
- **Context limits** – cannot ingest full corpora (e.g. Provide the full Harry Potter book and ask a question about one little part in the book)  

> Key idea: LLMs optimize *plausibility*, not *truth*.

---

## 2. Prompting vs RAG vs Fine-Tuning

### Prompt Engineering
- No training
- Fast iteration
- Weak factual guarantees
- Emotional Prompting can help to get a better answer (10,9% average improvement in performance, truthfullness and responsibility metrics)

### Retrieval-Augmented Generation
- No model training
- Requires database + retriever
- Enables fact grounding and citations

### Fine-Tuning
- Best stylistic control
- Expensive
- Knowledge becomes static again

🧠 **Mental model:**  
Prompting = *how you ask*  
RAG = *what the model knows at runtime*  
Fine-tuning = *how the model speaks*

---

## 3. What Is RAG?

RAG combines:
- **Retrieval** of external documents (External knowledge database, Google etc.)
- **Generation** using an LLM

The model:
1. Retrieves relevant passages
2. Injects them into the prompt
3. Generates a grounded answer

> RAG turns a closed-book LLM into an open-book system.

---

## 4. Foundational Pillars

### Generation (Transformers)
Transformers enable:
- contextual reasoning
- fluent text generation

### Retrieval (Dense Embeddings)
- Text → vectors
- Semantic similarity search
- Neural retrieval instead of keywords

---

## 5. Early RAG Breakthroughs

### REALM
- Retriever + generator trained jointly
- Retrieval becomes learnable

### Dense Passage Retrieval (DPR)
- Separate encoders for queries and passages
- Dot-product similarity
- Contrastive learning

Impact:
- Became the standard retriever for RAG

---

## 6. Canonical RAG Architecture

### Two Memories
- **Parametric**: model weights
- **Non-parametric**: document index

RAG = reasoning over both memories.

---

## 7. RAG Pipeline

1. Embed query
2. Retrieve top-k chunks
3. Inject context
4. Generate answer

Failures can occur at **R**, **A**, or **G**.

---

## 8. Evaluating RAG

### Three Core Metrics
1. Context relevance (retrieval quality)
2. Groundedness / faithfulness (Is the Geneation truthful)
3. Answer relevance

### Tools
- LLM-as-a-judge (RAGAS, TruLens)
- Inverse QA generation
- User feedback

---

## 9. Why RAG Changed Everything

RAG:
- Reduces hallucinations
- Enables up-to-date knowledge
- Adds domain specificity
- Allows verification
- Is cheaper than huge context windows

---

## 10. Why Naive RAG Fails

Simple pipeline:
> chunk → embed → retrieve → generate

Is fragile.

---

## 11. Failure Modes

### Retrieval Failures (R Failures)
- Lexical gap (exact matches fail)
- Short queries vs long documents
- Ignoring structure (tables, PDFs, methods that extract text from documents could fail)

### Augmentation Failures (A Failures)
- Lost-in-the-middle
- Context overload
- Bad chunking

### Generation Failures (G Failures)
- Conflicting internal knowledge
- Yes-man behavior LLM's are trained to be helpful -> often will agree with user
- Over-refusal

---

## 12. Why Not Just Use Long Context?

Because:
- LLMs struggle with mid-context info
- Cost and latency are high

RAG acts as a **precision cache**.

---

## 13. Improving RAG

### Data
- Semantic chunking
- Overlaps
- Structure-aware ingestion

### Retrieval
- Hybrid search
- Re-ranking
- Query rewriting

---

## 14. Advanced RAG

- Iterative / recursive RAG
- Graph RAG
- Agentic RAG

---

## 15. Self-RAG

- Model decides when retrieval is needed
- Uses self-critique
- Improves efficiency and quality

---

## 16. Mental Model

- LLM = fluent guesser
- Retrieval = evidence
- RAG = reasoning over evidence

---

## 17. Exam Tips

Explain:
- Why hallucinations happen
- R vs A vs G failures
- Dense vs sparse retrieval
- Why RAG beats long context

---

## 18. One-Sentence Summary

> Retrieval-Augmented Generation grounds language models in external knowledge, making them factual, up-to-date, and trustworthy.
