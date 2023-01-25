*January 24, 2023*
previous: [[2 Words, Lexical Semantics, and Static Word Embeddings]]

---

## Classification
A mapping *h* from input data x (drawn from instance space X) to a categorical label (or labels) y from some enumerable output space y
- X = set of all documents
- Y = {english, mandarin, greek, …}
- x = a single document
- y = ancient greek
discrete class

Let h(x) be the "true" mapping. We never know it. How do we find the best ĥ(x) to approximate it?
1. **Rule based**: if x has characters in unicode point range 0370-03FF: ĥ(x) = greek
2. **Supervised learning**: Given training data in the form of <x, y> pairs, learn ĥ(x)
ĥ(x): The classification function that we want to learn has two different components:
1. the formal structure of the learning method (what’s the relationship between the input and output?) → Naive Bayes, logistic regression, convolutional neural network, etc.
2. the representation of the data


| task | x | y |
|--|--|---|
| language ID | text | {english, mandarin, greek, …} |
| spam classification | email | {spam, not spam} |
| authorship attribution | text | {jk rowling, james joyce, …} |
| genre classification | novel | {detective, romance, gothic, …} |
| sentiment analysis | text | {positive, negative, neutral, mixed} |

---

## Sentiment analysis
- Document-level SA: is the entire text positive or negative (or both / neither) with respect to an implicit target OR explicit target within the text?
- Movie reviews
Sentiment as Tone: No longer the speaker’s attitude with respect to some particular target, but rather the positive/negative tone that is evinced.
- People happiest at 8am

Sentiment Dictionaries
- list of positive vs negative words
- LIWC: 73 separate lexicons designed for applications in social psychology (e.g. Emotion, Insight, Inhibition, Family, Negate)

Why is Sentiment Analysis (SA) hard?
- Sentiment is a measure of a speaker's private state, which is unobservable
- Sometimes words are a good indicator of sentiment (love, amazing, hate, terrible); many times it requires deep world + contextual knowledge

Representation for SA
- only positive / negative words in MPQA
- only words in isolation (bag of words)
	- Bag of words: Representation of text only as the counts of words that it contains (or binary indicator of presence / absence)
- conjunctions of words (sequential, skip ngrams, other non-linear combinations)
- higher-order linguistic structure (e.g., syntax)

--- 

Math Stuff
- exp(x) = e^x  = 2.7^x
- log(x) = y -> e^y = x
- exp(x + y) = exp(x) exp(y)
- log(xy) = log(x) + log(y)
- Binary logistic regression
	- P(y = 1 | x, β) = 
	- x = feature vector, β = coefficients

## Features
- logistic regression doesn't assume indep. features; discriminative classifier
- power partly comes in the ability to create richly expressive features without the burden of independence
- can represent text through features that is scoped over the entirety of the input
	- ex: contains 'like', has a word that shows up in positive sentiment dictionary, review begins with 'I like', at least 5 mentions of positive affectual verbs
- Features are where you can encode your own *domain understanding* of the problem.
	- ex: unigrams ('like'), bigrams ('not like'), prefixes ('-un')

How do we get good values for β?
- For all training data, we want the probability of the true label y for each data point x to be high.


---

## Topic



next: 