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
1. Rule based: if x has characters in unicode point range 0370-03FF: ĥ(x) = greek
2. Supervised learning: Given training data in the form of <x, y> pairs, learn ĥ(x)

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

Why is Snetiment Analysis (SA) hard?



---

## Topic



next: 