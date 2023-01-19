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
- 
