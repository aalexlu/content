*January 31, 2023*
previous: [[4 Text Classification 2 - MLP and CNN]]
Cherokee Cover
- Language Revitalization through NLP

---

How do we use word emmbeddings for document classification?
- Aggregation operation: take sum, take avg (every word equally imp.), take max 
	- Weighted sum: scale words based on their importance

## Attention
Let’s incorporate structure (and parameters) into a network that captures *which elements in the input we should be attending to* (and which we can ignore).
- Define v to be a vector to be learned – “important word” vector; the dot product here measures how similar each input vector is to that “important word” vector
- r1 = v⊤ x1 for each word

Variations on attention:
1. Linear transformation of xinto before dotting with v
2. Non-linearities after each operation
3. “Multi-head attention”: multiple v vectors to capture different phenomena that can be attended to in the input.
4. Hierarchical attention (sentence representation with attention over words + document representation with attention over sentences).

Attention gives us a normalized weight for every tokeni n a sequence that tells us how imp. that word was for the prediction
- Can be useful for visualization


---

## Transformers
Transformers map an input *sequence* of vectos to an output *sequence* of vectors of the same dimensionality
Core idea behind transformers; How attention operates

#### Self-Attention
1. Let's assume that our input vectors are static word2vec embeddings of words
2. The value for time step j at layer i is the result of attention over all time steps in the previous layer i-1

Separate out representations into query and key and value
- These are all parameters we learn. 100 is the original input dimension; 37 is a hyperparameter we choose.
Self attention from "**The**" at position 1 to every token in the sentence ("The dog barked")
- The compatibility score between two words is the dot product between their respective *query* and *key* vectors
	- score(ei, ej) = qi * kj
- The output of attention is a weighted sum over the values of the previous layer
	- The (0.07), dog (0.58), barked (0.35)
	- If the dimensionality of v is 100, the resulting vector is also size 100

---

## Multihead attention
Attention in transformers is essentially a set of *learned parameters* (WQ, WK, WV) and a mathematical expression for *how an input is transformed into an output* through operations involving those parameters.
- Q = XWQ; K = XWK; V = XWV
- SelfAttention(Q,K, V) =
Attention provides one view on the data
- just like we use multiple filters in CNNs to provide multiple perspectives (by learning separate parameters for each one), we learn multiple perspectives in a transformer by learning multiple (WQ, WK, WV) sets.



next:
