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




---




next:
