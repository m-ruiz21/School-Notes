## Review
Last time, we talked about embedding words into vectors.
The hope of this is to capture the "semantics" of words. 
So if you do "king - man + woman" you should get a vector similar to the vector for "queen".
## Word2Vec
Last time, we talked about [[Class 22 - word2vec|Word2Vec]], a framework for learning word vectors. 

This is done through:
$$ \begin{align} ((t_{in})^T \times w_{in}) \times w_{out} = (t_{i + j})^T\end{align} $$

where $w_{in}$ is the embeddings of the words whenever they are the center word and $w_{out}$ is the embeddings of the words whenever they are the outer "context" words.

> Note the same word might have different embeddings in both vectors. 
 
> we can think of $w_{in}$ as measuring the "definition" while $w_{out}$ measures its actual contribution to the context.
### Example:
So set up with 1 billion docs and then read them word by word. This is going to generate a dictionary of unique words. 

At this point, number of words = |V|.
**GOAL**:  find embeddings for every word (decrease vector) in our vocabulary to reduce the dimensions for our vector to a smaller number like 50. 
## Softmax
Transforms a vector or reals into a probability distribution (non negative and sums to 1).

$$ \begin{align} f_i(x) = \frac{exp(x_i)}{\sum_j exp(x_j)}\end{align} $$

How can we solve this? Through Stochastic gradient descent!