*January 24, 2023*
previous: [[2 Words, Lexical Semantics, and Static Word Embeddings]]

featurized

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


| task                   | x     | y                                    |
| ---------------------- | ----- | ------------------------------------ |
| language ID            | text  | {english, mandarin, greek, …}        |
| spam classification    | email | {spam, not spam}                     |
| authorship attribution | text  | {jk rowling, james joyce, …}         |
| genre classification   | novel | {detective, romance, gothic, …}      |
| sentiment analysis     | text  | {positive, negative, neutral, mixed} |

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

#### Representation for SA
- only positive / negative words in MPQA
- only words in isolation (bag of words)
	- Bag of words: Representation of text only as the counts of words that it contains (or binary indicator of presence / absence)
- conjunctions of words (sequential, skip ngrams, other non-linear combinations)
- higher-order linguistic structure (e.g., syntax)

--- 

## Features
- logistic regression doesn't assume indep. features; discriminative classifier
- power partly comes in the ability to create richly expressive features without the burden of independence
- can represent text through features that is scoped over the entirety of the input
	- ex: contains 'like', has a word that shows up in positive sentiment dictionary, review begins with 'I like', at least 5 mentions of positive affectual verbs
- Features are where you can encode your own *domain understanding* of the problem.
	- ex: unigrams ('like'), bigrams ('not like'), prefixes ('-un')

| Task | Features |
| -- | -- |
| Sentiment classification | Words, presence in sentiment dictionaries, etc |
| Fake news detection | Credibility of author, sources cited, engagement, extreme language, typos |
| Respect | … |

## Math Stuff
- exp(x) = e^x  = 2.7^x
- log(x) = y -> e^y = x
- exp(x + y) = exp(x) exp(y)
- log(xy) = log(x) + log(y)
- Binary logistic regression
	- P(y = 1 | x, β) = 
	- x = feature vector, β = coefficients

How do we get good values for β?
- For all training data, we want the probability of the true label y for each data point x to be high.

## Logistic regression Gradient descent
- Algorithm –
- If y is 1 and p(x) = 0, then tthis still pushes the weights a lot
- if y is 1 and p(x) = 0.99 then this still pushes the weights just a little bit
## Logistic regression Stochastic Gradient descent
- batch gradient descent reasons over every training data point for each update of β. Can be slow to converge

When calculating the P(y|x) or in calculating the gradient, only need to loop through features with nonzero values
- makes sparse, binary values useful

## Feature Selection
Many features that show up rarely may likeley only appear (by chance) with one label
- Easy to overfit to the randomness of the data
We can account for this with feature selection.
1. We can threshold features by minimum count but that also throws away information
2. We can take a probabalistic approach and encode a prior belief that all β should be 0 unless we have strong evidence otherwise.

L2 regularization
- add a penalty for having values of β that are high
- no L2 regularization vs. some L2 regularization vs. high L2 regularization
L1 regularization
- encourage coefficients to be exactly 0
- n controls for how much of a penalty to pay for coeff. that are far from 0

---

## Evaluation

training, development, testing (80%, 10%, 10%)
- purpose: training models, model selection, evaluation; never look at it until the very end

Multiclass confusion matrix
- diagonal is correct
- Accuracy: sum of diagonal / rest of matrix
- Precision: proportion of predicted class that are actually that class
	- can measure for each specific category
- Recall: proportion of true class that are predicted to be that class
- F score = (2 x precision x recall) / (precision + recall)

Majority class baseline
- pick the label that occurs the most frequently in the training data
- Predict that label for every data point in the test data





next: [[4 Text Classification 2 - MLP and CNN]]