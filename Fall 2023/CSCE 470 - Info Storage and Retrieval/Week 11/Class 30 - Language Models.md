# Recap

**Problem**
We need to learn to bridge the gap from "surface level" text representations like the [[Class 06 - Ranking#Vector Space Model|Vector Space Model]] or even [[Class 22 - word2vec|word2vec]] to richer approaches that help us actually answer questions.

**Solution**
We covered the pre ML approach being building a system like [[Class 29 - LLMs Start|AskMSR]] to take advantage of repetition on the Web.

# Language Model Basics

The probability of a sentence or a sequence of words:
$$P(W) = P(w_1, w_2, w_3, ..., w_n)$$

The probability of an upcoming word: 
$$P(w_5|w_1, w_2, w_3, w_4)$$

A model that computes either of these:
$P(w_5|w_1, w_2, w_3, w_4)$ or $P(W)$ is called a **language model**.

## Computing P(W)
We can compute this joint probability using the **Chain Rule of Probability**

### Reminder: The Chain Rule
Recall the definition of conditional probabilities:
$$p(B|A) = P(A,B) / P(A) \rightarrow P(A,B) = P(A)P(B|A)$$

With more variables:
$$P(A,B,C,D) = P(A) * P(B|A) * P(C|A,B)*P(D|A,B,C)$$

The chain rule in general:
$$P(x_1, x_2, x_3, ..., x_n) = \prod_i P(w_i|w_1, w_2, ... w_{i-1})$$

We can apply this chain rule to compute the joint probability of words in a sentence:

$P($ "its water is so transparent" $)$ = $P($ its $) * P($ water | its $) * P($ is | its water $) * P($ so | its water is $) * P($ transparent | its water is so $)$

But what if we just count and divide?
**NO!** That leaves us with too many possible sentences and thus too much data.

## Markov Assumption

Simplifying assumption:

$P($the | its water is to transparent that$) \approx P($ the | that $)$ 
or maybe
$P($the | its water is to transparent that$) \approx P($ the | transparent that $)$ 

In other words, we approximate each component in the product.

**Simplest Case: Unigram Model** ([[Class 29 - LLMs Start#Step 3 Mining N-Grams|N-gram]] for N = 1)

$$P(w_1, w_2, ..., w_n) \approx \prod P(w_i)$$

**Simplest Case: Bigram Model** ([[Class 29 - LLMs Start#Step 3 Mining N-Grams|N-gram]] for N = 2)

$$P(w_i|w_1, w_2, ..., w_{i-1}) \approx P(w_i, w_{i-1})$$

## N-gram models

We can extend the previous concept to trigrams, 4-grams, 5-grams, etc.

In general, this is an insufficient model of language because language has long-distance dependencies:

> e.g. “The computer which I had just put into the machine room on the fifth floor crashed.”  

But we can often get away with N-gram models.

So, **how do we calculate n-gram probabilities?**

$$P(w_i | w_{i-1}) = \frac{count(w_{i-1}, w_i)}{count(w_{i-1})}$$