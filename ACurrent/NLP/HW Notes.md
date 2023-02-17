
## HW1: Classification
Featurized Models for Sentiment Analysis
- Generate features for the positive/negative sentiment classification of movie reviews
- Train a model on those features to predict the sentiment of new data

A basic *logistic regression model* (from the scikit-learn package) is trained with your created features to predict each review’s sentiment
**Goal**: featurize the text creatively and optimize the accuracy of the model on the test data

#### Features
1. Bag of words: represent each *lowercase* word tokenized with NLTK; assigned to boolean 1 *(0.776)*
2. Feature 1: Modeled off of the example of Sentiment Classification on page 5 of SLP Ch.5. It takes the positive and negative word counts based on score in AFINN, has a boolean for each punctuation (?, !), and a boolean word no. *(0.734)*
3. Feature 2: This is a modified version of a bag of words; rather than a boolean of existence or a count, the AFINN dictionary score is the key within the dictionary (only non-zero scores). *(0.759)*
4. Feature 3: Adds all bigrams without stop words into the feature dictionary in a similar binary bag-of-words model. *(0.715)*

Features are then combined into one big model to make predictions on the test data. *(0.811)*

---

## HW2 PyTorch and Self-Attention
Exploring PyTorch, a neural network library

### Part 1: PyTorch and FFNN
#### Q1 PyTorch and embeddings
- PyTorch implementation of logistic regression
- How we load and access the GloVe embeddings
- neural net in PyTorch
	1. **forward** method in class that defines architecture
	2. **optimizer** (torch.optim.Adam)
	3. **loss function** (torch.nn.CrossEntropyLoss() combines softmax and negative log-likelihood)
- Input of this model is the *average of GloVe embeddings* for all words in a movie review

**Averaged embeddings vs. BoW**
Averaged GloVe embeddings represent each movie review as the average of the word embeddings for the words in that review, and are able to capture both the semantic meaning and syntactic structure of words. Including this data can help improve model performance compared to using the Bag of Words (BoW) method. BoW is simple and flexible which can be useful in other scenarios such as spam detection, but ignores the order of words in reviews and misses out on the relationships between words which would be useful in this scenario.

**GloVe** is an unsupervised learning algorithm for obtaining vector representations for words
1. Nearest neighbors: The Euclidean distance between two word vectors provides an effective method for measuring the linguistic or semantic similarity of the corresponding words
2. Linear substructures: vector difference between the two word vectors to capture as much meaning as possible
- https://nlp.stanford.edu/projects/glove/

#### Q2 Feedforward neural network (FFNN)
https://www.deeplearningwizard.com/deep_learning/practical_pytorch/pytorch_feedforward_neuralnetwork/
Add a hidden layer to the logistic regression classifier
- In the J&M terminology, a **“two-layer” network** has one hidden layer
- Non-linearity *g*: tanh
- Layer size
	- **Input layer** size is usually determined by the number of input features in the dataset.
		- Ex: if the dataset contains 10 features, the input layer will have 10 neurons.
	- **Hidden layer** size set to be a fraction of the input layer size; between input and output size
		- Here: hiddendim = 20
	- **Output layer** size depends on number of output classes or regression values that the model needs to predict.
		- Ex: if binary classification, output has 1 neuron
		- Ex: if multi-class classification with 5 classes, output layer has 5 neurons
**Implementation**
- INPUT -> linear function -> non-linear tanh function -> linear function -> OUTPUT

**Linear Function**
- Logistic regression problems can represent linear functions well
| INPUT -> Linear() -> | LOGITS -> Logistic() -> | SOFTMAX -> Cross-Entropy() -> | TRUE LABELS  |
| -------------------- | ----------------------- | ----------------------------- | ------------ |
| *1 layer NN*         |                         |                               |              |
| x                    | y                       | g(y)                          | L            |
| [10, 20, 100, 200]   | [1.3, 1.2, 4.5, 4.8]    | [0.1, 0.1, 0.4, 0.4]          | [0, 0, 1, 1] |

**Non-linear Function**
-   Function: takes a number & perform mathematical operation
-   Common Types of Non-linearity (pros and cons for each on website)
    -   ReLUs (Rectified Linear Units)
    -   Sigmoid
    -   Tanh
| INPUT -> Linear() -> | LOGITS -> **Non**-Linear() -> | NON-LINEAR OUTPUT -> Linear() -> | LOGITS -> Softmax() -> | SOFTMAX -> Cross-Entropy() -> | LABELS |
| -------------------- | ----------------------------- | -------------------------------- | ---------------------- | ----------------------------- | ------ |
| *input layer*        | *hidden layer*                | *hidden layer*                   | *readout layer*        | *readout layer*               |        |


### Part 2: Self-attention basics
#### Q3 The concept of self-attention
Simplest form of self-attention: scaled dot-product self-attention
- query, key, and value vectors role in attending to the input sequence
- Wq, Wk, Wv
	- if *query_key_size* = 37, *input_embedding_size* = 2
		- Wq.shape = (2, 37)
		- Wk.shape = (2, 37)
		- Wv.shape = (2, 2)
	- if 5-word sentence represented as **sent**; *input_sentence length* = 5; 
		- sent.shape = (5, 2)
			- each token is represented as embedding of len *input_embedding_size
		- key.shape = (5 x 37)
			- **sent** (5, 2) x **Wq** (2, 37) = **key** (5, 37)
- **Softmax**: normalizes over a set of values 𝑥 = [𝑥1,…,𝑥𝑛] such that each 0≤𝑥𝑖≤1 and the sum of 𝑥 = 1

…The mechanism of *self-attention lies at the core of transformer blocks*, which include the self-attention layer, but also additional feedforward layers, residual connections, and normalizing layers. ChatGPT correctly teaches us that it *takes in a sequence and evaluates each element in a weight-based manner*; at the core, the attention-based approach allows us to *compare an item of interest to other elements within a given sequence* in a way that *reveals its relevance in the current context* and helps us compute an output.

#### Q4: Scaled dot-product attention in NumPy
Attention, given a query vector Q, key vector K and value vector V
- **Attention(Q, K, V)** = softmax ( (Qxtranspose(K)) / (sqrt(*query_key_size*) ) x V
	- Q (5, 37) = input (5, 2) x Wq (2 x 37)
	- K (5, 37) = …
	- V (5, 2) = …

#### Q5: Scaled dot-product attention in PyTorch
Embed attention within a *larger model*
- Ex: 20 words represented by 100-dimensional embedding
- **Input** (20, 100)  ->  **Output** (20, 100)
	- **Average of output embeddings** (1, 100) to generate a final document; a single 100-dim vector
		- Fixed-length vector representation of a sentence or document
	- pass through a fully-connected dense layer (feedforward layers) to make a prediction (pos/neg)
- When used in a model, Wq, Wk, Wv are all trainable matrices; initialized as Linear layers that *transform the input tensor*
	- **forward** creates Q, K, V
	- Q, K vectors used to *calculate attention weights*
	- V vector used to *weigh the scores*


**From SLP 10.1**
- Self-attention allows a network to directly extract and use information from arbitrarily large contexts without the need to pass it through intermediate recurrent connections as in RNNs
- self-attention layer maps input sequences(x1,...,xn) to output sequences of the same length (y1,...,yn)
- The model has access to all of the inputs up to and including the one under consideration, but no access to information about inputs beyond the current one. 
	- The computation performed for each item is independent of all the other computations
- At the core of an attention-based approach is the ability to *compare* an item of interest to a collection of other items in a way that reveals their relevance in the current context. In the case of self-attention, the set of comparisons are to other elements within a given sequence. The result of these comparisons is then used to compute an output for the current input.
- Consider the three different roles that each input embedding plays during the course of the attention process.
	- As the current focus of attention when being compared to all of the other query preceding inputs. We’ll refer to this role as a **query**.
	- In its role as a preceding input being compared to the current focus of attention. We’ll refer to this role as a **key**
	- And finally, as a **value** used to compute the output for the current focus of attention.
- **Transformer blocks**
	- The self-attention calculation lies at the core of what’s called a transformer block, which, in addition to the self-attention layer, includes additional feedforward layers, residual connections, and normalizing layers.
- **Multi-head attention layer**
	- The different words in a sentence can relate to each other in many different ways simultaneously. For example, distinct syntactic, semantic, and discourse relationships can hold between verbs and their arguments in a sentence. It would be difficult for a single transformer block to learn to capture all of the different kinds of parallel relations among its inputs. Transformers address this issue with multihead self-attention layers. These are sets of self-attention layers, called heads, that reside in parallel layers at the same depth in a model, each with its own set of parameters.
- Modeling word order: **positional embeddings**
	- Transformers don't have notions of position unlike how it's built in for RNNs
		- One simple solution is to modify the input embeddings by combining them with positional embeddings specific to each position in an input sequence.
	- As with word embeddings, these positional embeddings are learned along with other parameters during training

Transformer Neural Networks - EXPLAINED! (Attention is all you need)
https://www.youtube.com/watch?v=TQQlZhbC5ps

---

## HW3: Masked Language Models, BERT, and Perplexity
### Part 1: Making approach for transformer-based language models
_masking_: preventing a model from seeing specific tokens in the input during training
BERT training relies on _masked language modeling_: masking a random set of input tokens in a sequence and attempting to predict them
- BERT is _bidirectional_, so that it can use all of the other non-masked tokens in a sentence to make that prediction
The GPT class of models acts as a traditional left-to-right language model (causal LM)
- also uses self-attention based transformers
- but word w at position i (wi) only has access to info about w1, … ,wi-1

in the masks
- 1 denotes that a position should be hidden
- 0 denotes that it should be visible

#### Q1 BERT Mask
Create a mask that randomly masks token positions 2 and 7

#### Q2 Causal Mask
When making a prediction for the word wi at position i, it can only use information about words wi , . . . , wi−1 to do so
All of the other tokens following position i − 1 must be *masked*

#### Q3 Input/outputs for causal language model
We provide the training structure for a left-to-right causal language model; all that is needed is the correct inputs (x) and outputs (y)

Write a function that takes in a sequence of token ids [w1, . . . , wn] and segments it into 8-token chunks – e.g., x1 = [w1, . . . , w8], x2 = [w9, . . . , w16]

For each xi , also create its corresponding yi
- Each yi should also contain 8 values
At token position i, when a model has access to [w1, . . . , wi ], which is the true yi for that position? Each element in y should be a word ID

#### Q4 Write-up
In this model, as implemented, does the following equivalence hold?
	𝑃(𝑦4∣𝑤1=go,𝑤2=ahead,𝑤3=make,𝑤4=my)=𝑃(𝑦4∣𝑤1=ahead,𝑤2=my,𝑤3=make,𝑤4=go)
Why or why not?

X Since our language model is a left-to-right causal language model, the probability of generating each token in the sequence only depends on the tokens that have been generated previously. Therefore, the equivalence does hold, as 𝑦4, the next word being predicted in the sequence will be based on the same four previous words 𝑤1=go, 𝑤2=ahead, 𝑤3=make, and 𝑤4=my. In this type of model, the probability will be the same regardless of the order of the tokens in this model, as long as the tokens are the same.

√ The probability of the next word 'y4' would not be the same in these two cases. In a left-to-right causal language model, the probability of the next word does depend on the order of the preceding words. In the first case, the context is "go ahead make my", and in the second case, the context is "ahead my make go". Even though the four words are the same, the order in which they appear does affect the conditional probability of the next word.

𝑃(𝑦4|𝑤1=go) * 𝑃(𝑦4|𝑤1=go,𝑤2=ahead) * 𝑃(𝑦4|𝑤1=go,𝑤2=ahead,𝑤3=make) * 𝑃(𝑦4𝑤1=go,𝑤2=ahead,𝑤3=make,𝑤4=my)
will be equal to
𝑃(𝑦4|𝑤1=ahead) * 𝑃(𝑦4|𝑤1=ahead,𝑤2=my) * 𝑃(𝑦4|𝑤1=ahead,𝑤2=my,𝑤3=make) * 𝑃(𝑦4|𝑤1=ahead,𝑤2=my,𝑤3=make,𝑤4=go)


### Part 2: Perplexity and implementing pseudo-perplexity for BERT
The **perplexity** of a language model (PP) on a test set is the inverse probability of the test set, normalized by the number of words
- However, since these probabilities are often small, taking the inverse and multiplying can be numerically unstable, so we often first compute these values in the log domain and then convert back.

#### Q5 Pseudo-perplexity for BERT
The perplexity calculation above presumes a left-to-right causal language model

*Helpful code blocks:*
1. BERT tokenizer tokenizes a sentence into a sequence of WordPiece ids. Note how BERT tokenization automatically wraps an input sentences with [CLS] and [SEP] tags
2. How we can calculate output probabilities using this model. The output of each token position 𝑖 gives us 𝑃(𝑤𝑖∣𝑤1,…,𝑤𝑛)---the probability of the word at that position over our vocabulary, given _all_ of the words in the sentence
3. BERT's `attention_mask` function only works for padding tokens; to mask input tokens, we need to intervene in the input andreplace a WordPiece token that we're predicting with a special [MASK] token (BERT tokenizer word id `103`).

**Implementation**
- tensor_input: encodes the input sentence using tokenizer
	- {'input_ids': tensor, 'token_type_ids': tensor, 'attention_mask': tensor}
- tensor_input_ids: input ids in tensor form
	- tensor([101, 2414, 2003, 1996, 3007, 1997, 1996, 2142, 2983, 1012, 102])
- input_ints: integer values within the tensor: 'input_ids'
	- [101, 2414, 2003, 1996, 3007, 1997, 1996, 2142, 2983, 1012, 102]
- wp_tokens: the words associated with input_ints
	- ['[CLS]', 'london', 'is', 'the', 'capital', 'of', 'the', 'united', 'kingdom', '.', '[SEP]']

To calculate *the probability of a word at position i* given all of the other words in the sentence
1. For each word i in a sentence, one at a time
2. We mask that word (Set input_id in tensor to "[MASK]") from the input and run the entire sentence through BERT to predict the probability of that masked word
3. Calculate the probability of the true word at the masked position and use that in the PP(W) equation
	- e ^ ((1/N) x SUMMATION(−ln(P(wi|w1...wi−1,wi+1,...,wn)))
	- 1.04856

---

## HW4: 
