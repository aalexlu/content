
## HW1



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