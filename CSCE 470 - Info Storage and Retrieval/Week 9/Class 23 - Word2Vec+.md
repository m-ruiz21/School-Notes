## Review
Last time, we talked about embedding words into vectors.
The hope of this is to capture the "semantics" of words. 
So if you do "king - man + woman" you should get a vector similar to the vector for "queen".
## Word2Vec
A framework for learning word vectors. 

**Big Idea:**
 - We have a large selection of text: a long list of words.
 - Every word in a fixed vocabulary is represented by a vector.
 - Go through each position t in the text, which has center word c and context ("outside") words o.
 - Use the similarity of the word vectors for c and o to calculate the probability of o given c (or vice versa).
 - Keep adjusting vectors to maximize this probability.

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