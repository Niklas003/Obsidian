## Representation of words
- one could use one hot encoding -> bad bc. it does not scale good (0 semantics)
- never enoutg training data to handle all possible words

### Lexical Semantics

- group words onto groups
- different words into lemmas
- **Synsens**: tie and necktie are quasi-synonyms

- Organized the whole eng language in sysenses and hyracy
- BabelNet (Word Net) still can not handle misspelled words bc. it was looked only at "clean text"
- but there are ideas to vectorize the words of WordNet
- Hierarchy and distances of words

### Distributional Semantics

- derive meaning of words just by its use
	- example _bariwac_
- make a word co occurence matrix/table
	- then we might see that there are words that co occur bc there occure similar times with each other
	- look at the degree of similaroty (bc they are now vectors and no longer orthoginal)
	- use **cosine similarity** (if angle small -> similar somehow, large -> not so similar)
- we could put that into a vector and might see similarities 
	- antonyms might look quite similar
	- negative vectors cannot accour bc. counts (from the word counting) can only be positive
- but now we dont have the ability of 100% distingush words
- still infinetly many words

- instead of co-occurence we measure statistic significance
- use the PMI instead of word counts
- Still **Problem:** large vocabulary

**How can we compress these large vectors in dense vectors?**
- Single Value decomposition (SVD)

### Takeaways
- computing this is quite expensive

### Word2Vec
- Continuesou bag of words: ate great ____ in Italy.
- Skip-Gram: ??? ??? Pasta ??? ???
- 