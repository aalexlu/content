*February 2, 2023*
previous: [[5 Text Classification 3 - Attention and transformers]]

---

## Transformers
Transforms map an input sequence of vectors to an output sequence of vectors of the same dimensionality
many attention blocks stacked
- Applications
	- Contextual language models, bidirectional attention (BERT)
	- Machine translation
	- Text generation

#### Self-attention
- transforms so you end up having a weighted average
- learning query, key, value
	- ex: comparing the query vector of 'The' with key vector of all other words
	- calculate weighted avg through value vectors
	- then run through softmax for 0-1

Residual layer adds the input of a layer to the output of a layer to preserve what went into it

---

## Modern NLP is driven by annotated data
1. Penn Treebank; morphosyntactic annotations of WSJ
2. OntoNotes; syntax, predicate-argument structure, word sense, coreference
3. FrameNet: frame-semantic lexical/annotations
4. MPQA: opinion/sentiment
5. SQuAD: annotated questions + spans of answers in Wikipedia
- In most cases, the data we have is the product of *human judgements*
	- What's the correct part of speech tag?
	- Syntactic structure?
	- Sentiment?
- Ambiguity

---

## Annotation guidelines
Our goal: given the constraints of our problem, how can we formalize our description of the annotation process to encourage multiple annotators to provide the same judgment?
- What is the goal of the project?
- What is each tag called and how is it used? (Be specific: provide examples, and discuss gray areas.)
- What parts of the text do you want annotated, and what should be left alone?
- How will the annotation be created? (For example, explain which tags or documents to annotate first, how to use the annotation tools, etc.)
Why not do it alone?
- Expensive/time-consuming, multiple people provide consistency, low agreement = not enough training, guideliens not well enough defined
Adjudication
- **Adjudication** is the process of deciding on a single annotation for a piece of text, using information about the *independent annotations*
#### Annotation project tips
- Your annotation task must be one that requires *your human judgement* for the labels
- You should manually be labeling your data, and not using algrotihmic processes to do so
- Your labels should not be deterministic, but really require some human comprehension of the context
- 500 documents as a group – view bcourses

---

## Interannotator agreement
**Cohen's kappa**: If classes are imbalanced, we can get high inter annotator agreement simply by chance
- Expected probability of agreement is how often we would expect two annotators to agree assuming *independent* annotations.
- k = (po - pe) / (1 - pe)
	- po = 88/100 = 0.88
	- pe (expected) = P(A=puppy, B=puppy) + P(A=chicken, B=chicken)
		- = P(A=puppy)P(B=puppy) + P(A=chicken)P(B=chicken)
		- = 0.773
	- k = 0.471
- Very good agreement: 0.8-1.0; Good agreement: 0.6-0.8…
- Cohen's kappa can be used for any number of classes
	- Still requires *two* annotators who evaluate the same items

k = 0
| 0   | 0   |
| --- | --- |
| 0   | 100 |
k = (1-0.5) / (1-0.5)
| 0   | 0   |
| --- | --- |
| 0   | 100 | 
k = -1 (pe = 0.5)
| 0   | 50  |
| --- | --- |
| 50  | 0   |

**Fleiss' kappa** generalizes to *multiple* annotators, each of whom may evaluate *different* items (e.g., crowdsourcing)
- Same fundamental idea of measuring the observed agreement compared to agreement we would expect by chance
- With n > 2, we calculate agreement among *pairs* of annotators

Krippendorf's alpha
- Kappa values still require categorical labels
- What about *real-valued* labels
- How much do our *observed* labels for a document differ from what we'd *expect* given the ratings we see?
	- when one annotator gives this label…how often do we see another with this label for that same item?





next:
