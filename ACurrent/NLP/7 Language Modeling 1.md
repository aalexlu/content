*February 7, 2023*
previous: [[6 Annotation]]

---
Building models that can tell us things in NLP

## Language Model
- Language models provide us with a way to quantify the likelihood of a sequence — i.e., plausible sentences.
- Vocabulary *V* is a finite set of discrete sybols (words, characters); V = | *V* |
- *V+* is the infinite set of sequences of symbols from *V*; each sequence ends with STOP
- x ∈ *V+* (a given sentence)
- **P(w)** = P(w1, …, wn)
	- P("Call me Ishmail") = P(w1 = “call”, w2 = “me”, w3 = “Ishmael”) x P(STOP)

1. Optical Character Recognition (OCR) – picture of text, what do the characters / pixels look like
2. Machine translation (MT)
	- **fidelity** (to source text) how much meaning from the English is in the Italian
	- **fluency** (of the translation)
3. Speech recognition
4. Dialogue generation (Q -> A)

Start with an X, come out with a Y
- Given X, give me the probability of Y, so I can pick which Y has the highest probability of being my best guess
|     | X               | Y             |
| --- | --------------- | ------------- |
| ASR | speech signal   | transcription |
| MT  | target text     | source text   |
| OCR | pixel densities | transcription |

**The fundamental task:**
#### Language modeling is the task of estimating P(w)
- Chain rule of probability
- Markov assumption
	- Need the probability of one word to get the probability of the next
	- bigram model (first-order markov)
	- trigram model (second-order markov) – relies on previous two words
- Estimation
- Generating: As we sample, the words we generate form the new context we condition on - sample until STOP symbol
	- Unigram model < bigram model (pairs make sense but not quite) < trigram model (better)
	- none are global

#### Evaluation
- The best evaluation metrics are *external* – how does a better language model influence the application you care about?
- Speech recognition (word error rate), machine translation (BLEU score), topic models (sensemaking)
- A good language model should judge *unseen real language* to have high probability
- **Perplexity** = inverse probability of test data, averaged by word.
	- want it to be lower
	- 
- To be reliable, the test data must by truly unseen (including knowledge of its vocabulary)

Interpolation
- As ngram order rises, we have the potential for higher *precision* but also higher *variability* in our estimates.
- A linear interpolation of any two language models p and q (with lambda ∈ [0,1]) is also a valid language model.
- We can use this fact to make higher-order language models more *robust*

---

#### Multi-class Logistic Regression
We can use multiclass logistic regression for alnguage modeling by treating the vocab as the output space
Smoothing can combine second and first-order markov in one

Tradeoffs
- Richer representations than just markov assumptions; more parameters, higher likelihood of overfitting
- Much


---

## Why?

- Language models give us an estimate for the probability of a sequence, which is directly useful for applications that are deciding between different sentences as viable outputs:
	- Machine translation
	- Speech recognition
	- OCR
	- Dialogue agents
- Language models directly allow us to predict the next word in a sequence (useful for *autocomplete*)
- Language models can directly encode knowledge present in the training corpus
- Language modeling turns out to be a good proxy task for learning about linguistic structure
	- See contextual word embeddings (BERT)
- 


next: [[8 Language Modeling 2 - Contextual embeddings]]
