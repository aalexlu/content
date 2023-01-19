*January 19, 2023*

---

## Words
as dimensionality reduction (cat)

Type: abstract descriptive concept
Token: instantiation of a type

*"to be or not to be"*
- 6 tokens (to, be, or, not, to, be)
- 4 types (to, be, not, or)

How can we use types and tokens to determine vocabulary richness?
- type / token ratio

---

## Sentence segmentation
Whitespace – `text.split("")`
- explosion of tokenization with this method due to punctuation
- but we typically don't want to just strip all punctuation
	- signals boundaries (sentence, clausal boundaries, parentheticals, asides)
	- some punctuation has illocutionary force (e.g. !, ?)
	- emoticons are strong signals (e.g. sentiment)
Regular Expressions
- Most tokenization algorithms (for languages delimited by whitespace) use regex to segment a string into discrete tokens.
https://bit.ly/3XCiOGQ

## Sentence Segmentation (Syntax)
- Word tokenization presumes a preprocessing step of sentence segmentation – identifying the boundaries between sentences
- Lots of NLP operates at the level of the sentence – important to get it right
- Harder to write regexes to delimit these – there are many cases where the usual delimiters (periods, question marks) serve double duty
```
import nltk
tokens = nltk.word_tokenize(text)
```
- tokenizes following the conentions of the Penn Treebank
- Punkt sentence tokenizer — unsupervised method to learn common abbreviations, collocations, sentence-initial words. Can be trained on data from new domain.
```
import spacy
```
- Relies on dependency parsing to find sentence boundaries

---

## Stemming and lemmatization (Morphological)
- Many languages have some inflectional and derivational morphology, where similar words have similar forms: organizes, organized, organizing
- Stemming and lemmatization reduce this variety to a single common base form.

Stemming
- Heuristic process for chopping off the inflected suffixes of a word
	- organizes, organized, organizing → organ
- Porter Stemmer: Sequence of rules for removing suffixes from words
Lemmatization
- Using morphological analysis to return the dictionary form of a word (the entry in a dictionary you’d find all forms under)
	- organizes, organized, organizing → organize
```
import spacy
nlp = spacy.load(‘en_core_web_sm')
lemmas=[token.lemma_ for token in nlp(text)]
```

---

## Lexical Semantics

"You shall know a word by the company it keeps"
- everyone likes __ (noun)
- a bottle of __ is on the table (liquid)
- __ makes you drunk (can be metaphorical)

## Distributed representation
- Vector representation that encodes information about the distribution of contexts a word appears in
	- distribution of words around the word we're looking at
- Words that appear in similar contexts have similar representations (and similar meanings, by the distributional hypothesis)
- We have several different ways we can encode the notion of **"context"**
	- Term-document matrix: content = appearing in the same document
		- Vectors: Vector representation of the term; vector size = number of documents
			- Cosine Similarity
				- calculate the cosine similarity of two vectors to judge the degree of their similarity
				- Euclidean distance measures the magnitude of distance between two points
				- Cosine similarity measures their orientation
	- Term-context matrix
		- Rows and columns are both words
		- cell counts = the number of times word wi and wj show up in the same context (e.g., a window of 2 tokens).
	- Directional ngrams
		- a defined order occurring to the left or right of the term
	- Syntactic context


Weighting dimentions
- not all dimensions are equally informative
## TF-IDF (Term frequency-inverse document frequency)
- A scaling to represent a feature as function of how frequently it appears in a data point but accounting for its frequency in the overall collection
- IDF for a given term = the number of documents in collection / number of documents that contain term
- Term frequency (tft,d) = the number of times term t occurs in document d; several variants (e.g., passing through log function)
- Inverse document frequency = inverse fraction of number of documents containing (Dt) among total number of documents N
	- IDF for words that appear in every document => 0
## PMI
- Mutual information provides a measure of how independent two variables (X and Y) are
- Pointwise mutual information measures the independence of two outcomes (x and y)
