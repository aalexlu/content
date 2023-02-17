
## HW1


---

## HW2

https://www.deeplearningwizard.com/deep_learning/practical_pytorch/pytorch_feedforward_neuralnetwork/

#### Linear function
- Logistic regression problems can represent linear functions well
- View image: https://www.deeplearningwizard.com/deep_learning/practical_pytorch/images/cross_entropy_final_4.png

#### Non-linear Function
-   Function: takes a number & perform mathematical operation
-   Common Types of Non-linearity (pros and cons for each on website)
    -   ReLUs (Rectified Linear Units)
    -   Sigmoid
    -   Tanh
- View image: https://www.deeplearningwizard.com/deep_learning/practical_pytorch/images/logistic_regression_comparison_nn5.png
	- Hidden layer

#### Self-attention
- simplest form of self-attention: scaled dot-product self-attention
	- query, key, and value vectors role in attending to the input sequence
- From SLP 10.1
	- Self-attention allows a network to directly extract and use information from arbitrarily large contexts without the need to pass it through intermediate recurrent connections as in RNNs
	- self-attention layer maps input sequences(x1,...,xn) to output sequences of the same length (y1,...,yn)
	- the model has access to all of the inputs up to and including the one under consideration, but no access to information about inputs beyond the current one. In addition, the computation performed for each item is independent of all the other computations
	- At the core of an attention-based approach is the ability to *compare* an item of interest to a collection of other items in a way that reveals their relevance in the current context. In the case of self-attention, the set of comparisons are to other elements within a given sequence. The result of these comparisons is then used to compute an output for the current input.
	- Consider the three different roles that each input embedding plays during the course of the attention process.
		- As the current focus of attention when being compared to all of the other query preceding inputs. We’ll refer to this role as a **query**.
		- In its role as a preceding input being compared to the current focus of attention. We’ll refer to this role as a **key**
		- And finally, as a value used to compute the output for the current focus of attention.
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

## HW3
#### Part 1: Making approach for transformer-based language models
_masking_: preventing a model from seeing specific tokens in the input during training
BERT training relies on _masked language modeling_: masking a random set of input tokens in a sequence and attempting to predict them
- BERT is _bidirectional_, so that it can use all of the other non-masked tokens in a sentence to make that prediction
The GPT class of models acts as a traditional left-to-right language model (causal LM)
- also uses self-attention based transformers
- but word w at position i (wi) only has access to info about w1, … ,wi-1

in the masks
- 1 denotes that a position should be hidden
- 0 denotes that it should be visible

**Q1 BERT Mask**
Create a mask that randomly masks token positions 2 and 7

**Q2 Causal Mask**
When making a prediction for the word wi at position i, it can only use information about words wi , . . . , wi−1 to do so
All of the other tokens following position i − 1 must be *masked*

**Q3 Input/outputs for causal language model**
We provide the training structure for a left-to-right causal language model; all that is needed is the correct inputs (x) and outputs (y)

Write a function that takes in a sequence of token ids [w1, . . . , wn] and segments it into 8-token chunks – e.g., x1 = [w1, . . . , w8], x2 = [w9, . . . , w16]

For each xi , also create its corresponding yi
- Each yi should also contain 8 values
At token position i, when a model has access to [w1, . . . , wi ], which is the true yi for that position? Each element in y should be a word ID

**Q4 Write-up**
In this model, as implemented, does the following equivalence hold?
	𝑃(𝑦4∣𝑤1=go,𝑤2=ahead,𝑤3=make,𝑤4=my)=𝑃(𝑦4∣𝑤1=ahead,𝑤2=my,𝑤3=make,𝑤4=go)
Why or why not?

Since our language model satisfies the left-to-right causal property, and the probability of generating each token in the sequence only depends on the tokens that have been generated previously, the equivalence does hold. 𝑦4, the next word in the sequence that the language model is predicting, will be based on the same four previous words 𝑤1=go, 𝑤2=ahead, 𝑤3=make and 𝑤4=my, and the order does not affect the probability in our left-to-right causal language model.

𝑃(𝑦4|𝑤1=go) * 𝑃(𝑦4|𝑤1=go,𝑤2=ahead) * 𝑃(𝑦4|𝑤1=go,𝑤2=ahead,𝑤3=make) * 𝑃(𝑦4𝑤1=go,𝑤2=ahead,𝑤3=make,𝑤4=my)
will be equal to
𝑃(𝑦4|𝑤1=ahead) * 𝑃(𝑦4|𝑤1=ahead,𝑤2=my) * 𝑃(𝑦4|𝑤1=ahead,𝑤2=my,𝑤3=make) * 𝑃(𝑦4|𝑤1=ahead,𝑤2=my,𝑤3=make,𝑤4=go)


#### Part 2: Perplexity and implementing pseudo-perplexity for BERT
The **perplexity** of a language model (PP) on a test set is the inverse probability of the test set, normalized by the number of words
- However, since these probabilities are often small, taking the inverse and multiplying can be numerically unstable, so we often first compute these values in the log domain and then convert back.

**Q5 Pseudo-perplexity for BERT**
The perplexity calculation above presumes a left-to-right causal language model

*Helpful code blocks:*
1. BERT tokenizer tokenizes a sentence into a sequence of WordPiece ids. Note how BERT tokenization automatically wraps an input sentences with [CLS] and [SEP] tags
2. How we can calculate output probabilities using this model. The output of each token position 𝑖 gives us 𝑃(𝑤𝑖∣𝑤1,…,𝑤𝑛)---the probability of the word at that position over our vocabulary, given _all_ of the words in the sentence
3. BERT's `attention_mask` function only works for padding tokens; to mask input tokens, we need to intervene in the input andreplace a WordPiece token that we're predicting with a special [MASK] token (BERT tokenizer word id `103`).

Implementation
- tensor_input: encodes the input sentence using tokenizer
	- {'input_ids': tensor, 'token_type_ids': tensor, 'attention_mask': tensor}
- tensor_input_ids: input ids in tensor form
	- tensor([101, 2414, 2003, 1996, 3007, 1997, 1996, 2142, 2983, 1012, 102])
- input_ints: integer values within the tensor: 'input_ids'
	- [101, 2414, 2003, 1996, 3007, 1997, 1996, 2142, 2983, 1012, 102]
- wp_tokens: the words associated with input_ints
	- ['[CLS]', 'london', 'is', 'the', 'capital', 'of', 'the', 'united', 'kingdom', '.', '[SEP]']

For each WordPiece token
To calculate *the probability of a word at position i* given all of the other words in the sentence
1. For each word i in a sentence, one at a time
2. We mask that word (Set input_id in tensor to "[MASK]") from the input and run the entire sentence through BERT to predict the probability of that masked word
3. Calculate the probability of the true word at the masked position and use that in the PP(W) equation
	- e ^ ((1/N) x SUMMATION(−ln(P(wi|w1...wi−1,wi+1,...,wn)))
	- 1.04856